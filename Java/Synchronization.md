# Synchronization
- **동기화** 란, 프로세스(스레드)가 수행되는 시점을 조절하여 서로가 알고 있는 정보가 일치하는 것인데, 쉽게 말해 프로세스 간 데이터가 일치하도록 하는 것을 의미합니다.

- 동기화 메커니즘인 **상호배제**는 프로세스들이 필요로 하는 자원에 대해 배타적인 통제권을 요구하는 것입니다. 즉, 하나의 프로세스가 공유자원을 사용할 때 다른 프로세스가 동일한 공유자원에 접근할 수 없도록 통제하는 것을 뜻합니다.

- Monitor은 임계 구역을 지켜내기 위한 방법인 상호 배제를 프로그램으로 구현한 것입니다. 순차적으로 사용할 수 있는 공유 자원 혹은 공유 자원 그룹을 할당하는 데 사용됩니다. 모니터는 이진 세마포어만 가능합니다. 모니터를 통해 프로세스가 자원에 접근하는 방식을 이미지로 보면 아래와 같습니다.
![image](https://user-images.githubusercontent.com/76711238/236782612-46cbe66b-a17c-4b70-8af8-13f16dd01f50.png)
   - 공유 자원에 점유 중인 프로세스(스레드)는 Lock 을 가지고 있습니다. 
   - 공유 자원을 점유 중인 프로세스(스레드)가 있는 상황에서 다른 프로세스(스레드)가 공유 자원에 접근하려고 하면 외부 모니터 준비 큐에서 진입을 wait 합니다. 
   - Monitor 는 Semaphore 처럼 signal 연산을 보내는 것이 아니라 조건 변수를 사용하여 특정 조건에 대해 대기 큐에 signal 을 보내 작업을 시작시킵니다.

- Java 에서는 이러한 `Monitor` 을 통해 객체에 Lock 을 걸어 상호배제를 할 수 있습니다. 이러한 monitor를 가질 수 있는 것은 `synchronized` 키워드 내에서 가능합니다.
- Monitor는 여러 스레드가 객체로 동시에 객체로 접근하는 것을 막습니다. 여기서 모든 객체라는 사실이 중요한 이유는 heap 영역에 있는 객체는 모든 스레드에서 공유 가능하기 때문입니다.
- 스레드가 monitor를 가지면, monitor를 가지는 객체에 lock을 걸 수 있습니다. 그렇게 되면 다른 thread들이 해당 객체에 접근할 수가 없습니다.
- 즉 흔히 스레드가 공유객체의 lock을 얻는다는 것이 monitor (혹은 monitor lock)을 얻는 것을 말합니다
- Monitor에 접근한 스레드는 Entry Set에 대기합니다. Monitor에 접근 가능한 스레드는 단 한 개뿐이기 때문입니다. 
![image](https://user-images.githubusercontent.com/76711238/236784824-7009f0b2-ad24-496c-b2d1-96161a28c6bb.png)

<details>
<summary> ※ intrinsic lock (고유 락) </summary>

- 자바의 모든 객체는 lock 을 가지고 있습니다. 
- 이를 고유 락 (intrinsic lock) 또는 모니터 락 (monitor lock) 이라고 부릅니다.
- synchronized 는 고유 락을 사용하는데, synchronized 메서드가 호출되면 해당 스레드는 고유 락을 획득하고 메서드가 종료되면 락을 해제합니다.

</details>

### Q) Thread-local 에 대해서 설명해주세요.
- 오직 한 쓰레드에 의해서 읽고 쓰여질 수 있는 변수입니다. 두 쓰레드가 같은 코드를 실행하고 이 코드가 하나의ThreadLocal 변수를 참조 하더라도 서로의 ThreadLocal 변수를 볼 수 없습니다.
- 즉, ThreadLocal 변수를 선언하면 멀티쓰레드 환경에서 각 스레드마다 독립적인 변수를 가지고 접근 할 수 있습니다.
   - 활용 1) Thread-local 클래스를 활용하면 스레드 단위로 로컬 변수를 사용할 수 있기 때문에 마치 전역변수처럼 여러 메서드에서 활용할 수 있습니다. (한 쓰레드에서 실행되는 코드가 동일한 객체를 사용할 수 있도록 해주기 때문에 관련된 코드에서 파라미터를 사용하지 않고 객체를 각자가 가져다 쓸때 사용 됩니다.)
   - 활용 2) 클라이언트 요청에 대해서 각각의 스레드에서 처리할 때나, 스레드 독립적으로 처리해야 하는 데이터와 같이 인증 관련 처리에서도 활용될 수 있습니다.
   - 활용 3) 사용자 인증 정보 Spring Security 에서 사용자마다 다른 인증 정보/Session정보를 사용해야 할 때 사용됩니다.

   ### Q-1) 멀티쓰레드 환경에서 Thread-local 을 사용할 때 유의할 점에 대해 설명해주세요. 
   - 쓰레드 로컬은 **메모리 누수의 주범**이 됨으로 주의해서 사용해야 합니다.
   - 또한 스레드 로컬은 스레드 풀(thread pool)을 사용하는 환경에서는 주의해야 합니다. 스레드가 재활용될 수 있고 **재사용 되는 쓰레드가 올바르지 않은 데이터를 참조할 수도 있기 때문**에, 사용이 끝났다면 스레드 로컬을 비워주는 과정이 필수적입니다.
   - 이와 같이 스레드 풀을 통해서 스레드가 재사용되기 때문에 의도하지 않은 결과가 발생할 수 있습니다. 이러한 문제를 방지하려면 사용이 끝난 스레드 로컬 정보는 제거될 수 있도록 `remove` 메서드를 마지막에 명시적으로 호출하면 됩니다. 

