# TCP, UDP
둘 다 데이터를 보내기 위해 사용하는 프로토콜 입니다.
TCP 는 연결형 서비스로, 속도는 느리지만 신뢰성이 높습니다.
UDP 는 비연결형 서비스, 속도는 빠르지만 신뢰성이 낮습니다.

  ### Q) HTTP에서 꼭 TCP를 연결해서 사용해야하는 이유?
  - 신뢰성을 보장하기 위해서 입니다.
  - HTTPS 를 사용하면 SSL/TLS 와 함께 사용할 수 있다는 이점이 있습니다.

  ### Q) TCP는 신뢰성을 보장하고 오류를 검출하는데, 어떤 방식으로 오류를 검출할까요?
  > 💡Hint) TCP 의 헤더에 담긴 정보 중 하나
  
  checkSum을 통해 오류를 검출합니다. 
  - 체크섬은 전송할 데이터를 16bits씩 나눠서 차례대로 더해가는 방법으로 생성합니다.
    -  두 개의 수를 더했을 때 자리 수가 하나 올라간 부분을 캐리(Carry)- 계산 결과에서 캐리 부분만 떼어내서 다시 계산 결과에 더함.(Warp Around)
    -  마지막 계산 결과에 1의 보수를 취하면 => 체크섬
   
  - 수신 측은 데이터를 받으면 위의 과정을 동일하게 거치되 1의 보수를 취하지 않은 값까지만 만든 다음, 이 값과 송신 측이 보낸 체크섬을 더해서 모든 비트가 1이라면 이 데이터가 정상이라고 판단합니다.
  
  - 0이 하나라도 있으면 송신 측이 보낸 데이터에 뭔가 변조가 있었음을 알 수 있음 !
  
  ### Q) TCP는 SYNC 와 ACK 를 통해 연결을 수립하고, 반환하는 방식에 대해 설명해주세요.
  **3-way-HandShaking (연결 과정)**   
  <img src = "https://user-images.githubusercontent.com/67494004/236833172-7f3590a0-ee1e-4377-a19f-8b24a2e65ee9.png" width="60%" height="50%">   
  1. 클라이언트가 서버에게 SYN 패킷을 보냄 (sequence : x)
  2.  서버가 SYN(x)을 받고, 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 보냄 (sequence : y, ACK : x + 1)
  3.  클라이언트는 서버의 응답은 ACK(x+1)와 SYN(y) 패킷을 받고, ACK(y+1)를 서버로 보냄

  **4-way-HandShaking (반환 과정)**   
  <img src = "https://user-images.githubusercontent.com/67494004/236833246-60d25f71-d54e-44d8-84a0-cd942fcfdd4e.png" width="60%" height="50%">   
  1. 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보냄
  2. 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보냄 (이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 된다)
  3. 데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보냄
  4. 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보냄 (아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다림)
  - 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
  - TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)
  
    ### Q-1) 4-way에서 TIME_WAIT 용어와 필요성에 대해 설명해주세요.
    - 전송 중에 지연되어 연결이 닫힌 후 도착하는 패킷이 있을 수 있으므로 TIME_WAIT 상태가 필요합니다. ACK 세그먼트를 수신한 후 소켓이 즉시 닫히면 이러한 지연된 패킷이 손실되어 데이터가 손실되거나 손상될 수 있습니다. 
  
  ### Q) 3-way-HandShaking 이전에 사용했던 2-way-HandShaking가 있습니다. 이제 사용하지 않는 이유는 뭘까요?
  - 마지막 단계가 빠져 2-way가 된다면 클라이언트가 ACK를 받았는 지 알 수 없습니다. 따라 2-way는 신뢰성을 보장할 수 없습니다. 

  ### Q) 지금까지 클라어인트와 서버로 설명하셨는데, 웹서버가 클라이언트가 될 수 있을까요?
  - 네 가능합니다.
    ### Q-1) 그럼 클라이언트와 서버의 관계를 설명해주세요.
    - 클라이언트 : 데이터를 요청하는 쪽
    - 서버 : 요청한 데이터를 반환하는 쪽
  
    ### Q-2) 각각의 클라이언트끼리 Syn 패킷을 보내면 어떻게 될까요?
    > ❌ 오답 : 패킷 충돌
    - TCP는 전이중 방식을 취하기 때문에, 각 클라이언트는 독립적으로 TCP연결을 유지합니다. SYN packet에 대한 파이프가 따로 생성됩니다.

    ### Q-3) SYN bit를 보낼 때 발생할 수 있는 취약점에 대해 설명해주세요. 
    - Backlog Queue는 서버가 클라이언트의 연결 요청을 대기할 때, 요청 정보를 저장하는 공간입니다. 만약 정상 연결 되었다면(ESTABLISHED) Backlog Queue 공간에서 연결 요청정보가 삭제되어 공간은 계속 유지됩니다. 하지만 연결 과정이 중간에 정상적으로 진행되지 않는다면 정보가 계속 Backlog Queue에 남아있게 됩니다.
    - 계속 연결요청 대기 Queue가 쌓이면 Backlog Queue 공간을 가득 채워 다른 연결 요청 정보 저장이 불가합니다.
    - SYN 패킷이 백로그 큐에 어느 정도 저장이 되겠지만 결국 가득 차게(flooding) 되어 더 이상의 연결을 받아들일 수 없는 상태, 즉 서비스 거부 상태로 들어가게 되는 것이다.
    - 이처럼 백로그 큐가 가득 찼을 경우에 공격을 당한 해당 포트로만 접속이 이루어지지 않을 뿐 다른 포트에는 영향을 주지 않고, 또한 서버나 네트워크에 별다른 부하도 유발하지 않기 때문에 관리자가 잘 모르게 되는 경우가 많다.

    - 누군가 악의적으로 서버에게 SYN패킷을 계속 보내게 될 때, 그 과정에서 서버가 다운되거나 느려지는 Sync flooding 현상이 발생합니다.

    ### Q-3-1) Sync flooding 해결 방안에 대해 설명해주세요.
    1. Backlog Queue의 크기를 늘린다.
    2. SYN Cookie를 설정한다.
    3. TCP 연결 과정 대기 시간을 줄인다.
    4. 방화벽의 동일 클라이언트 IP에 대해 연결 요성(SYN) 임계치를 설정한다.
    
  ### Q) 온라인 게임이나 DNS와 같은 프로그램은 어떤 통신 프로토콜을 사용하는 지 이유와 함께 설명해주세요.
  - 속도가 빨라야 하기 때문에 UDP 프로토콜을 사용합니다.
    
    ### Q-1) UDP를 사용했을 때, 패킷 손실 등의 단점은 DNS 를 사용하면 위험하지 않을까요?
    - DNS 관련 손실은 Application layer에서 처리해줍니다.

  ### Q) 4-way-handShaking에서 중간에 한 쪽에서 서버를 끊어야하는 경우 어떻게 해결하나요?
  - Reset패킷을 사용하여 연결을 강제로 종료합니다.
  
    ### Q-1) 마지막에 서버쪽에서 FIN을 보내고 클라이언트의 ACK를 서버쪽에서 받지 못하는 경우, 어떻게 판단하나요?
    - TIME WAIT에 걸어둔 시간이 다 지나면 , TIME OUT 으로 연결이 종료됩니다.
    
    ### Q-2) 어플리케이션을 사용하다보면 TIME_WAIT이 길게 잡혀있습니다. 그럼 성능이 저하될 것 같은데, 이를 개선하기 위해 도입된 방법을 아시나요?
    > 💡Hint! 명시적 혼잡 통보, TCP 헤더의 예약 비트에 추가된 비트로 확인
    - 새롭게 추가된 NS, CWR, ECE 플래그는 네트워크의 명시적 혼잡통보(Explicit Congestion Notification, ECN)을 위한 플래그입니다.
    - CWR, ECE, ECT, CE 플래그를 사용하여 상대방에게 혼잡 상태를 알려줄 수 있는데, 이 중 CWR, ECE는 TCP 헤더에 존재하고 ECT, CE는 IP 헤더에 존재합니다.
      - NS : ECN에서 사용하는 CWR, ECE 필드가 실수나 악의적으로 은폐되는 경우를 방어하기 위해 RFC 3540에서 추가된 필드
      - ECE :	ECN Echo 플래그. 해당 필드가 1이면서, SYN 플래그가 1일 때는 ECN을 사용한다고 상대방에게 알리는 의미. SYN 플래그가 0이라면 네트워크가 혼잡하니 세그먼트 윈도우의 크기를 줄여달라는 요청의 의미
      - CWR :	이미 ECE 플래그를 받아서, 전송하는 세그먼트 윈도우의 크기를 줄였다는 의미
  
  ### Q) TCP와 UDP의 통신방식에 대해 설명해주세요. (1:1, 1:N 등 ...)
  - TCP : 1:1
  - UDP : 1:1, 1:N, N:N

  ### Q) TCP와 UDP의 패킷 교환방식에 대해 설명해주세요 (가상 회선 방식, 데이터그램 방식)
  - TCP : 가상 회선 방식
  - UDP : 데이터그램 방식

  ### Q) TCP와 UDP는 checkSum 프로토콜을 다른 방식으로 검사하는데, 그 방식에 대해 설명해주세요.   
  <img src = "https://user-images.githubusercontent.com/67494004/236833420-f8196d93-d6e3-46bd-a27c-3d88e099a3e9.png" width="60%" height="50%">   

  TCP : Checksum 필수, 데이터를 송신하는 중에 발생할 수 있는 오류를 검출하기 위한 값

  ![image](https://user-images.githubusercontent.com/67494004/236833547-6b18f080-e557-4099-ae4e-9886b7125062.png)   
  UDP : Checksum 선택, 네트워크를 통해서 전송된 데이터의 값이 변경되었는지(무결성)를 검사하는 단순한 값
  UDP 헤더의 Checksum을 통해서(옵션) 헤더와 데이터 모두 포함한 사용자 데이터그램 전체에 대한 오류 탐지

  ### Q) TCP에서 흐름제어, 혼잡제어에 대해 설명해주세요.
  **흐름제어**
  - 송신자측 속도가 빠를 경우, 수신자측 버퍼가 다 찼을 때 데이터 손실이 발생합니다. 이를 방지하기 위해 흐름제어를 사용합니다.

  **혼잡제어**
  - 라우터가 값을 못받을 때 계속 재전송을 하게 되는데, 이 때 네트워크가 혼잡해짐
  네트워크 내의 패킷 수가 과도하게 생성될 때 혼잡이 발생하고, 이를 방지하기 위해 혼잡 제어

  ### Q-1) 혼잡제어 방식에 대해 설명해주세요.
  **AIMD(Additive Increase / Multicative Decrease)**   
  <img src = "https://user-images.githubusercontent.com/67494004/236832515-0fde4b1b-9581-449f-a814-f634eb2955c6.png" width="60%" height="50%">   

  - 송신 측이 transmission rate(window size)를 패킷 손실이 일어날 때까지 증가시키는 방식입니다.
    - additive increase : 송신 측의 window size를 손실을 감지할때까지 매 RTT 마다 1 MSS씩 증가시킨다. 
    - multiplicative decrease : 손실을 감지했다면 송신측의 window size를 절반으로 감소시킨다.
  - 단점 : AIMD는 window size를 1MSS씩 밖에 증가시키지 않기 때문에 네트워크의 모든 대역을 활용하여 빠른 속도로 통신하기까지 시간이 오래 걸립니다.
  
  **Slow Start (느린 시작)**   
  <img src = "https://user-images.githubusercontent.com/67494004/236832613-1c841c15-b7da-40ab-b766-6018223fc310.png" width="60%" height="50%">   

  - 송신 측이 window size를 1부터 패킷 손실이 일어날 때까지 지수승(exponentially)으로 증가시키는 방식입니다.
    - 초기 window size : 1 MSS
    - 매 RTT마다 window size를 2배로 키움 ( ex : 1, 2, 4, 8, 16...)
    - 패킷 손실을 감지하면 window size를 1 MSS로 줄임.
  - 처음에는 window size가 1이라 속도가 느리나 지수승으로 window size가 커지므로 속도도 빠르게 증가합니다.

  ### +) TCP 혼잡 제어 정책
  **TCP Tahoe**   
  <img src = "https://user-images.githubusercontent.com/67494004/236832657-93fce51a-fd78-4b4a-baca-2ef6a849d2fb.png" width="60%" height="50%">   
  -  처음에는 Slow Start를 사용하다가 임계점(Threshold)에 도달하면 AIMD 방식을 사용
     -  처음 window size는 1 MSS
     - 임계점까지는 Slow Start를 사용한다( window size가 2배씩 증가)
    - 임계점부터는 AIMD 방식을 사용한다( window size가 1씩 증가)
  - 3 duplicate ACKs 혹은 timeout을 만나면 아래와 같이 줄임.
    - 임계점 : window size의 절반
    - window size : 1
  - TCP Tahoe 방식은 3 duplicate ACKs를 만나고 window size가 다시 1부터 키워나가야 하므로 속도가 느립니다.
  
  **TCP Reno**   
  <img src = "https://user-images.githubusercontent.com/67494004/236832714-e613f20d-9efb-450b-9712-3e16cfcc6fcf.png" width="60%" height="50%">   
  -  TCP Tahoe와 비슷하지만 3 dupicate ACKs와 timeout을 구분한다는 점이 다릅니다.
    -  처음 window size는 1 MSS
    - 임계점까지는 Slow Start를 사용 (window size가 2배씩 증가)
    - 임계점부터는 AIMD 방식 사용( window size가 1씩 증가)
    - 3 duplicate ACKs를 만나면 
      - window size를 절반으로 줄이고 임계점을 그 값으로 설정
    - timeout을 만나면 
      - window size를 1로 줄인다. 임계점은 변하지 않는다.

  
  ### Q-2) 흐름제어에서 대표적인 해결방안 STOP AND WAIT, SLINDING WINDOW 에 대해 설명해주세요. 추가로 SLINDING WINDOW는 STOP AND WAIT의 단점을 보완하기 위해 나온건데 그 이유도 함께 설명해주세요.
  **STOP AND WAIT**   
  ![image](https://user-images.githubusercontent.com/67494004/236832901-69754e89-f053-48f7-8cf9-a996898f6699.png)   
  - 매번 전송한 패킷에 대해 확인 응답을 받아야만 그 다음 패킷을 전송하는 방법

  **SLINDING WINDOW**   
  ![image](https://user-images.githubusercontent.com/67494004/236832941-23e3318b-b5ee-4df3-b459-46c32337a3ad.png)   
  - 수신측에서 설정한 윈도우 크기만큼 송신측에서 확인응답없이 세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 제어기법
  - 먼저 윈도우에 포함되는 모든 패킷을 전송하고, 그 패킷들의 전달이 확인되는대로 이 윈도우를 옆으로 옮김으로써 그 다음 패킷들을 전송합니다.
    - 최초 윈도의 크기는 3way-handshaking 과정을 통해 설정
    - 이후 수신측에서 버퍼의 공간에 따라 변경합니다. ('윈도우'값은 TCP header에 존재하고 관리됩니다.)
    -  윈도우에 포함된만큼은 수신 측의 응답(ACK)없이도 보낼 수 있지만, 그 이상은 보낼 수 없습니다. 
    -  그 이상의 데이터 패킷을 보내기 위해서는 수신의 응답(ACK)가 확인되어 다시 윈도우의 크기가 갱신되어야 합니다.




### 참고
[TCP 혼잡제어](https://code-lab1.tistory.com/30)
[내용 및 사진 - 1](https://evan-moon.github.io/2019/10/08/what-is-http3/)
