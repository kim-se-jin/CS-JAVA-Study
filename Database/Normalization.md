# Normalization (정규화)

**정규화(Normalization)**
  - 정규화의 기본 목표는 **테이블 간에 중복된 데이터를 허용하지 않는다는 것**이며, 중복된 데이터를 허용하지 않음으로써 **무결성(Integrity)를 유지하고, DB의 저장 용량을 줄일 수 있다.**
  - 정규화를 하지 않았을 때에는 **이상(Anomaly) 현상**이 발생한다.

**이상(Anomaly) 현상**
  - 이상 현상은 3가지로 구분한다.
  1. **삽입 이상(Insertion Anomaly)** : 튜플 삽입 시 특정 속성에 해당하는 값이 없어 NULL을 입력해야 하는 현상
  2. **삭제 이상(Deletion Anomaly)** : 튜플 삭제 시 같이 저장된 다른 정보까지 연쇄적으로 삭제되는 경우
  3. **갱신 이상(Update Anomaly)** : 속성 값 갱신 시 중복된 데이터의 일부만 갱신되어 정보의 모순이 발생하는 현상

**함수적 종속성(Functional Dependency)** 
  - 정규화를 이해하기 전에 함수적 종속성에 대해서 이해 할 필요가 있다.
  - 함수 종속성은 어떤 릴레이션 R이 있을 때 X와 Y를 각각 속성의 부분집합이라고 가정했을 때, **X의 값을 알면 Y의 값을 알 수 있고**, **X의 값에 따라 Y의 값이 변경되는 Y는 X에 함수적 종속**이라고 한다.
  - **X를 결정자, Y를 종속자**라고 한다.
  - 함수적 종속관계에는 **완전 함수적 종속, 부분 함수적 종속, 이행적 함수 종속**이 있습니다.
  1. **완전 함수적 종속**
  ![완전 함수적 종속](https://github.com/bombo-dev/CS-JAVA-Study/assets/74203371/43e53522-4a00-4b50-9674-f53ee319e5da)   
  - 종속자가 **기본키에만 종속되며, 기본키가 여러 속성으로 구성되어 있을 경우 기본키를 구성하는 모든 속성이 포함된 기본키의 부분집합에 종속**된 경우
  - 즉, 여러 속성으로 구성되어 있을 경우 **어떠한 속성이 기본키의 최소성을 만족시키는 경우**를 말한다.

  2. **부분 함수적 종속(Partial Functional Dependency)**
  ![부분 함수적 종속](https://github.com/bombo-dev/CS-JAVA-Study/assets/74203371/141efcb0-f4ae-4d7b-84a9-523772b07711)
  - 릴레이션에서 종속자가 기본키가 아닌 다른 속성에 종속되거나, 기본키가 여러 속성으로 구성되어 있을 경우 기본키를 구성하는 속성 중 일부만 종속되는 경우
  - 즉, 여러 속성으로 구성되어 있을 경우 **어떠한 속성에 대해서 기본키의 최소성을 만족시키지 못하는 경우**를 말한다.
  
  3. **이행 함수적 종속(Transitive Functional Dependency)**
  ![이행 함수적 종속](https://github.com/bombo-dev/CS-JAVA-Study/assets/74203371/2c653086-6361-42ac-ab16-b9010ddbc104)
  - 릴레이션에서 X, Y, Z라는 3개의 속성이 있을 때 **X -> Y, Y -> Z 라는 종속 관계가 있을 경우, X -> Z가 성립될 때**를 말한다.

### 제 1 정규화
![제 1 정규형 위반](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNbQUm%2FbtqT18yag04%2FpTXJX3wB23ouk8az7EgWQ1%2Fimg.png)   
- `제 1 정규화`는 **테이블의 컬럼이 원자값(Atomic Value) 즉, 하나의 값을 갖도록 테이블을 분해하는 것**입니다. 
- 위 예시는 `제 1 정규형`을 만족하지 못하는 상황입니다. 해당 테이블을 정규화를 수행하게 되면 다음과 같이 변하게 됩니다.   
![제 1 정규화 수행](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMlNZj%2FbtqT17FWVot%2FjUKTAUyOdrH83pRraKw3K0%2Fimg.png)

### 제 2 정규화
![제 2 정규형 위반](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FylbaZ%2FbtqT8Jc4K3s%2F0VFTPoKKFkbxZghKWDwKo1%2Fimg.png)
- **제 1 정규형을 만족하는 테이블에 대해서 완전 함수 종속을 만족하도록 테이블을 분해하는 것**입니다. 즉, **부분 함수 종속을 제거 하는 것**입니다. 
- 위 예시는 `제2 정규형`을 만족하지 못하는 상황입니다. 한 강좌가 한 강의실에서만 이루어질 경우, 현재 기본키가 학생번호, 강좌이름으로 구성되어 있을 때 강좌이름 만으로도 강의실을 구분 할 수 있기 때문입니다. 해당 테이블을 정규화를 수행하게 되면 다음과 같이 변하게 됩니다.   
![제 2 정규화 수행](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbluCnc%2FbtqT7VEOf04%2FMe8DfY7rtycgJPYlYQKEWK%2Fimg.png)

### 제 3 정규화
![제 3 정규형 위반](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FenwN1N%2FbtqUeiMyErd%2FsP8NKCe70NKsZncGuhO9uK%2Fimg.png)
- **제 2 정규형을 만족하는 테이블에 대해서 이행적 종속을 없애도록 테이블을 분해하는 것**입니다. 즉, **이행 함수 종속을 제거 하는 것**입니다.
- 위 예시는 `제 3 정규형`을 만족하지 못하는 상황입니다. 기본키는 학생 번호이고, 한 명의 학생은 한 가지 강의밖에 듣지 못한다고 가정했을 때, 수강료가 강좌이름에 종속되어 있을 경우, 수강료는 학생번호에도 종속되는 이행종속이 발생되게 됩니다. 해당 테이블을 정규화를 수행하게 되면 다음과 같이 변하게 됩니다.
![제 3 정규화 수행](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fci1le3%2FbtqUeXnPnpD%2FyKkURqr8cZl21f5erx42QK%2Fimg.png)

### BCNF 정규화
![BCNF 정규형 위반](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBN6xu%2FbtqT6IlqRF4%2FMvBoxYMxtgS1JT7t1AymnK%2Fimg.png)
- **제 3정규형을 만족하는 테이블에 대해서 모든 결정자가 후보키가 되도록 테이블을 분해하는 것입니다.** 즉, 테이블 내 모든 속성이 유일성과 최소성을 만족하도록 만드는 정규화입니다.
- 위 예시는 기본키가 학생번호 특강이름으로 이루어졌을 때, 학생번호 특강이름이 교수를 결정합니다. 하지만 교수가 한 가지 강의만 진행한다고 가정했을 때, 교수또한 특강이름의 결정자가 되지만 해당 테이블에서는 중복된 값이 발생해서 유일성을 위배하므로 후보키가 될 수 없습니다. 해당 테이블을 정규화를 수행하게 되면 다음과 같이 변하게 됩니다.   
![BCNF 정규화 수행](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3cbHr%2Fbtq3mNylPan%2Fc6b2lBuH4OkdDNmrzGHWUk%2Fimg.png)

### Q) 프로젝트를 진행하면서 정규화 혹은 역정규화의 필요성을 느껴서 해보신 경험이 있다면 얘기해주세요.
- **제 3 정규형**을 위반하여 테이블의 조회 성능을 높인 경험이 있습니다. 통합 테이블 기법을 사용하여 슈퍼타입 서브타입에 대한 공통 부분에 대해서는 유지하고 추가적으로 어떤 세부 타입에 따라 값이 별개로 필요한 상황이었는데, 이때 세부 항목에 대한 필드가 많지 않을 것이라고 판단해서 테이블 내부에 구분하기 위한 Dtype 필드를 명시하고 해당 Dtype 필드에 해당 값들을 종속시켜 해당 값들이 기본 키에도 종속적이지만 Dtype에도 종속적인 이행 종속을 지키지 않았던 경험이 있습니다.

  ### Q) 외래키를 꼭 사용해야 하는지, 아니면 사용하지 않아도 되는지에 대한 의견을 말씀해주세요.
  - 외래키를 사용하지 않는 다는 것은 테이블과 관련이 있는 데이터들을 관계로 인한 테이블을 구성하지 않고, 조인에 의한 성능 저하로 인해 한 테이블에 관계를 지정할 수 있는 모든 데이터들을 한 테이블에 넣는 것으로 보입니다.
  - 이럴 경우에 해당 테이블이 어떠한 역할을 하는지 파악 하기가 어려우며, 이상현상등이 발생할 가능성이 높고, 또 테이블에 어떠한 필드가 추가되었을 때 수정하기가 어렵다는 단점이 존재합니다. 물론 테이블을 통합 했을 때 필드가 적다면 조인을 하지 않아 조회 성능을 향상 시킬 수 있다는 장점이 있기 때문에, 필드 수 혹은 조인의 횟수에 대해서 고민해서 트레이드 오프를 잘 판단해야 된다고 생각합니다.

### Q) 정규화를 계속 진행을 하였을 때의 단점이 무엇인가요?
  - 정규화를 계속해서 진행을 한다는 것은 테이블을 계속해서 분할을 하는 것을 의미합니다. 테이블을 계속해서 분할 한 상탸에서 원하는 데이터들을 조회하기 위해서는 조인 기법을 이용하여 테이블을 조회를 해야 합니다.
  - 이때, 인덱스가 없는 상황에서 테이블을 조인하게 되었을 때, 어떠한 조인 기법을 택하냐에 따라 다르지만 조인으로 인해 성능저하가 발생합니다.
  - 따라서, 정규화를 진행하는 것이 무조건적으로 좋다 라고 말하기는 어렵습니다.

### 참고 자료
[[정규화]https://mangkyu.tistory.com/110](https://mangkyu.tistory.com/110)   
[[정규화2]https://code-lab1.tistory.com/48](https://code-lab1.tistory.com/48)   
[[이상현상]https://code-lab1.tistory.com/47](https://code-lab1.tistory.com/47)   
[[함수적 종속]https://dodo000.tistory.com/20](https://dodo000.tistory.com/20)
