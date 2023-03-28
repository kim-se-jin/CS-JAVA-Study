# Synchronous x Asynchronous & blocking x non-bloking

### Q) 동기, 비동기, 블락킹, 논블락킹에 대해 간략히 설명해주세요.

- 동기

  - 여러 작업들을 순차적으로 실행합니다.

- 비동기
  - 여러 작업들을 독립적으로 실행합니다.

<img width="500" alt="syn_async" src="https://user-images.githubusercontent.com/43171179/228144302-1ba4693d-ec62-4ccd-ae5c-289f1c27d036.png">

- blocking
  - 작업을 요청한 프로세스/스레드는 요청이 완료될 때까지 블락됩니다.
    <img width="500" alt="syn_async" src="https://user-images.githubusercontent.com/43171179/228145313-05379635-f15b-449a-802b-daacdb6163cd.png">
- non-blocking
  - 프로세스, 스레드를 블락시키지 않고 요청에 대한 현재 상태를 즉시 반환합니다.
    <img width="500" alt="syn_async" src="https://user-images.githubusercontent.com/43171179/228145317-82118d1a-ccc6-4e4c-8a36-da3a7f7d36a2.png">

> ### Q) 비동기처리를 하는 예시를 들어주세요.

- 비동기 처리의 대표적인 예시는 자바스크립트의 setTimeout같은 웹 API가 있습니다.

```jsx
setTimeout(() => {
  console.log("1번");
}, 5000);
setTimeout(() => {
  console.log("2번");
}, 3000);
setTimeout(() => {
  console.log("3번");
}, 1000);
console.log("4번");
// 4번->(1초)->3번->(2초)->2번->(2초)->1번
```

적힌 순서대로 1번 2번 3번 4번으로 될 것 같지만, `setTimeout`은 비동기 함수이기 때문에 완전히 다른 결과가 나오게 됩니다.
`setTimeout`이 만약 동기적으로 처리됐다면 5초뒤 1번이, 3초뒤 2번이, 1초뒤 호출되어 총 8초가 걸렸겠지만,비동기적으로 처리됐기 때문에 전체 걸린 시간은 5초가 된 것입니다.

> ### Q) Java에서도 비동기처리를 하는 예시를 들어주세요.

- #### execute

  - runnable 인터페이스 필요, result값 설정 가능
  - runnable - 객체를 리턴하지 않음, exception 발생시키지 않음
    고로, 객체를 리턴할 필요가 없을 때 사용한다.
  - shutdown() 걸어줘야 함.

  exit 우선 출력
  2초 후 Hello 출력

```java
public class FutureEx {
    public static void main(String[] args) {
        ExecutorService es = Executors.newCachedThreadPool();
        es.execute(() -> {
            try {
                Thread.sleep(2000); //interrupt 발생시 exception 던질 수 있도록
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            log.info("Hello");
        });
        log.info("Exit");
    }
}

```

```
[main] INFO com.example.demo.FutureEx - Exit
[pool-1-thread-1] INFO com.example.demo.FutureEx - Hello
```

- #### submit
  - runnable, callable 인터페이스 사용 가능
  - runnable - 객체를 리턴하지 않음, exception 발생시키지 않음
  - callable - 값 리턴 가능, exception 발생시킬 수 있음
  - 객체 리턴이 필요하거나 exception 발생이 필요할 때 사용한다.

```java

public class FutureEx {
    public static void main(String[] args) {
        ExecutorService es = Executors.newCachedThreadPool();
        es.submit(() -> {
            Thread.sleep(2000); //interrupt 발생시 exception 던질 수 있도록
            log.info("Async");
            return "Hello";
        });
        log.info("Exit");
    }
}
```

- #### FutureTask

Future 자체를 Object로 만들어준다.

```java
public class FutureEx {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        ExecutorService es = Executors.newCachedThreadPool();
        FutureTask<String> f = new FutureTask<>(()->{
            Thread.sleep(2000);
            log.info("Async");
            return "Hello";
        });
        es.execute(f);

        System.out.println(f.isDone()); //즉시 리턴(작업이 완료되었는지)
        Thread.sleep(2100);
        log.info("Exit");
        System.out.println(f.isDone());
        System.out.println(f.get());
    }
}

```

