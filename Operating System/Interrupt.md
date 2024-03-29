### 인터럽트는 언제 발생돼서 어떻게 처리하나요?
- 인터럽트는 **컴퓨터 파워에 이상이 있거나 하드웨어 디바이스로인한 인터럽트,프로세스 오류등**으로 발생합니다.
인터럽트 요청이 들어오면 일시중단하고 현재 프로그램상태를 보존하고 인터럽트를 요청한 장치와 원인을 파악하고 작업을 수행합니다. 그후, 인터럽트 발생시 저장해둔 PC를 다시 복구해서 재개합니다.
작업을끝내고나면 OS에 정의되어있는 인터럽트 핸들러를 실행합니다. 인터럽트 핸들러로 I/O를 대기중인 프로세스를 꺠우거나 깨어난 프로세스가 작업을 계속할수있도록 할수 있습니다.

    #### Q) 시스템콜이 들어오면 운영체제에서 어떤 과정을 통해 실행되나요?
    - 유저모드에서 수행되던 작업중 write()라는 시스템콜이 발생하면 현재 어떤모드인지 구분하는 모드비트를 1에서 0으로변경하고 커널모드에서 write()를 실행하고 실행이완료되면 모드비트를 다시 1로 변경하고 유저모드로 돌아갑니다.

    #### Q) 인터럽트와 시스템콜 각각이 발생할수있는 상황 예시를 들어주세요
    - 시스템콜 : 인텔리제이 같은 개발도구에서 콘솔에 hello를 출력하고자 할때 모니터에 hello를 출력하기위해 write() 시스템콜을  호출하게 되어 발생할수있습니다.
    - 인터럽트 : 컴퓨터 파워에이상이있거나 존재하지않는 메모리주소에 접근한다던지, 0으로 나누는연산을 실행하는경우 발생할수있습니다.

        > #### Q) 사용하는 프로그래밍언어에서 시스템콜을 어떻게 사용하는지 알고계신게 있나요?
        - JAVA에서 파일을읽는 read를 사용하는경우 운영체제의 기능이 구현된 C나 C++로 만들어진 함수가 실행됩니다. 이때 시스템콜이 발생하고 커널모드로 진입하게되고 
        디스크 컨트롤러를 거쳐 커널버퍼, JVM버퍼를 복사하는등의 과정을거쳐 운영체제의 기능이 실행됩니다. JVM -> JNI -> 시스템콜 -> 커널 -> 디스크컨트롤러 -> 버퍼복사 ...

        > #### Q) JNI가 무엇인지 설명해주세요
        - JVM이 특정 OS환경에 종속되지않은 상태로 운영체제의 기능을 담고있는데 일부 운영체제의 기능을 담지는 못했기때문에 자바언어로 해결이 안되는경우 **운영체제의 Native기능을 C나 C++로 만들어논 함수를 자바 메서드와 연결해주는 역할**을합니다.

        #### Q) 하드웨어/ 소프트웨어 인터럽트에대해 설명해주세요
        - 소프트웨어 인터럽트는 CPU내부에서 사용자가 실행할때 명령관련 모듈이 변화하는경우 발생합니다. 0으로 나누는 연산을 한다던지, 예외가발생한다던지,  존재하지않는 메모리 주소에 접근할때 발생합니다.
        
        - 하드웨어 인터럽트는 CPU외부에서 요구되고 , 운영체제의 처리가 필요한 상황을 전기적인신호를 사용해 알리기위해 발생합니다. 컴퓨터 파워에 이상이 있거나 하드웨어 디바이스로인한 인터럽트 등으로 발생합니다.

    > #### Q) 인터럽트 벡터/핸들러에대해 설명해주세요
    - 인터럽트 벡터 : 인터럽트를 요구한 I/O장치의 식별번호 , 해당 장치를위한 인터럽트처리 루틴의 시작주소를 찾는데 사용된다.
    - 인터럽트 핸들러 : 실제 인터럽트를 처리하기위한 루틴으로 인터럽트 서비스 루틴이라고도 한다(ISR) , 인터럽트별로 처리해야할 내용들이 프로그램되어있다.
 
    > #### Q) 소프트웨어 인터럽트를 처리하는 3가지 방법
    - Trap : 의도적으로 발생하는 상황, 대표적으로 시스템 콜 사용할때 발생하는 경우가 있다.   트랩 발생후 제어를 다음 명령으로 넘긴다.
    - Fault : **핸들러가 정정할수있을 가능성이 있는 일**로 발생한다. 대표적인예로 페이지가 없는 경우 발생하는 page fault. fault 발생후 오류 핸들러로 제어를 넘긴다.
    => 핸들러가 에러를 정정할수있으면 제어를 오류를 발생시킨 명령으로 돌려서 재실행한다.
    - 중단 : 하드웨어 오류와같이 **복구불가능한 치명적인 에러에서 발생**한다. 대표적인예로 0으로 나누는 경우가 있다. 응용프로그램으로 제어를 리턴하지않고 종료하는 중단루틴으로 반환한다.
    
    > #### Q) 인터럽트를 처리하는도중 또다른 인터럽트가 발생한다면 어떻게 처리되는지 설명해주세요
    인터럽트를 처리하는도중 또다른 인터럽트가 발생할수있는데 이때 두가지 처리방법이있습니다. 
    - 첫번째 **인터럽트 핸들러를 실행하고있는도중엔 다른 인터럽트를 수행하지않도록 하는 방법** . 이경우엔  새로 발생한 인터럽트는 대기상태로있다가 CPU 가 다시 인터럽트 가능한상태로 바뀐후에 인식됩니다
    - 두번째방법은 **인터럽트들간에 우선순위를 정하고 우선순위가 낮은 인터럽트를 처리하는동안 우선순위가 높은 인터럽트가 들어오면 새로운 인터럽트를 처리하는 방법**이있습니다.

      원칙적으로는 여러 인터럽트가 발생했을때 데이터 일관성을 유지하기위해 첫번째방법을 사용하지만 두번째방법을 사용하는경우도 있습니다.

   
    #### Q) 유저모드와 커널모드에대해 아는대로 설명해주세요 
    유저모드와 커널모드로 나눈이유는 유저프로그램과 커널을 분리시키기 위해서 입니다. 분리시키는 이유는 첫번째로 **유저프로그램은 파일을 읽는다거나 프로세스가 생성되는 내부동작을 신경쓸 필요없기때문**입니다.두번째로는 **보안이 강화**됩니다. 신뢰할수없는 유저가 운영체제의 서비스를 쉽게 조작하는걸 방지할수있습니다.
    - 유저모드 : 사용자 애플리케이션 코드가 실행되고, 하드웨어를 직접 접근할수없습니다. 시스템 서비스를 호출하면 유저모드에서 커널모드로 전환됩니다. 
    - 커널모드 : 모든 CPU명령을 실행할수있고 , 운영체제의 서비스나 디바이스 드라이버같은 커널모드코드를 실행합니다.
        
       > #### Q) 유저모드에서 시스템콜 이외의 경우에 커널모드로 변환되는 사례
        - 인터럽트 : 현재 작업실행을 중지하고 커널모드로 전환해서 인터럽트 서비스루틴으로 제어가 넘어가는 경우
        - DMA : DMA를 사용하면 하드웨어 장치가 CPU를 사용하지 않고 시스템 메모리에 직접 액세스할 수 있습니다. DMA 전송이 시작되면 CPU는 커널모드로 전환하여 전송을 수행하게 됩니다.

    #### Q) 폴링이 뭔지 설명해주세요
    - 운영체제가 하드웨어 장치의 상태레지스터를 읽음으로써 명령의 수신여부를 주기적으로 확인하는것.레지스터에 데이터를 전달하고 명령레지스터에는 명령을 기록하고 하드웨어 장치가 특정 동작을 처리했는지 폴링 반복문을 돌면서 기다리게된다(성공/실패코드를 받게된다). 하드웨어가 간단하지만 검사하는데 걸리는시간이 많이걸린다는 단점이있다.

       > #### Q) 폴링, 인터럽트중 어떤것이 더 신속하게 대응할수있는지?
        - 폴링은 특정 주기마다 응답을 확인하기때문에 **정확한 타이밍에 대응할수있다는 보장이 없으며**, 인터럽트는 인터럽트 장치에 신호가 들어오는 **즉시 발동**되기때문에 폴링보다 신속하게 대응할수있다.


    #### Q) DMA가 생기게 된 이유, 어떻게 동작하는지 설명해주세요
   - 기억장치와 I/O 장치간의 데이터이동에 반드시 CPU를 경유해야하기때문에 큰 데이터블록을 전송하는경우 인터럽트과정이 무수히 많아질수있어 CPU가 효율적으로 작동할수 없을수 있습니다. 예를들어 I/O를 write하는경우 CPU가 주 기억장치로부터 데이터를 한개씩 읽어 내부레지스터에 적재한다음 I/O장치로 보내고, I/O 명령도 보내야하는 일이 반복됩니다.이러한 문제를 해결하기위해 CPU의 개입없이 I/O장치와 기억장치 사이에 데이터 전송을 수행할수있는 DMA가 등장합니다.
   
   - **한마디로 인터럽트의 오버헤드를 줄이기위해 등장했습니다.**
   
   - 운영체제가 DMA엔진에 메모리상의 데이터위치와 전송할 데이터의 크기와 대상장치를 프로그램해서 CPU가 다른일을 진행할수있도록 합니다. 
