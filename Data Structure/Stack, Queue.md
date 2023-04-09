# Stack, Queue
스택(Stack)은 top이라 불리는 한쪽 끝에서만 자료를 넣거나 뺄 수 있는 Data Structure입니다. 자료를 넣는 것을 push, 꺼내는 것을 pop이라 하며 가장 마지막에 넣은 자료가 먼저 나오는 Last-In-First-Out(LIFO) 구조입니다.
큐는(Queue)는 rear라 불리는 한 쪽 끝에서만 자료를 넣고 front라 불리는 반대쪽 한쪽 끝에서만 자료를 뺄 수 있는 Data Structure입니다. 자료를 넣는 것을 자료를 넣는 것을 enqueue, 꺼내는 것을 dequeue이라 하며 가장 먼저 넣은 자료가 먼저 나오는 First-In-First-Out(FIFO) 구조입니다.

### Q) 스택과 큐의 내부 구조를 배열로 구현하면 어떻게 구현할 수 있나요?
- stack : JAVA의 ArrayList로 구현을 할 시 push 는 add() 메소드를 통해, pop은 리스트의 맨 앞(인덱스 0)의 요소를 반환하고 제거해줍니다. 
- queue : JAVA의 ArrayList로 구현을 할 시 push 는 add() 메소드를 통해, pop은 리스트의 맨 뒤(인덱스 -1)의 요소를 반환하고 제거해줍니다.
![image](https://user-images.githubusercontent.com/76711238/230778624-da39aed3-e391-4ccd-8e35-b0fec3015bad.png)

  ### Q) 삽입, 삭제가 빈번할텐데, 배열은 정적인 크기를 가지고 있는데 위의 말씀하신 대로라면 배열의 크기가 동적으로 변한다는 문제가 있지 않나요?
  JAVA의 ArrayList는 배열과 리스트의 특성을 합친 자료구조입니다. 그렇기에 배열은 정적인 크기를 갖고 있으나, JAVA의 ArrayList는 동적으로 크기를 변하는 것이 가능하기에 괜찮습니다.

### Q) 큐의 사용 사례에 대해 설명해주세요.
- 버퍼(Buffer) : 먼저 요청이 들어온 요청부터 먼저 처리해줍니다. 
(+) 버퍼 사용 이유 
버퍼를 사용하지않으면 입력과 즉시 데이터가 전송되기때문에 전송타겟에 부하가 걸릴 수 있습니다.
입력된것을 한번에 묶어서 전달하기에 전송시간이 줄어들며, 성능이 향상합니다.
더 나아가, 사용자가 잘못 입력시 수정도 가능하다는 장점을 갖고 있습니다.
그러나 입력과 즉시 데이터 전송을 하지않기 때문에 반응시간이 느립니다.

### Q) 스택의 사용 사례에 대해 설명해주세요.
- call stack : 함수의 순서를 저장해두는 데 사용됩니다. 
- 웹 브라우저 뒤로가기 : 가장 나중에 열린 페이지부터 뒤로 가기를 실행합니다.
- 문서작업에서 Ctrl+Z : 가장 나중에 수정한 내역부터 되돌립니다.

### Q) 스택으로 큐를 구현하는 방법에 대해 설명해주세요.
💡 스택 한개는 InBox, 한 개는 OutBox 용도로 만듭니다.
1. inBox에 데이터를 push(삽입)합니다. ex) 4→ 3→ 2→ 1
![image](https://user-images.githubusercontent.com/76711238/230779672-472b90f2-1c42-4528-b282-459f49fdc2e4.png)
2. inBox에 있는 데이터를 pop(추출) 하여 outBox에 push(삽입)합니다. ex) 1→ 2→ 3→ 4
![image](https://user-images.githubusercontent.com/76711238/230779686-f5e1b205-60bf-4221-b2e8-d5a19ac94919.png)
![image](https://user-images.githubusercontent.com/76711238/230779691-e21859b5-e243-4218-b222-86b0ef9a486b.png)
3. outBox에 있는 데이터를 pop(추출) 합니다. - 4→ 3→ 2→ 1
![image](https://user-images.githubusercontent.com/76711238/230779703-6be2f97e-df2c-4539-b74d-6fc639d1612a.png)

### Q) 큐로 스택을 구현하는 방법에 대해 설명해주세요.
💡 큐 한 개는 메인 큐, 다른 큐는 임시 큐 용도로 둡니다.
1. 메인 큐에 값을 넣습니다.(put) ex) 1→ 2→ 3 → 4
![image](https://user-images.githubusercontent.com/76711238/230779529-c38d703f-7c57-40b0-be27-e8f3bd0ca381.png)
2. 메인 큐에 1개의 원소가 남을 때까지 get 한 값을 임시 큐에 put 합니다.
![image](https://user-images.githubusercontent.com/76711238/230779545-fb44dd74-e49c-47c1-a0b6-fb4359b571ae.png)
3. 마지막 남은 원소는 result 변수에 저장합니다.
![image](https://user-images.githubusercontent.com/76711238/230779569-9be41f2e-c13f-45a9-8dbc-760bf815ea83.png)
4. 임시 큐에 있는 원소들을 메인 큐로 모두 이동시킵니다. (get → put)
![image](https://user-images.githubusercontent.com/76711238/230779584-f67516c4-3bea-4feb-92e9-50d5df42b0e1.png)
5. result 값을 리턴합니다.

### Q) Stackoverflow 현상에 대해 설명해주세요.
- Stack overflow는 스택 포인터가 메모리 내 스택의 경계를 넘어갈 때 발생하는 에러입니다. 해당 변수의 크기가 Stack보다 크거나, 함수를 무한으로 호출하고 있을 때, 혹은 Stack을 넘어가 다른 곳에 위치하고 있는 경우에 주로 발생합니다. 
- (+) Stack은 높은 주소 (High Address)부터 낮은 주소 (Low address)로 메모리에 할당됩니다.
    ![image](https://user-images.githubusercontent.com/76711238/230779310-e1e1b9dd-05df-4a26-8782-0f650d3765c6.png)

   ### Q-1) 해결하는 방법은 무엇이 있나요?
   - JAVA VM 옵션에서 스택의 크기를 증가시켜주면 됩니다. 

### Q) Messaging queue에 대해 아는 데까지 말씀해주세요.
- 메시지 큐는 메시지를 임시로 저장하는 간단한 버퍼라고 생각하면 됩니다. 메시지를 전송 및 수신하기 위해 중간에 메시지 큐를 두는 것입니다.
- 메시지 전송 시 생산자(Producer)로 취급되는 컴포넌트가 메시지를 메시지 큐에 추가합니다. 해당 메시지는 소비자(Consumer)로 취급되는 또 다른 컴포넌트가 메시지를 검색하고 이를 사용해 어떤 작업을 수행할 때까지 메시지 큐에 저장됩니다.  
    ![image](https://user-images.githubusercontent.com/76711238/230777739-cd082bdc-ac8b-4477-bef3-aab5e2a0a59f.png)
- 사용하는 이유 : 메시지 큐는 소비자(Consumer)가 실제로 메시지를 어느 시점에 가져가서 처리하는 지는 보장하지 않습니다. 언젠가는 큐에 넣어둔 메시지가 소비되어 처리될 것이라고 믿습니다. 
이러한 비동기적 특성 때문에 메시지 큐는 실패하면 치명적인 핵심 작업보다는 **어플리케이션의 부가적인 기능**에 사용하는 것이 적합합니다.
- 메시지 큐의 이점
    - 비동기(Asynchronous)
    메시지 큐는 생산된 메시지의 저장, 전송에 대해 동기화 처리를 진행하지 않고, 큐에 넣어 두기 때문에 나중에 처리할 수 있습니다. 여기서, 기존 동기화 방식은 많은 메시지(데이터)가 전송될 경우 병목이 생길 수 있고, 뒤에 들어오는 요청에 대한 응답이 지연됩니다.
    - 낮은 결합도(Decoupling)
    생산자 서비스와 소비자 서비스가 독립적으로 행동하게 됨으로써 서비스 간 결합도가 낮아집니다.
    - 확장성(Scalable)
    생산자 서비스 혹은 소비자 서비스를 원하는 대로 확장할 수 있기 때문에 확장성이 좋습니다.
    - 탄력성(Resilience)
    소비자 서비스가 다운되더라도 어플리케이션이 중단되는 것은 아닙니다. 메시지는 메시지 큐에 남아 있습니다. 소비자 서비스가 다시 시작될 때마다 추가 설정이나 작업을 수행하지 않고도 메시지 처리를 시작할 수 있습니다.
    - 보장성(Guarantees)
    메시지 큐는 큐에 보관되는 모든 메시지가 결국 소비자 서비스에게 전달된다는 일반적인 보장을 제공합니다.
    
### Q) 우선순위 큐는 어떤 자료구조로 구현돼있나요?
heap을 통해서 구현합니다.
   ### Q-1) 왜 heap을 사용하나요?
   heap은 최대, 최소값을 반환하는데 특화된 (시간복잡도 O(1)) 자료구조입니다. 우선순위가 높은/낮은 데이터 추출에 가장 빠르게 반환할 수 있는 자료구조이기 때문입니다.

   ### Q-2) heap을 toString()으로 출력한다면 순서대로 나올까요?
   아닙니다. heap은 tree로 구성된 자료구조이기에, 순서대로가 아닌 트리 노드에 담긴 순서대로 나올 것 입니다.
   
   ### Q-3) 우선순위 큐의 사용사례는 무엇이 있나요? 
   우선순위가 가장 높은 것을 추출할 때 사용됩니다. 
    1. 다익스트라 알고리즘(Dijkstra’s algorithm) : 최소 값을 찾을 때 우선순위 큐가 사용됩니다. 
    2. 힙정렬: 많은 힙 정렬에서는 우선순위 큐를 사용합니다. 
    3. 허프만 코딩: 문자열을 트리를 이용해 2진수로 압축하는 알고리즘이고 min-Priority를 사용합니다. 

### Q) 양방향 큐는 무엇인가요?
- 덱(Deque)는 양방향에서 요소를 추가하고 제거할 수 있는 양방향 큐입니다. 
큐는 맨 뒤 요소 (rear) 에 값을 추가하고, 맨 앞 요소 (front) 의 값을 삭제하는 방식이지만 덱(Deque)는 맨 앞에 추가할수고, 맨 뒤를 삭제할 수도 있습니다.
- 스택처럼 사용할 수도 있고 큐 처럼 사용할 수도 있는 자료구조입니다.
- 단방향 큐를 일반적인 리스트(list) 로 구현할 때 요소를 추가하고 제거할 때의 복잡도는 O(n) 인 반면, 양방향에서 값을 추가하고 제거하는 처리의 복잡도는 O(1)로 구현할 수 있습니다.
![image](https://user-images.githubusercontent.com/76711238/230778945-11fba7c9-b633-4cad-b10e-27e234e65729.png)

#### 사진 & 내용 출처
https://tecoble.techcourse.co.kr/post/2021-09-19-message-queue/
https://pro-programmer.tistory.com/4
https://cocoon1787.tistory.com/691
https://80000coding.oopy.io/bab54a8f-01de-4dcc-9630-2e8eaae9ed67
https://underdog11.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Priority-Queues-%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84-%ED%81%90
https://ryu-e.tistory.com/96