### Q) synchronized 를 사용할 시 sychronized method, sychronized block, static sychronized method, static synchonized block 의 4가지 쓰임새 경우에 대해 설명해주세요. 

- 1. synchronized method 
   - 클래스 **인스턴스** 에 lock을 겁니다.
   - 동일한 인스턴스 내 synchronized 키워드가 적용된 메서드끼리 lock을 공유합니다.
   
- 2. static synchronized method
   - 인스턴스가 아닌 **클래스 단위** 로 lock을 겁니다.
   - 다른 인스턴스더라도 static 메서드에 synchronized가 붙은 경우 lock을 공유할 수 있습니다.  
   - static synchronized와 synchronized가 혼용되어있을 때 각자의 lock으로 관리

- 3. synchronized block
   - **인스턴스의 block 단위** 로 lock을 걸고 lock 객체를 지정해야 합니다.
   - this를 명시하면 synchronized method와 동일하게 동작하면서 synchronized method와 lock을 공유합니다.
   - 특정 객체를 명시하면 해당 객체에만 특정 lock을 걸면서 해당 객체에 lock을 거는 block끼리만 lock을 공유합니다.
   - .class 형식 명시하면 해당 클래스에만 특정 lock을 걸면서 해당 클래스에 lock을 거는 block끼리만 lock을 공유합니다.

