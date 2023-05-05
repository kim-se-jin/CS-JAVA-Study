# Wrapper
### Wrapper 클래스란 
  * **기본 자료타입(Primitive Type)을 객체로 다루기 위해서 사용하는 클래스**를 말합니다.

  #### Q) Wrapeer 클래스는 언제 사용하는가
  - 기본 값 간의 식별성으로 구분해야 될 때 사용할 수 있고, null을 허용해야 하는 경우 사용 할 수 있습니다.
  - 제너릭 및 Collection, Arrays 등을 사용 할 때 스트림을 쓰지 않고 컬렉션 API를 사용하기 위해서는 대부분 제너릭으로 인해 클래스 타입을 사용해야하기 때문에 이럴 경우에도 사용합니다. 

  #### Q) Boxing(박싱), Unboxing(언박싱)에 대해서 설명해주세요.
  ![사진1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbrryw5%2FbtrbhYdkjlR%2Fkd888gYsrnmPgcTGuXNpXk%2Fimg.png)
  - Primitive Type 과 Wrapper class 는 서로 상호 변환이 이루어집니다.
  - **박싱 : Primitive -> Wrapper**
  - **언박싱 : Wrapper -> Primitive**
  - JDK 1.5 버전부터는 AutoBoxing/Unboxing이 생겨 따로 형변환 처리를 해주지 않아도 변환됩니다.


### 참고이미지
[사진1](https://tragramming.tistory.com/97)