# 접근제어자

### 1. 접근제어자에 대해서 설명해주세요.
* 접근제어자는 **클래스 또는 클래스의 내부의 멤버들에 사용되어 해당 클래스나 멤버들을 외부에서 접근하지 못하도록 접근을 제한하는 역할을 수행하는 것**입니다.
* 자바에는 **public**, **default**, **protected**, **private** 총 4가지로 구성이 되어 있습니다.

![Image](https://i0.wp.com/blog.codestates.com/wp-content/uploads/2022/11/%EC%9E%90%EB%B0%94-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4%EC%9E%90-%ED%91%9C.png?w=1312&ssl=1)

### 2. DI 사용 시 어떤 접근제어자를 사용하여 개발을 하는가
  - 외부 객체에서 내부 객체에 속성에 직접 접근을 하면 안되기 때문에 private를 사용해주어야 하며, 추가적으로 해당 객체 내에 구성클래스가 있는 경우 의존 주입을 무조건 받도록 하는 것이 좋기 때문에 final 키워드를 사용해서 객체 생성 시 컴파일 단계에서 체크하도록 하여 의존 주입을 잊지 않도록 합니다.

  #### Q) 스프링 프레임워크가 없는 세상이라면 DI를 어떻게 구현 할 것인가.
  - 클라이언트가 요청 할 때마다 생기는 것이 아닌 애플리케이션이 실행 할 때만 필요한 것이고, 그 클래스의 수가 많지 않다면 직접 new 키워드를 사용해서 직접 주입을 해 줄것이고 그 외에 상황에서는 의존주입 받아야 하는 클래스에 대해서 직접 싱글톤 패턴을 통해 구현을 하고 동시성 처리를 하여 구현을 할 것 같습니다.
  - 즉, **IOC(Inversion Of Control, 제어의 역전)** 를 직접 구현해서 사용을 할 것 같습니다.

**[내용 및 사진 출처]**
- https://www.codestates.com/blog/content/%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%8A%B9%EC%A7%95
  