CPU가 DMA컨트롤러에게 명령을 보내면 CPU로 버스요청을 보내고, CPU는 DMA 컨트롤러에게 버스승인 신호를 보냅니다. 그러면 DMA컨트롤러가 버스를 사용해 주기억장치로부터 데이터를 읽어서 디스크에 저장합니다. 저장할 데이터가 남아있지 않을때까지 이 과정을 반복합니다.

        
        > #### Q) 큰 데이터를 보낼떄만 DMA를 사용하나요? 작은데이터를 DMA로 보냈을떄 성능상 문제는없나요?
        - 해당 데이터에서 복사해야될 I/O 블록의 크기, DMA컨트롤러, 메모리 동기화 같은 기타 작업수행이 포함되는 비용 등을 고려해봐야합니다. 전송되는 데이터 양에비해 DMA전송 설정의 오버헤드가 더 크다면 CPU를 사용해 데이터를 직접 복사하는것이 더 효율적일수있습니다.

    #### Q) 서로다른 시스템콜을 어떻게 구분할수있나요?
    - **커널에서 내부적으로 시스템콜별로 고유번호를 할당**하고 read() 시스템콜이 호출되면 read()의 고유번호에 해당하는 제어루틴을 커널내부에 정의해두었고 커널이 그 번호를 확인후 호출합니다.



#### 사진,내용에 대한 출처
- https://www.tutorialspoint.com/operating_system/os_io_hardware.htm DMA, 폴링/ 인터럽트
