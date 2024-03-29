# JDK 8


### Q) 스트림 API에 대해 설명해주세요

람다식를 이용한 기술 중에 하나로 컬렉션, 배열 등을 조작 및 가공, 변환하여 원하는 값으로 반환해주는 API

### Q) 스트림이 나오게된 이유는?

- 자바를 이용해 함수형프로그래밍을 할수있게끔 지원해주기위해
- 데이터 조작작업을 병렬로 구성하여 실행할수있게되어 **데이터 변환 수행 방식**에 집중하기보다는 **수행되는 데이터변환**에 중점을 두어 간결하고 가독성이 좋은 코드를 작성할수있게끔하기위해 

### Q) 일반적인 for-loop 보다 스트림의 for-each가 느린이유

- 반복문 내부에 특정조건을 만족하면 종료조건이있는경우 기존의 for-loop는 조건을 만족하면 바로 종료하지만 stream의 forEach는 종료조건이 만족되도 모두 조건을 확인한다.

### Q) 함수형 인터페이스에대해 설명해주세요

- 추상메서드를 하나만 가지고있는 인터페이스
- 함수형 인터페이스여야만 람다표현식에 사용할수있다.

### Q) java에서 제공하는 함수형 인터페이스에대해 설명해주세요

- `Supplier<T>`
  - 매개변수 없이 반환값만을 가진다.
- `Consumer<T>`
  - 매개변수를 받고 반환값은 가지지않는다. 
- `Predicate<T>`
  - 객체 T를 받고 
- `Function<T,R>`
  - 객체 T를 매개변수로 받고 R로 반환한다. 

### Q) Optional 에대해 설명해주세요

- null 을 처리하기위한 좋은방법을 제공하는 API로 null을 반환할수있는 경우 Optional을 사용해서 NullPointException을 효율적으로 처리할수있다. 
