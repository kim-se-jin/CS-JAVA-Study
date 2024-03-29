# Generic

### 1. Generic 이란 
  * 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입 체크를 해주고 형변환의 번거로움을 줄여주는 기능을 하는 것입니다.   

  #### Q) Generic에는 어떤 타입이 가능한가?
  - 제너릭은 레퍼런스 타입만 사용이 가능합니다. 따라서 기본형 타입을 제너릭에 사용하려면 Wrapper 클래스를 사용해야합니다.

    #### Q) Generic의 장점에는 무엇이 있는가?
    - 타입의 안정성을 제공해주고, 타입 체크와 형변환을 생략할 수 있으므로 코드가 간결해진다.
    - 부모 타입을 미리 정할 수 있고, 다형성으로 유연한 설계가 가능하기 떄문에 재사용성도 높아진다.

  #### Q) 제너릭 타입이 컴파일 시에 제거되는 과정을 말해주세요.
  1. 제너릭 타입의 경계를 제거합니다. `<T extends Fruit>` 이때 T는 Fruit로 치환됩니다. 만약 `<T>` 였다면 Object로 치환됩니다.
  2. 타입 제거 후 타입이 일치하지 않는 곳은 형변환을 추가해줍니다.
  ```java
  List list = new ArrayList();

  Fruit get(int i) {
    //return list.get(i);  Object, Fruit 일치 X
    return (Fruit) list.get(i);
  }
  ```
  - 제너릭 타입을 컴파일 당시에 제거하는 이유는 JDK 1.5에 제너릭이 도입되었는데, 그 이전 코드와의 호환성을 위해 이러한 과정을 거치는 것이다.

    #### Q) 제한된 제너릭(Bounded Generic)의 장점에 대해서 설명해주세요.
    - 기존의 제너릭은 타입을 하나 밖에 선언하지 못하여 유연성이 좋지 않다는 문제가 있었습니다. 하지만 제한된 제너릭을 사용하면 유연성있게 특정 타입의 자손 혹은 구현체들에 대해 타입 지정을 할 수 있게 됩니다.

        #### Q) `List<Object>` 와 `List<?>` 의 차이에 대해서 설명해주세요.  
        - ``List<Object>`` 는 Object 타입만 들어 올 수 있고, ``List<?>``은 다양한 타입이 들어오는 게 가능합니다.
        - 와일드카드의 큰 장점은 형변환에 있다. 하지만, 컴파일 에러가 아닌 경고 메시지를 반환하므로 주의해서 사용해야 한다.

          #### Q) Integer 타입이 들어온다면 `<Object>`, `<?>` 둘 중 어디에 일치하는가
          - `<?>` 에 일치합니다.

            #### Q) 코드에서 `<T>` 와 `<?>` 가 달려있는 것을 보고 어떻게 해석할 것인가.
            - `<T>` 가 달려있다는 것은 정말 엄격하게 해당 타입만 사용해야 하는 것으로 판단하여, 형변환 이나 다른 타입을 사용하지 않도록 주의 할 것이고, `<?>`의 경우에는 여러가지 타입을 상황에 맞게 적절히 생성해서 사용하라는 것으로 해석 할 것 같다.