# 세션 계층

### 1. 세션 계층에 대해서 설명해주세요.

* 세션 계층은 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공해주고, 네트워크 상 양쪽 연결을 지속시켜주는 역할을 합니다.
* 통신을 하기 위해 전이중통신 혹은 반이중통신 같은 전달 방식도 관리를 하며, TCP/IP 세션을 만들고 유지하며 세션이 종료되거나 전송이 중단될 시 복구를 하기 위한 동기화도 제공합니다.

### 2. 세션 계층의 동기화에 대해서 설명해주세요.
  ![세션계층 동기화](https://mblogthumb-phinf.pstatic.net/MjAxOTA0MjNfMjMx/MDAxNTU1OTgzNDg2NTU1.yoHsHSSuV85zupTfvyxeefdTAaq96-KdvcP9-yI99tog.8baNq2WQKtnxFcEnUiuW_DxTXzmP_y1mIAkN0pITkcgg.PNG.cni1577/%EC%BA%A1%EC%B2%98.PNG?type=w800)
  * 세션 계층은 **서로 간의 통신 중에 동기점을 선택해서 해당 지점까지의 데이터는 안전하게 도착했다는 것을 보장하여 동기화를 수행**한다. 주 동기점과 주 동기점 사이에는 부 동기점이 존재하는데, 주 동기점에 대하여 어디서 잘못되었는지 확인하고 내부의 부 동기점에서 재차 확인하여 거슬러 올라가면서 확인이 가능합니다. 

  #### Q) 전이중통신과 반이중통신에 대해서 설명해주세요.
  1. **전이중통신** : 전이중통신은 두 디바이스간 통신선을 송신선과 수신선 두 가지를 따로 사용하여 데이터의 송수신을 각 디바이스가 동시에 가능하도록 하는 통신 방식입니다.
  2. **반이중통신** : 반이중통신은 전이중통신과 달리 두 디바이스간 통신선이 하나만 존재합니다. 송수신선을 서로가 공유중이기 때문에 한 쪽에서 송신을 하는 도중에 다른 쪽에서 송신을 하게 되면 충돌 문제가 발생하므로 반대쪽에서는 수신만 하도록 하는 통신 방식입니다.

### 3. 세션 하이재킹에 대해서 설명해주세요.
![세션 하이재킹](https://postfiles.pstatic.net/MjAxNzEwMTBfMjA4/MDAxNTA3NjQwNzQyNDk5.EUY9CqxhBp5k3OeJIovWoZCtXpjnGnX34vtapNcmH9Mg.MhB8H2gWVv-siQeeJb1DegV0sDEYrzekxcGR4Bt3un8g.PNG.wnrjsxo/image.png?type=w773)
* 세션이랑 두 호스트가 연결이 된 상태를 의미합니다. 여기서 세션 하이재킹이란 이 연결이 활성화 된 상태를 가로채는 것을 말합니다.
* 세션 하이재킹은 TCP/IP 연결에서 발생하는 취약점을 이용한 공격입니다.
* TCP/IP 연결 시에 취약점은 TCP/IP는 3-way-handShake를 하는 과정에서 클라이언트와 서버가 각각 SequenceNumber와 Acknowledgment Number를 주고 받으면서 받아야 하는 데이터인지 확인을 합니다. 만약에 문제가 있다면 이를 바로 잡기 위해 재수행을 하는데 이러한 점을 공격자는 이러한 점을 악용하여 클라이언트와 서버에게 각각 잘못된 시퀀스 넘버를 위조하여 제공하고, 스니핑을 통해 SequenceNumber를 알아낸 뒤 바로 잡는 동안 공격자가 세션을 가로채서 전송을 하는 방식입니다.


### 참고자료 주소
- https://m.blog.naver.com/cni1577/221520444328
- https://hydroponicglass.tistory.com/280
- https://blog.naver.com/PostView.nhn?blogId=wnrjsxo&logNo=221114275533&parentCategoryNo=&categoryNo=2&viewDate=&isShowPopularPosts=true&from=search