- 4. static synchronized block
   - 인스턴스가 아닌 **클래스 단위** 로 lock을 겁니다.
   - block의 인자로 정적 인스턴스나 클래스만 사용
   - static 메서드 안에도 synchronized block을 사용할 수 있는데 이때는 this와 같이 현재 객체를 가르키는 표현은 사용할 수 없습니다.
   - static synchronized method 방식과의 차이는 lock 객체를 지정하고 block 범위를 한정 지을 수 있다는 점입니다. 

   ### Q-1) synchronized 사용 시 데드락이 발생하는 상황을 설명해주세요. 
   - **Deadlock** : 상호 배타적인 접근을 동시 수행하려 할 때 발생하는 현상입니다. 
   - **synchronized 사용 시 Deadlock 발생 경우** : Thread 1 번이 Transaction 수행 중 A 객체에 대한 monitor Lock 을 잡은 상태에서 B 객체에 대해 monitor Lock 을 잡기 위해 접근하는 상황에서 Thread 2 번이 B 객체에 대해 monitor Lock 을 획득 하 고 연산을 수행하는 도중에 A 객체의 monitor Lock 을 잡기 위해 대기 하는 상황이 발생합니다. 이렇게 서로가 서로의 Lock 을 먼저 해제하기만을 기다리고 있는 상황이 바로 Deadlock 현상입니다.

   - ![image](https://user-images.githubusercontent.com/76711238/236788130-67b9f113-2268-442f-bbf5-6b9f924fa231.png)
      - Thread 가 Deadlock 상황에 빠지게 되면 서로 다른 쪽의 monitor Lock 을 획득하기 위해 무한 대기합니다. 이러한 Transaction 이 빈번하게 수행 된다면 얼마 지나지 않아 가용 Thread 가 전부 소진되어 서비스 장애가 일어날 것입니다.

   - **해결방법** :  `Synchronized` 를 사용해야만 하는 환경에서 Deadlock 을 회피하기 위해서는 `Synchronized` 로 동기화 된 자원에 대해 어떤 Application 이든지 **항상 같은 순서로 참조하게 하면 되는 것**입니다. 위의 상황에서 B, C Method 를 수행하는 모든 Application 이 B Method 수행 후에 C Method 를 수행하도록 짜여져 있다면 Deadlock은 발생하지 않을 것입니다.

### Q) volatile 키워드에 대해 설명해주세요. 
- 동시성 프로그래밍에서 발생할 수 있는 문제 중 하나인 가시성 문제를 해결하기 위해 사용되는 키워드입니다. 가시성 문제는 여러 개의 스레드가 사용됨에 따라, CPU Cache Memory와 RAM의 데이터가 서로 일치하지 않아 생기는 문제를 의미합니다. volatile 키워드를 붙인 공유 자원은 RAM에 직접 읽고 쓰는 작업을 수행할 수 있도록 해줍니다.

- 동시성 프로그래밍에서 가시성 문제로 인한 공유 자원 접근 시 문제 상황이 발생할 수 있습니다. 가시성 문제란, 여러 개의 스레드가 사용됨에 따라, CPU Cache Memory와 RAM의 데이터가 서로 일치하지 않아 생기는 문제를 의미합니다.

<details>
<summary>  CPU와 RAM의 관계도 </summary>

![image](https://user-images.githubusercontent.com/76711238/236790675-af22c4e1-4897-4b81-8a44-301c13a4e4c4.png)

- CPU가 어떤 작업을 처리하기 위해 데이터가 필요할 때, CPU는 RAM의 일부분을 고속의 저장 장치인 CPU Cache Memory로 읽어들입니다.
- 이 읽어들인 데이터로 명령을 수행하고, RAM에 저장하기 위해서는 데이터를 CPU Cache Memory에 쓴 다음 RAM에 쓰기 작업을 수행합니다.
- 그러나 CPU가 캐시에 쓰기 작업을 수행했다고 해서 바로 RAM으로 쓰기 작업을 수행하지 않습니다.
- 반대로 읽기 작업도 해당 데이터가 RAM에서 변경이 되었다고 해도, 언제 CPU Cache Memory가 아닌 RAM에서 데이터를 읽어 들여서 CPU Cache Memory를 업데이트할 지 보장하지 않습니다.
- 동시성 프로그래밍에서는 CPU와 RAM의 중간에 위치하는 CPU Cache Memory와 병렬성이라는 특징때문에 다수의 스레드가 공유 자원에 접근할 때 두 가지 문제가 발생할 수 있습니다.

</details>

- 이를 해결하기 위해서는 가시성이 보장되어야 하는 변수를 CPU Cache Memory가 아니라 RAM에서 바로 읽도록 보장해야 합니다. 이때 변수에 valatile 키워드를 붙임으로써 변수를 CPU Cache Memory가 아니라 RAM에서 바로 읽도록 보장이 가능하며, 결국 가시성을 보장할 수 있습니다. 

- **다만 가시성이 보장된다고 동시성이 보장되는 것은 아닙니다.**
   - volatile 키워드는 어디까지나 volatile 변수를 메인 메모리로부터 읽을 수 있게 해 주는 것이 전부이고, 다른 스레드에 의해 이 값이 언제든 바뀔 수 있다. 즉, 가시성이란 공유 데이터를 읽는 경우의 동시성만 보장하는 것이라 생각하면 됩니다.

   ### Q-1) lock을 사용했을 시와 volatile을 사용할 시에, volatile 단점에 대해서 설명해주세요.
   <details>
   <summary> 가시성 문제과 원자성 문제</summary>

   ### 가시성 문제 
      - CPU - Cache - Memory 관계 상의 개념
      - 여러 개의 스레드가 사용됨에 따라, CPU Cache Memory와 RAM의 데이터가 서로 일치하지 않아 생기는 문제를 의미합니다.
      - 
   ### 원자성 문제
      - 한 줄의 프로그램 문장이 컴파일러에 의해 기계어로 변경되면서, 이를 기계가 순차적으로 처리하기 위한 여러 개의 Machine Instruction이 만들어져 실행되기 때문에 일어나는 현상
      - 예를 들어 프로그램 언어적으로 i++ 문장은 다음과 같은 기계가 수행하는 명령어로 쪼개집니다.
         - i를 메모리로부터 읽는다.
         - 읽은 값에 1을 더한다.
         - 연산한 값을 메모리에 저장한다.
      - 멀티 스레드 환경에서는 한 스레드가 각 기계 명령어를 수행하는 동안에 다른 스레드가 개입하여 공유 변수에 접근하여 같은 기계 명령어를 수행할 수 있으므로 값이 꼬이게 됩니다. (race condition)
      - 원자성 문제를 해결하기 위해서는 synchronized 또는 atomic을 사용해야 합니다.
      - 참고로 원자성 문제를 synchronized 또는 atomic을 통해 해결한다면 가시성의 문제도 해결됩니다. 
         - 1) synchronized 블럭을 들어가기 전에 CPU Cache Memory와 Main Memory를 동기화 해줍니다.
         - 2) atomic의 경우에는 CAS 알고리즘에 의해 원자성 문제와 CPU Cache Memory에 잘못된 값을 참조하는 문제를 동시에 해결해주기 때문입니다.
         
   </details>

   - `volatile` 사용 : 가시성 문제만 보장합니다.
      - 원자성 문제를 보장하지 못합니다. 
   - `lock` 사용 : 원자성 문제(단일 연산) + 가시성 문제 모두를 보장합니다.

