# TCP/IP - Network Access Layer (OSI - Physical & Data Layer)

![image](https://github.com/kim-se-jin/CS-JAVA-Study/assets/76711238/008cd036-165d-481e-8f03-2d866c1b8866)

- 물리적인 데이터의 전송을 담당하는 계층
- 인터넷 계층과 달리 **같은 네트워크 안에서 데이터가 전송**됩니다.
- 노드 간의 신뢰성 있는 데이터 전송을 담당하며, 논리적인 주소가 아닌 물리적인 주소인 MAC을 참조해 장비간 전송을 하고, 기본적인 에러 검출과 패킷의 Frame화를 담당한다.

> - 역할 : 실제 데이터인 프레임 송수신
- 데이터 단위 : Frame
- 전송 주소 : MAC
- 프로토콜 : Ethernet  
- 장치 : 브릿지, 스위치

**OSI : 1계층 물리 계층(Physical Layer)**
- 케이블이 연결되어 있는 기기에 대한 신호 전달을 수행하는 계층
- 데이터 링크 계층의 프레임을 받고, 다음 장치에 구리나 광섬유(케이블) 또는 무선 통신 매체를 통신해 전송하기 위한 신호로 바꾸어 줍니다. 
- 물리적 매체를 통해 데이터(bits)를 전송하기 위해 요구되는 기능들을 정의합니다.
- USB 케이블, 동축 케이블 등 두 디바이스 간의 실제 접속을 위한 기계적, 전기적 특성에 대한 규칙을 정의합니다.

|제목|내용| 
|------|---| 
|데이터 전송 단위|비트(bit)| 
|프로토콜 |RS-232, RS-449 등 케이블| 
|장비 | 허브, 리피터| 

(+) 허브 : 허브는 여러 대의 기기를 연결하고 신호를 증폭하고 재생하는 역할을 하며 플러딩을 일으킵니다.

**OSI : 2계층 데이터링크 계층(Data Link Layer)**
- 네트워크 계층 패킷 데이터를 물리적 매체에 실어 보내기 위한 계층 
- 포인트 투 포인트(Point to Point) 간 신뢰성있는 전송을 보장하기 위한 계층
- 신뢰성있는 전송을 위해 오류 검출 및 회복을 위한 오류 제어 기능 수행
- 송수신측의 속도 차이 해결을 위해 흐름 제어 기능 수행

|제목|내용| 
|------|---| 
|데이터 전송 단위|프레임(frame)| 
|프로토콜 | Ethernet(이더넷), PPP, HDLC, ALOHA 등| 
|장비 | 브릿지, 스위치 (스위치 안에는 MAC 주소 테이블 존재)|   

### Q) Mac 주소에 대해 설명해주세요.
 랜카드에 할당된 전 세계에서 유일한 번호로 물리 주소입니다. 
- 컴퓨터에 장착된 랜(LAN) 카드를 구별하기 위해 만들어진 식별 번호입니다. 
   ### Q-1) 어떤 하드웨어
   - Network interface card (LAN card) 에 위치합니다. 

### Q) 데이터 링크 계층에서 자주 사용되는 Ethernet protocol 에 대해 설명해주세요.
- 랜에서 데이터를 주고받기 위한 규칙으로, 허브와 같은 장비에 연결된 컴퓨터와 데이터를 주고받을 때 사용합니다.
-  고유의 MAC 주소를 가지고 이 주소를 이용해 상호간에 데이터를 주고 받을 수 있도록 만들어졌습니다.
- 이더넷에서는 수신처 MAC 주소를 보고 **자기에게 온 것만 받고 다른 프레임은 파기**합니다. (멀티캐스트의 경우 그룹 번호가 들어가있기 때문에 자신이 속한 그룹 번호로 수신처가 적혀있다면 수신)
- CSMA/CD : 이더넷은 CSMA/CD라는 데이터 전송 시점을 늦추는 방법을 사용하여 충돌을 방지합니다.
- 하지만 최근에는 스위치(switch)라는 장비를 사용하면서 CSMA/CD를 사용하지 않습니다.

### Q) 처음에 MAC 주소 테이블에 아무것도 존재하지 않을 때 어떻게 MAC 주소 테이블을 채우는지 설명해주세요.
- MAC 주소 테이블에 등록되어 있지 않은 MAC 주소가 들어오면, 송신 포트를 제외한 모든 포트에 데이터를 전송합니다. 이를 `플러딩 (flooding)` 이라고 합니다. 

<details>
<summary>MAC 주소 테이블 (MAC address table)</summary>

- 스위치의 포트 번호와 해당 포트에 연결되어 있는 컴퓨터의 MAC 주소가 저장된 데이터베이스입니다.
스위치에 연결된 컴퓨터가 프레임(데이터)을 전송하면 MAC 주소 테이블을 확인하고 해당 포트로 전송합니다.
- 만약 테이블에 저장되지 않는 주소라면, MAC 주소와 포트 번호를 데이터베이스에 정보를 저장 합니다.
- 이를 MAC 주소 학습 기능이라고 하고, 허브에는 없는 기능입니다.

</details>

### Q) 물리 계층에서 전기 신호가 약해지는 경우, 이를 보완해주기 위해 어떻게 하는지 설명해주세요.  
- 긴 케이블(동선)을 지나는 동안 신호가 약해지는데 그렇게 되면 신호의 진폭의 약해져서 수신측에서 데이터를 못 읽을 수도 있습니다. 이러한 문제점을 해결하기 위하여 약해진 신호를 다시 강하게 해주는 증폭기를 사용합니다.
- 신호의 증폭 / 재생 => 허브로!
   - 감쇠된 신호를 **허브**를 통해 증폭 / 재생한다. 원래 신호를 증폭하기 위한 기계로 리피터(Repeater)가 있는데, 리피터는 허브처럼 여러개의 기기들을 연결할 수 없다는 단점이 있습니다. 
   - 그래서 **허브에 신호를 증폭하는 기능을 추가**해 사용하곤 합니다. 
   - 추가로 신호를 증폭 / 재생하지 않는 허브도 있는데, 이런 허브는 패시브(passive) 허브라고 부르고, 증폭기능을 하는 허브를 액티브(active) 허브라고 부릅니다.

### Q) 데이터 링크 계층은 헤더가 붙는 방식이 다른 계층과 다른데, 이를 설명해주세요.
- 트레일러(FCS) 가 붙습니다.
- 트레일러는 데이터 뒤에 붙고, FCS(Frame Check Sequence)라고 부르기도 합니다.
- FCS는 데이터 전송 도중 오류가 발생하는지 확인하는데 사용됩니다.
- 다른 계층에선 단순히 헤더 하나씩만 추가되는데 데이터 링크에서는 FCS 가 추가적으로 붙습니다. 
![image](https://user-images.githubusercontent.com/76711238/236818056-3795767b-29bc-474a-95ab-eca30d058bab.png)

    ### Q-1) 각 계층에서의 데이터를 어떻게 부르는 지 설명해주세요.
    - 이미지 참조
![image](https://user-images.githubusercontent.com/76711238/236815251-373e8061-9be0-4518-b6a5-bf179245d80f.png)

#### 사진 & 내용 출처

https://jinmay.github.io/2018/12/09/network/daily-network-first-layer/

https://www.google.com/url?sa=i&url=https%3A%2F%2Ffreloha.tistory.com%2F20&psig=AOvVaw3MQJsoUixvuSrJi0DfcJps&ust=1683633451536000&source=images&cd=vfe&ved=0CBMQjhxqFwoTCLicp8DV5f4CFQAAAAAdAAAAABAE