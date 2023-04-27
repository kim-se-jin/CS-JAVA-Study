# GC
가비지 컬렉션은 가바 가상 머신내의 실행 엔진 영역에 존재합니다. 
**Heap 영역에서 동적으로 할당했던 메모리 중 필요 없게 된 메모리 객체**(garbage)를 모아 **주기적으로 제거**하는 프로세스입니다.
-  여기서 동적으로 할당했던 메모리 영역 : 프로그램 런타임에 사용되는 Heap 영역 메모리
-  필요 없게 된 영역 : 어떤 변수도 가리키지 않게 된 영역

### Q) GC의 작동원리에 대해 설명해주세요.
  - ### Q-1) 언제 GC가 작동될까요? ( = Garbage가 될 때 )
    - 참조되는 객체가 **더 이상 참조되지 않을 때** GC 처리를 합니다.

  - ### Q-2) GC의 내부 작동 원리
 ![image](https://user-images.githubusercontent.com/67494004/234883381-816208ba-528c-4cb7-b668-d3a075e5e416.png)
   - GC는 Young 영역과 Old 영역으로 나눠져 있습니다. 

#### Young 영역
- **새롭게 생성된 객체가 할당되는 영역**입니다. Young영역에 대한 GC를 **Minor GC**라고 부릅니다.
    - Eden, Survivor0, Survivor1 으로 나뉨
      - **Eden**
        - new를 통해 새로 생성된 객체가 위치
        - 정기적인 쓰레기 수집 후 살아남은 객체들은 Survivor 영역으로 보냄
      - **Survivor 0/1**
        - 최소 1번의 GC 이상 살아남은 객체가 존재하는 영역
        - Survivor 0 또는 Survivor 1 둘 중 하나에는 꼭 비어 있어야 함
          - 만약 두 Survivor 영역에 모두 데이터가 존재하거나, 모두 사용량이 0이라면 현재 시스템이 정상적인 상황이 아님
        
        - ### Q) 왜 Survivor 영역은 2개 인가요?
        ![image](https://user-images.githubusercontent.com/67494004/234882564-c23d4d0d-e27b-4997-801e-dbdf99cd6b0f.png)
          - 외부 단편화 문제를 해결하기 위해서 입니다. 메모리가 할당되고 헤제되기를 반복하다 보면 왼쪽 사진과 같이 총 메모리 공간은 남지만,
파편화되어있어 메모리를 할당할 수 없는 문제가 발생합니다. (외부 단편화) 

> 💡 **age !**
- minorGC 때 garbage되어 사라지지 않고, **Survivor영역에서 살아남은 횟수를 의미하는 값**입니다. **age 값이 임계값에 다다르면 Promotion(Old 영역으로 이동) 여부를 결정**합니다.
  - Object Header에 기록됨 
  - JVM 중 가장 일반적인 HotSpot JVM age의 기본 임계값 : 31
    - 객체 헤더에 age를 기록하는 부분이 6 bit로 되어 있기 때문


#### Old 영역
  - Young영역에서 Reachable 상태를 유지하여 **살아남은 객체가 복사되는 영역**입니다.
  - Young 영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지는 적게 발생합니다.
  - old 영역에 대한 가비지 컬렉션(Garbage Collection)을 **Major GC** 또는 Full GC라고 부릅니다.
  - **Young에서 처리할 수 없을 정도로 큰 경우, 바로 Old Generation**

#### Meta Space 영역
![java7 8](https://user-images.githubusercontent.com/67494004/234877495-d4a322b5-dc94-4b78-b55d-da2806715cf7.JPEG)
- **자바 8 이전** : **Permanation 영역** - Heap 영역에 위치
- **자바 8 이후** : **MetaSpace 영역** - Native Memory 영역에 위치
  
- 저장하는 데이터 : 자바의 메타 데이터
    - Class Meta Data
    - Method Meta Data
    - Static Object Variable

💡 **PermGen 제거된 이유 ? ( = 단점 )**
- PermGen 영역이 **고정 크기**로 할당되어 있기 때문에, 할당 가능한 메모리 크기가 제한적입니다.
- 클래스 메타데이터가 많아지면, PermGen 영역의 **메모리 부족으로 인해 OutOfMemory(OOM) Error 가 발생**할 수 있습니다.
- PermGen 영역의 GC는 **Full GC** 를 수행하기 때문에, GC 가 길어집니다.

💡 이를 보완한 MetaSpace
- Metaspace 영역은 JVM에 의해 관리되는 Heap이 아닌 OS 레벨에서 관리되는 Native Memory 영역
  - 운영체제가 메모리를 동적할당하는 방식으로 변경
- 그러므로 Metaspace가 Native 메모리를 이용함으로서 개발자는 영역 확보의 상한을 크게 의식할 필요가 없어지게 됨!
- 메모리의 동적할당으로 이루어지기 때문에 메모리 단편화를 방지하기 위하여 블록 할당방식으로 변경되었으며 메타데이터의 정보는 힙과 네이티브 메모리 두 영역에 모두 할당


### Q) Young/Old 영역을 나누는 이유?
  - Heap 영역은 처음 설계될 때 다음의 2가지 전재로 설계되었습니다.
    - 대부분의 객체는 금방 접근 불가능한 상태가 된다. 
    - 오래된 객체에서 새로운 객체로의 참조는 아주 적개 존재한다.
  - 즉, **객체는 대부분 일회성이며, 메모리에 오래 남아있는 경우가 드물기 때문에** 생존 기간에 따라 **객체를 효율적으로 관리**하기 위해 나눕니다.

### Q) Minor GC와 MajorGC 의 차이점에 대해 말씀해주세요.
- 소요 시간 입니다. Young 영역은 크기가 작기때문에 Minor GC 적은 시간, Old 영역은 크기가 크기 때문에 MajorGC는 오래 걸립니다.
  
    ### Q-1) Stop the World 에 대해 설명해주세요.
    - Stop the world는 GC를 수행하기 위해 어플리케이션 자체를 멈추는 현상을 말합니다. GC는 자신을 제외한 모든 스레드를 모두 멈추기 때문에 차질이 생길수도 있습니다.

    ### Q-2) 왜 다른 스레드들은 모두 종료해야 할까요?
    - Heap의 상태가 변경될 수 있기 때문에 중단하고, 값을 변경해야 합니다.
  
### Q) Old 영역의 객체는 Young 영역의 객체를 참조하는 경우가 있습니다. 이럴 경우, Eden 영역에서 GC가 실행되면, Old 영역이 참조하고 있는 객체는 지우면 안됩니다. List형식으로 순차적으로 확인해야하는데, 개선하기 위한 방법을 JVM이 보유한 방법에 대해 설명해주세요.
> Hint💡 Table
- Old영역에 512bytes 크기의 Card Table 이 있습니다.
  - Card Table
    - **old 영역에 있는 객체가 Young 영역을 참조할 때 마다 그에 대한 정보가 표시**됩니다.
    - **Minor GC**가 실행될 때, 모든 Old영역에 존재하는 객체를 검사하는 것은 비효율적임, Young 영역에서 GC가 진행될 때 **카드 테이블만 조회**하여 GC의 대상인 지 식별합니다.

### Q) 가장 인상깊었던 Garbage Collection 알고리즘에 대해 설명해주세요.
**CMS GC (Concurrent Mark Sweep)**
![gc_cms](https://user-images.githubusercontent.com/67494004/234877620-6b0603c5-5546-4271-a335-2776a4e1695e.png)
-  애플리케이션의 지연 시간을 최소화 하기 위해 고안되었으며, 애플리케이션이 구동중일 때 프로세서의 자원을 공유하여 이용 가능한 알고리즘
- Mark Sweep 알고리즘을 **Concurrent하게 수행**
- ❌ 단점 : 다른 GC 방식보다 메모리와 CPU를 더 많이 필요로 하며, Compaction 단계를 수행하지 않음.
  - 시스템이 장기적으로 운영되다가 조각난 메모리들이 많아 Compaction 단계가 수행되면 오히려 **Stop The World 시간이 길어지는 문제가 발생**

**G1(Garbage First) GC**


![image](https://user-images.githubusercontent.com/67494004/234877925-d83cefe4-f19f-40cf-b78d-1cd11c0ce2df.png)
- 장기적으로 많은 문제를 일으킬 수 있는 CMS GC를 대체하기 위해 개발
- **Region(지역)이라는 개념**을 새로 도입하여 **Heap을 균등하게 여러 개의 지역**으로 나누고, **각 지역을 역할과 함께 논리적으로 구분**하여(Eden 지역인지, Survivor 지역인지, Old 지역인지) 객체를 할당
  - Heap을 동일한 크기의 Region으로 나누고, 가비지가 많은 Region에 대해 우선적으로 GC를 수행
  

### Q) static을 잘못쓰면 Memory Leak 이 발생할 수 있는데, 자바 GC와 연관지어 설명해주세요.
- Memory Leak은 프로그램에서 동적으로 할당한 메모리 공간을 반환하지 않는 경우 발생할 수 있는 문제 입니다. 개발자가 객체를 생성하고 사용한 후, 메모리를 반환하지 않는 경우에 발생합니다.
  
  - (질문자 예시) 가변적인 자료구조 앞에 static을 붙이는 경우
    - static 으로 hashMap이 있다고 쳤을 때 할당 해제가 되지 않아 memory leak 발생
    - 참조가 안되어있으면 GC 가 발동이 되어야하는데, static을 사용함으로 인해 Memory에 계속 남아있게 됨.

- static을 사용하게 되면 compile과 동시에 method영역에 객체가 할당되게 됩니다. 사용되지 않는데 메모리에 계속 남아있다면 메모리 낭비이기 때문에 GC가 안쓰는 걸 확인하고 비워줌으로 메모리를 효율적으로 사용할 수 있습니다.

### Q) 자바8부터 static이 저장되는 영역이 바꼈는데, static은 어디에 저장될까요?

- MetaSpace영역 입니다.
  -  Method Area : 클래스 정보와 메서드 코드를 저장
  -  Metaspace : 클래스 메타데이터를 저장

> [추가 참고]
> class meta-data가 metaspace로 이동하고 기존에 perment 영역에 저장되던 static object는 heap영역에 저장되도록 변경되었다고 설명하는데 이는 reference는 여전히 metaspace에서 관리됨을 의미하기에 참조를 잃은 static object는 GC의 대상이 될 수 있으나 reference가 살아있다면 GC의 대상이 되지 않음을 의미한다.
>
> 
> 따라서, metaspace는 여전히 static object에 대한 reference를 보관하며 애매하게 heap에 걸쳐지지 않고 non-heap(native memory)로 이관되며 static 변수(primitive type, interned string)는 heap 영역으로 옮겨짐에 따라 GC의 대상이 될 수 있게끔 조치한 것이다.
  
  - ### Q-1) static은 결국 heap으로 옮겨졌으면, 결국 GC가 될 수 있는 거 아닌가요?
    - **null 선언 시** 사용하지 않는 객체로 GC가 가능해집니다.

### Q) JVM도 되게 다양한데, 그 중 Hotspot JVM 이 기존의 Mark-And-Sweep 을 개선하였는데 알고 계시면 설명해주세요.
> Hint💡 Bump the Pointer, TLABs
- **Bump the pointer** 란
  - **Eden영역에 마지막으로 할당된 객체의 주소를 캐싱**해두는 것 입니다. 
  - 새로운 객체를 위해 유효한 메모리를 탐색할 필요없이 마지막 주소의 다음 주소를 사용하게 함으로써 **속도를 높일** 수 있습니다. 
  - 이를 통해 새로운 객체를 할당할 때 객체의 크기가 Eden영역에 적합한지만 판별하면 되므로 빠르게 메모리를 할당할 수 있습니다.

멀티쓰레드 환경인 경우, Eden영역에 할당할 때 동기화가 필요합니다. **멀티쓰레드 환경에서 성능 문제를 해결하기 위해 TLABs 가 도입**되었습니다.

- **TLABs(Thread Local Allcation Buffers)** 란 
  - **각각의 스레드마다 Eden영역에 객체를 할당하기 위한 주소를 부여함**으로써 동기화 작업 없이 빠르게 메모리를 할당하는 기술입니다.
  - 각각의 쓰레드는 자신이 갖는 주소에만 객체를 할당함으로써 동기화없이 bump the pointer를 통해 빠르게 객체를 할당할 수 있습니다.

### Q) Traffic 이 몰릴 것으로 예상되는 이벤트가 예정되어 있습니다. 여기서 Young 과 Old 영역의 비율을 튜닝할 수 있는데, 어떤 비율로 튜닝해야 할까요? 
> Plus💡 기존 default값 **Young 1 : Old 3**

##### 1.먼저 **트래픽의 특성을 파악**해야 합니다.
- Young 영역은 적은 크기의 객체를 빠르게 처리하는 데 사용되며, Old 영역은 큰 크기의 객체를 처리하는 데 사용됩니다.

##### 2-1. **짧은 시간동안 대량의 작은 객체가 생성되는 경우**
- **Young 영역의 크기를 늘리고** Old 영역의 크기를 줄여서 Young GC가 더 자주 발생하도록 설정하는 것이 좋습니다. 작은 객체를 더 빠르게 처리하고 메모리를 효율적으로 사용할 수 있습니다.
  - Young 영역의 크기를 늘리면 Major GC 빈도가 줄어들기 때문에 가비지 수집기의 성능이 향상될 수 있습니다.
    -  == 마이너 GC가 더 자주 발생할 수 있음

##### 2-2. **대량의 큰 객체가 생성되는 경우**
- **Old 영역의 크기를 늘려** GC가 덜 발생하도록 설정하는 것이 좋습니다. 이렇게 함으로써 큰 객체를 더 효율적으로 처리하고 메모리를 효율적으로 사용할 수 있습니다.
  - Old 영역의 크기를 늘리면 Major GC의 빈도를 줄일 수 있지만, Major GC의 일시 중지 시간이 길어질 수 있음

##### 3.**결론**
- 따라서 예상되는 트래픽의 특성을 고려하여 Young 영역과 Old 영역의 비율을 조정하면, GC 성능을 최적화할 수 있습니다.
  - 응용 프로그램이 수명이 짧은 개체를 많이 생성하는 경우 Young 영역의 크기를 늘리는 것이 좋습니다. 
  - 응용 프로그램에 수명이 긴 개체가 많은 경우 Old 영역의 크기를 늘리는 것이 좋습니다.


---

_**스터디 진행 시 대답과 꼬리질문**_
(꼬리질문이 좋아서 넣어봤습니다 ㅎㅎ )

- 먼저 Young 영역의 비중을 늘릴 것 입니다. 트레픽이 몰린다는 것은 많은 유저가 들어온다는 뜻이므로, 금방 생성되었다 사라지는 객체가 많을 것 같기 때문에 3:1 로 하겠습니다.

  - ### Q-1) 그럼 Young 영역을 높인다는건데, 영역이 크기가 커지면 Stop-the-World 시간도 길어지고 수거해야할 객체가 많아지지 않을까요?
    - Young 영역과 Old영역을 늘렸을 때의 Trade-off 설명




### 참고
[내용 및 사진-1](https://inpa.tistory.com/entry/JAVA-☕-JVM-내부-구조-메모리-영역-심화편#가비지_컬렉터_garbage_collector_,gc)   
[내용 및 사진-2](https://flightsim.tistory.com/240)    
[MetaSpace 내용-1](https://goodgid.github.io/Java-8-JVM-Metaspace/)   
[MetaSpace 내용-2](https://velog.io/@agugu95/자바-런타임-환경과-메모리-Java-Heap-Permgen-and-MetaSpace)   
[GC 알고리즘](https://mangkyu.tistory.com/119)   
[G1 GC 알고리즘](https://steady-coding.tistory.com/590)   
[GC-static -1](https://8iggy.tistory.com/230)   
[GC-static -2](https://8iggy.tistory.com/229)