### Q) synchronized 선언 시 이는 암묵적으로 수행하는데 세밀하게 control 할 수 있는 명시적인 lock 의 방법으로 뭐가 있을까요?

- JAVA에서 Monitor 방식의 구현은 두 가지로 나뉩니다.

- 1. **Implicit(암묵적) Lock (synchronized 키워드)**
   - Lock 클래스를 사용하여 직접 lock, unlock 을 구현하는 것이 아니라 내부적으로 객체의 고유 락을 사용하여 접근을 제어하기 때문에 암묵적이라고 분류됩니다.

- 2. **Explicit(명시적) Lock (java.util.concurrent.locks)**
   - 직접 Lock 객체를 명시적으로 생성하여 제어할 수 있습니다. 
   - `java.util.concurrent.lock` 패키지 : 
      - concurrent.locks 패키지는 내부적으로 synchronized를 사용하여 구현되어 있지만 더욱 유연하고 세밀하게 처리하기 위해 사용됩니다. 
      - 고유 락 외에 직접 동기화를 구현할 수 있는 lock 구현체를 제공합니다. 이들은 보다 다양한 기능을 제공하고 있으며, 이를 통해서 코드에서 lock 획득과 해제를 구현할 수 있습니다.
      - `ReentrantLock` : Lock의 구현체로 임계 영역의 시작과 종료 지점을 직접 명시할 수 있습니다. (가장 일반적인 lock / 특정 조건에서 lock 을 반납하고 이후에 다시 재진입 시도 가능 /  lock 을 걸고 싶은 위치에서 ReentrantLock 객체의 lock() 메서드를 호출하고, 해제하고 싶은 위치에서 unlock() 을 호출하여 lock 을 제어 가능)

      - `ReentrantReadWriteLock` :  공유 자원에 여러 개의 스레드가 read 가능하고, write는 한 스레드만 가능한 인터페이스로 읽기를 위한 lock과 쓰기를 위한 lock을 별도로 제공합니다. ( 읽기 락과 쓰기 락을 함께 제공 )

   - `java.util.concurrent.atomic`의 **atomic** : 
      - 해당 타입으로 선언한 단일 변수에 대하여 atomic operations 를 지원하는 타입입니다. 
      - atomic 타입은 사용 시에 내부적으로 **CAS (Compare And Swap)** 알고리즘을 사용하여 값을 비교하는 방식으로 동기화를 적용합니다. 
      - 이 방식을 사용하여 따로 lock 을 사용하지 않고 동기화를 처리할 수 있습니다.
      <details>
      <summary> CAS (Compare And Swap) </summary> 

         - CAS 알고리즘은 변수의 값을 확인할 때, **현재 스레드의 데이터를 실제 메모리에 저장된 데이터와 비교하여 두 값이 일치하는 경우에만 해당 값을 사용**할 수 있도록 합니다. 
         - 현재 연산 중에서 스레드의 값과 메모리의 값이 다른 경우 중간에 다른 스레드를 통한 작업이 있었던 것으로 판단하여 write 를 중단하고 작업을 재시도하도록 한다.

      </details>