- FutureTask에 익명클래스로 done()메서드를 추가한 코드

  - 2초 후 Async 출력
  - Hello가 리턴되며 done()이 호출됨
  - get()호출로 Hello가 출력

```java
public class FutureEx {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        ExecutorService es = Executors.newCachedThreadPool();
        FutureTask<String> f = new FutureTask<>(()->{
            Thread.sleep(2000);
            log.info("Async");
            return "Hello";
        }) { //비동기 작업이 모두 완료되면 호출되는 hook같은 것.
            @Override
            protected void done() {
                try {
                    System.out.println(get());
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } catch (ExecutionException e) {
                    e.printStackTrace();
                }
            }
        };
        es.execute(f);
        es.shutdown(); //이 메서드를 쓰더라도 하던 작업이 중단되지는 않음
    }
}

```

- Callback

  - Callback을 이용하여 비동기 실행 결과를 처리할 수 있는 코드
  - try/catch 작성이 빈번한 Future보다 더 우아한 코드라고 할 수 있다.
  - 더 나은 방법이 있지만, 기본기 중에서는 콜백 기법이 더 나음

```java

public class FutureEx {
    interface SuccessCallback {
        void onSuccess(String result);
    }
    interface  ExceptionalCallback{
        void onError(Throwable t);
    }
    public static class CallbackFutureTask extends FutureTask<String> {
        SuccessCallback sc;
        ExceptionalCallback ec;
        public CallbackFutureTask(Callable<String> callable, SuccessCallback sc, ExceptionalCallback ec) {
            super(callable);
            this.sc = Objects.requireNonNull(sc); //Tip. Null이 들어오면 안될 때 사용하는 메서드
            this.ec = Objects.requireNonNull(ec);
        }

        @Override
        protected void done() {
            try {
                sc.onSuccess(get());
            } catch (InterruptedException e) {
               Thread.currentThread().interrupt();
            } catch (ExecutionException e) {
                ec.onError(e.getCause());
            }
        }
    }

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        ExecutorService es = Executors.newCachedThreadPool();

        CallbackFutureTask f = new CallbackFutureTask(() -> {
            Thread.sleep(2000);
            if(1==1) throw new RuntimeException("Async ERROR!!!");
            log.info("Async");
            return "Hello";
        },
            s -> System.out.println(s),
            e-> System.out.println("Error: "+e.getMessage()));

        es.execute(f);
        es.shutdown(); //이 메서드를 쓰더라도 하던 작업이 중단되지는 않음
    }
}
```

> ### Q) 동기, 비동기의 장단점 알려주세요.

- 동기방식은 설계가 매우 간단하고 직관적이지만 결과가 주어질 때까지 아무것도 못하고 대기해야 하는 단점이 있고, 비동기방식은 동기보다 복잡하지만 결과가 주어지는데 시간이 걸리더라도 그 시간 동안 다른 작업을 할 수 있으므로 자원을 효율적으로 사용할 수 있는 장점이 있다.

> ### Q) node.js, spring을 동기,비동기, 블로킹, 논블로킹 관점에서 설명해주세요.

- #### Spring vs Node.js

  - Spring: Multi-Thread, 동기방식, blocking

  - 노드 등장 이전 스프링은 멀티 쓰레드를 사용하여 다중요청을 동시에 처리하였음
  - 한개의 쓰레드가 하나의 요청을 담당하여 응답까지 책임지고 반환하고 요청이 들어오면 바로 \* 결과를 반환해주는 동기 방식을 사용하고 연산이 완료되는 동안 기다리는 블록킹 방식
  - 문제점 : 쓰레드가 응답을 기다리면서 블록킹하는 시간이 많아지면 효율적이지 않음

- Node: single-Thread, 비동기 방식, non-blocking

  - 싱글 쓰레드를 사용하여 한개의 쓰레드에서 모든 요청을 처리하는 방식
  - 기존의 스프링과 달리 요청이 들어오면 바로 결과를 주는 것이 아니라 작업이 완료되는 대로 결과를 넘겨주는 비동기 방식
  - 한개의 쓰레드는 작업이 진행되는 동안 멈춰있는 것이 아니라 다른 작업을 수행할 수 있는 non-blocking
  - 문제점 : 갑자기 요청이 많아지고 복잡해지면 서버 반응이 느려진다.

- #### Spring의 보완 (5 이후)

