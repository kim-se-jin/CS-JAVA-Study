# 응용 계층

### 1. 응용 계층에 대해서 설명해주세요.
* 응용 계층은 사용자 또는 애플리케이션이 네트워크에 접근할 수 있도록 해주는 영역이다. 사용자를 위한 인터페이스를 제공하며, 사용자에게 보이는 유일한 계층입니다.
* 주된 프로토콜로 HTTP, FTP, SMTP, POP3, IMAP, Telnet 등과 같은 많은 프로토콜이 존재합니다.

### 2. DNS에 대해서 설명해주세요.
* DNS 프로토콜은 응용 계층에 위치한 프로토콜입니다.
* DNS가 하는 주된 일은 IP를 사람들이 보기 편한 도메인으로 변환하거나, 도메인을 IP로 변환하는 일을 담당합니다.
* DNS의 특징으로 크게 2가지로 볼 수 있습니다.
  1. 추가적으로 복잡한 호스트네임에 대하여 여러가지 별칭을 가질 수 있습니다. 이로 인해 메일서버 별칭 같은 것도 가능합니다. ex) `relay1.west-coast.enterprise.com` -> `enterprise.com`, `www.enterprise.com`
  2. 같은 도메인에 대해서 여러 IP 지정이 가능합니다. 따라서 같은 도메인 질의시 DNS는 IP를 돌려가면서 사용합니다.
* 사용자가 직접 사용하는 프로토콜이 아니라, 웹 브라우저가 실행하는 프로토콜입니다.
* 포트 번호는 53번 포트를 사용하고, 평소에는 UDP/53 을 사용하다가 두 가지 경우에만 TCP/53을 사용합니다.
  1. 전송데이터가 512 Bytes 이상
  2. Zone transfer(존 영역을 전송할 때)

### 3. DHCP에 대해서 설명해주세요.
* DHCP는 호스트의 IP주소와 각종 TCP/IP 프로토콜의 기본 설정을 클라이언트에게 자동적으로 제공해주는 프로토콜로 동적주소 할당 프로토콜입니다.
* DHCP는 UDP 프로토콜을 사용합니다. 클라이언트가 IP가 설정이 안되어 있는 경우 DHCP 서버를 찾아야 하는데, 이 과정에서 클라이언트는 DHCP 서버의 위치를 모르기 때문에 브로드캐스팅을 통해 DHCP 서버를 찾아야합니다. 이 과정에서 신뢰성보다는 빠른 속도가 중요하기 때문에 UDP를 사용합니다.
* **[장점]** : DHCP는 PC의 수가 많거나 PC 자체의 변동사항이 많은 경우 IP 설정이 자동으로 되어서 효율적으로 사용이 가능하고 IP 충돌을 막을 수 있습니다.
* **[단점]** : DHCP 서버에 의존하기 때문에 서버가 다운되면 IP 할당이 제대로 이루어지지 않는다는 문제가 있습니다.