### Q) 자바에서 thread 를 생성하는 방법과 실행하는 방법을 설명해주세요.
- Java에서 Thread를 생성하는 방법은 두가지가 존재합니다.
   - 1. Thread 클래스를 상속 받아 run 메서드를 오버라이딩 하는것
   - 2. Runnable 인터페이스를 Implements 하여 run 메서드를 정의하는것

   ### Q-1) thread 실행 시 run()으로 수행할 때와 start()로 수행할 때와의 차이를 설명해주세요.
   ![image](https://user-images.githubusercontent.com/76711238/236792234-e1488ca8-1aa1-4792-abe1-17149a27ab37.png)
   - jvm은 ‘data, code, stack, heap’ 영역으로 구성되어 있습니다.
여기서 프로세스 내부의 thread들은 data, code, heap 영역을 공유하게 됩니다.
   - **start()** 메서드는 각 쓰레드마다 call-stack을 새로 만들어 작업을 합니다. 즉 새로 thread를 실행하는 것입니다. (개인의 thread를 만들고 개인의 call stack을 이용)
   -  **run()** 메서드는 메인쓰레드의 call-stack을 공유하여 작업을 합니다. 즉 기존에 있던 thread를 실행하는 것입니다. 

   ### Q-1) 일반 방식에서 main thread가 종료되면 어플리케이션이 종료될 텐데, 멀티스레드 방식에서 main thread는 언제 종료되나요?
   - 멀티쓰레드 환경에서 마지막 thread까지 모두 수행을 종료할 때 어플리케이션이 종료됩니다.



#### 사진 & 내용 출처

https://tecoble.techcourse.co.kr/post/2021-10-23-java-synchronize/

https://lordofkangs.tistory.com/28

https://bgpark.tistory.com/161

https://yeonbot.github.io/java/ThreadLocal/

https://madplay.github.io/post/java-threadlocal

https://jgrammer.tistory.com/entry/Java-%ED%98%BC%EB%8F%99%EB%90%98%EB%8A%94-synchronized-%EB%8F%99%EA%B8%B0%ED%99%94-%EC%A0%95%EB%A6%AC

https://a07274.tistory.com/268

https://steady-coding.tistory.com/554

https://yhmane.tistory.com/215