- #### Spiring WebFlux

      - 스프링의 쓰레드 단점을 보완하고자 스프링 웹플럭스가 spring5부터 도입됨

  노드의 장점을 가져와서 업그레이드함
  기존의 멀티 쓰레드 방식을 유지하면서, 각각의 요청에 하나의 쓰레드가 대응되는 것이 아니라 싱글 쓰레드처럼 다수의 요청을 처리하게하게 되는 구조이다.

- 스프링을 사용하면 좋은 경우

  - 복잡한 요구 사항이 많은 경우 스프링을 사용하는 것이 유리하다. ex) 실시간 게임, 영상처리
    node를 사용하면 좋은 경우
  - 간단한 요구사항이 많은 경우 노드를 사용하는 것이 유리하다. ex) 채팅, crud기반 서비스

> ### Q) I/O작업이 잦은 경우 어떤 방식이 좋을까요?

- 비동기 I/O의 장점은 I/O 작업이 완료되는 동안 호출자가 다른 작업을 수행하거나 더 많은 요청을 발급할 시간이 있기때문에 비동기 I/O가 더 효율적으로 처리할 수 있습니다.

> ### Q) P2P 서비스 다운로드 받는 경우 4가지 경우를 어떻게 조합해서 사용할 수 있을지 상상해서 알려주세요.

- 사용자는 주로 다운로드 받는 경우로 생각했을 때, 여러 파일을 효율적으로 다운받는 경우 비동기 + 논블로킹 방식으로 사용할 것 같습니다.

> ### Q) 동기 + 논블로킹, 비동기 + 블로킹 방식이 잘사용되지 않는 이유는 무엇인가요?

- #### 동기 + 논블로킹

    <img width="500" alt="syn_async" src="https://user-images.githubusercontent.com/43171179/228160677-3b9f9999-c66f-41f5-a6e3-d295aaad143a.png">
    A 함수는 B 함수를 호출한다. 이 때 A 함수는 B 함수에게 제어권을 주지 않고, 자신의 코드를 계속 실행한다(논블로킹).

  그런데 A 함수는 B 함수의 리턴값이 필요하기 때문에, 중간중간 B 함수에게 함수 실행을 완료했는지 물어본다(동기).

  즉, 논블로킹인 동시에 동기인 것이다.

- #### 비동기 + 블로킹

    <img width="500" alt="syn_async" src="https://user-images.githubusercontent.com/43171179/228160693-bdd19ee3-5f50-4860-b91f-5b6d3c22fd4f.png">
    비동기 논블로킹은 이해하기 쉽다. A 함수는 B 함수를 호출한다.

  이 때 제어권을 B 함수에 주지 않고, 자신이 계속 가지고 있는다(논블로킹). 따라서 B 함수를 호출한 이후에도 멈추지 않고 자신의 코드를 계속 실행한다.

  그리고 B 함수를 호출할 때 콜백함수를 함께 준다. B 함수는 자신의 작업이 끝나면 A 함수가 준 콜백 함수를 실행한다(비동기).

  Async-blocking의 경우 sync-blocking과 성능의 차이가 또이또이하기 때문에 사용하는 경우는 거의 없다.

> ### Q) Multiflexing I/O에 대해서 알려주세요.

- #### I/O Multiplexing (멀티플렉싱, 다중화)

  - Asynchronous Blocking I/O

  간단하게 말하면 '하나'를 '여러 개'처럼 동작하게 한다는 뜻이다. 이를 I/O 관점에서 해석하면 '한 process가 여러 파일(file)을 관리'하는 기법이라 볼 수 있다.
  우리는 파일이 process가 kernel에 진입할 수 있도록 다리 역할을 해주는 interface 라는걸 알고 있다.
  이 개념을 server-client 환경에 접목 시키면 하나의 server가 여러 socket 즉, 파일을 관리하여 여러 client를 수용할 수 있게 구성하는 것을 의미한다.

  프로세스에서 특정 파일에 접근할 때는 File Descriptor(이하 FD)라는 추상적인 값을 사용하게 된다. 이 FD들을 어떻게 감시하냐는게 I/O Multiplexing의 주요 맹점이라 할 수 있다.
  여기서 어떤 상태로 대기하냐에 따라 select, poll, epoll(linux), kqueue(bsd), iocp(windows) 등 다양한 기법들이 등장한다.