### 4. Https에서 서버가 인증서를 발급받고 클라이언트와 TLS(SSL) HandShake에 대해서 설명해주세요.
![SSL HandShake](https://i.imgur.com/YIfy1wK.png)
1. 먼저 서버는 CA에게 일정 금액을 제공하고 SSL 인증서를 받습니다.
2. 클라이언트가 서버에게 메시지를 전송합니다. 메시지에는 TLS버전, 암호화 알고리즘, 무작위 바이트 문자열이 포함됩니다.
3. 서버가 클라이언트에게 메시지를 전송합니다. 메시지에는 SSL 인증서, 선택한 암호화 알고리즘, 무작위 바이트 문자열이 포함됩니다.
4. 클라이언트는 해당 SSL 인증서가 신뢰할만한지 CA에 검증합니다.
5. 클라이언트는 서버에서 제공한 무작위 바이트 문자열을 서버의 공개키로 암호화된 premaster secret key를 서버에 전송합니다.
6. 서버는 premaster secret key를 개인키로 복호화합니다.
7. 클라이언트와 서버는 클라이언트의 무작위 바이트 비트열, 서버의 무작위 바이트 비트열, premaster secret key를 통해 검증하고, 세션 키를 생성합니다. 이때, 양쪽 다 같은 키(대칭키)가 생성됩니다.
8. 클라이언트는 세션 키로 암호화된 완료 메시지를 전송합니다.
9. 서버도 세션 키로 암호화된 완료 메시지를 전송합니다.
10. HandShake가 완료되고, 세션 키를 이용해 통신을 진행합니다. 이 과정에서는 대칭키 암호화를 사용하여 통신합니다.

### 5. CORS에 대해서 설명해주세요.
* CORS에 대해서 설명하기 전에 먼저 SOP에 대해서 알아야합니다.
* **SOP(Same-Origin-Policy)** 는 **같은 출처에서만 리소스를 공유할 수 있다는 규칙입니다.** SOP를 도입하게 된 이유는 출처가 다른 두 애플리케이션이 자유로이 소통을 하게 된다면 해커가 **CSRF(Cross-Site Request Forgery)** 혹은 **XSS(Cross-Site Scripting)** 등의 방법을 이용해서 개인 정보를 탈취할 수 있기 때문입니다.
* SOP는 **Origin을 Scheme, Host, Port 3가지가 동일하다면 동일한 것으로 판단**을 합니다.
* 세상이 발전하게 되면서 다른 출처의 리소스를 사용해야 하는 상황이 적지않게 발생하게 되면서 CORS가 생겨났고, **CORS**는 **SOP 정책을 위반하더라도 CORS 정첵에 따르면 다른 출처의 리소스라도 허용을 하게 해주는 정책**입니다.
* **[기본 동작]**
  1. 다른 출처의 리소스 요청시 요청 헤더에 origin 이라는 필드에 요청을 보내는 출처를 담아서 보낸다.
  2. 서버가 응답시 응답 헤더에 Access-Control-Allow-Origin 이라는 필드에 허용가능한 리소스 출처를 담아서 보낸다.
  3. 브라우저가 요청 헤더에 보냈던 origin과 Access-Control-Allow-Origin 을 비교하여 유효한 응답인지 결정한다.

* **CORS는 크게 3가지 시나리오**로 동작합니다.

  

#### Preflight Request
  ![Preflight Request](https://evan-moon.github.io/static/c86699252752391939dc68f8f9a860bf/21b4d/cors-preflight.png)
  - 일반적으로 웹 애플리케이션을 개발할 때 마주치는 시나리오 입니다. 요청을 한 번에 보내지 않고 예비 요청과 본 요청으로 나누어서 본 요청으로 보내기 전에 브라우저 스스로 이 요청을 보내는 것이 안전한지 확인하는 방식입니다. 
#### Simple Request
  ![Simple Request](https://evan-moon.github.io/static/d8ed6519e305c807c687032ff61240f8/21b4d/simple-request.png)
  - 예비 요청을 보내지 않고 바로 서버에게 본 요청을 보낸 후 브라우저가 Access-control-allow-origin을 확인하는 방식입니다. 이렇게만 보면 Preflight Request보다 속도도 빠르고 좋을 것 같지만 몇 가지 조건이 존재합니다.
    1. HTTP 메서드가 GET, HEAD, POST 이여야만 한다.
    2. Accept, Accept-Language, Content-Language, Content-type, DPR, DownLink, Save-Data, viewport-width, width 요청 헤더만 사용이 가능합니다.
    3. Content-type 중에서도 `application/x-www-form-urlencoded`, `multipart/form-date`, `text/plain`만 허용됩니다.
  - 최근에는 text/xml, application/json을 사용한 api 통신을 많이 사용하기 때문에 조건 충족이 까다롭습니다.
#### Credentialed Request
  - 인증된 요청을 추가하여 사용하는 방식입니다. CORS 기본 방식보다는 다른 출처간 통신에서 보안을 강화하고 싶을 때 사용합니다.   
  XMLHttpRequest 혹은 fetch API는 비동기 API로써 쿠키 혹은 인증과 관련된 헤더를 요청에 담지 않는데, 이러한 요청을 달 수 있게 도와줍니다.
  - 인증 옵션은 3가지로 구분합니다.
    1. same-origin : 같은 출처 간 요청에만 인증 정보를 담을 수 있다.
    2. include : 모든 요청에 인증 정보를 담을 수 있다. 하지만 `Access-Control-Allow-Origin: *`로 모든 URL을 허락하는 상황은 불가능하고, 응답 시 URL을 명시해주어야 하고, `Access-Control-Allow-Credentials: true` 헤더를 추가해주어야 한다.
    3. omit : 모든 요청에 인증 정보를 담지 않는다.

### 참고자료 주소
- https://steady-coding.tistory.com/504
- https://galid1.tistory.com/53
- https://kanoos-stu.tistory.com/46
- https://wayhome25.github.io/cs/2018/03/11/ssl-https/
- https://evan-moon.github.io/2020/05/21/about-cors/
- https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F