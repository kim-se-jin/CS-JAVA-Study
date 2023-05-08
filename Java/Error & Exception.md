# Error & Exception 
자바의 예외는 크게 3가지로 나눌 수 있습니다.

![image](https://user-images.githubusercontent.com/76711238/236800636-d2964fe2-27ff-4bb8-9e92-9639b266120f.png)

- 1. **에러(Error)**: 
   - 에러(Error)는 시스템에 무엇인가 비정상적인 상황이 발생한 경우에 사용됩니다. 주로 자바 가상 머신에서 발생시키는 것이며 예외와 반대로 이를 애플리케이션 코드에서 잡을 수 없습니다.
   - (ex) 메모리 부족(OutofMemoryError), 스택오버플로우(StackOverflowError)

- 2. **예외** 
   - 예외(Exception)란 입력 값에 대한 처리가 불가능하거나, 프로그램 실행 중에 참조된 값이 잘못된 경우 등 정상적인 프로그램의 흐름을 어긋나는 것을 말합니다. 자바에서 예외는 개발자가 직접 처리할 수 있기 때문에 예외 상황을 미리 예측하여 핸들링할 수 있습니다.

   > 컴파일러가 에러처리를 확인하지 않는 RuntimeException 클래스들은 unchecked 예외라고 부르고
예외처리를 확인하는 Exception 클래스들은 checked 예외라고 부릅니다.

   - 2-1. **체크 예외(Checked Exception)** : 
      - Checked Exception은 RuntimeException을 상속하지 않은 클래스입니다.
      - 명시적인 예외 처리를 해야 합니다. 
      - 컴파일 시점에 확인할 수 있습니다. (=> 따라서 반드시 에러 처리를 해야하는 특징(try/catch or throw)을 가집니다. )
      - 트랜잭션 안에서 동작할 때 Checked Exception이 발생하면 Rollback 되지 않는다는 특징이 있습니다.
         - **기본적으로 Checked Exception은 복구가 가능하다는 메커니즘** 을 가집니다. 
         - 복구가 가능하니 트랜잭션 도중 에러가 발생하더라도 롤백이 발생하지 않습니다.
         - 예를 들어, 특정 이미지 파일을 찾아서 전송해 주는 함수에서 이미지를 찾지 못 했을 경우 기본 이미지를 전송한다는 복구 전략을 가질 수 있습니다. 
         - 즉, **복구가 가능하니 Rollback은 진행하지 않는다**는 의미이다.
      - (ex) 존재하지 않는 파일의 이름을 입력(FileNotFoundException)
실수로 클래스의 이름을 잘못 적음(ClassNotFoundException)

   - 2-2. **언체크 예외(Unchecked Exception)** : 
      - Unchecked Exception은 RuntimeException을 상속한 클래스입니다.
      - 명시적인 예외 처리를 하지 않습니다. 즉, 에러 처리를 강제하지 않습니다. 
      - 런타임 시점에 확인할 수 있습니다. ( RuntimeException의 하위 클래스이기에 실행 중에(runtime) 발생할 수 있는 예외를 의미합니다. )
      - 트랜잭션 안에서 동작할 때 Unchecked Exception이 발생하면 롤백된다는 특징이 있습니다. 
      - (ex) 열의 범위를 벗어난(ArrayIndexOutOfBoundsException)
값이 null이 참조변수를 참조(NullPointerException)

![image](https://user-images.githubusercontent.com/76711238/236801670-80cb9e99-a32c-4571-96d5-f6260598eba6.png)


### Q) Checked Exception 과 Unchecked Exception 의 transaction 예외 처리 방식을 설명해주세요.
- Checked Exception : 기본적으로 commit 이 됩니다. (무조건 처리돼야 하는 exception)
- Unchecked Exception : rollback 이 됩니다. (무조건 처리돼야 하지 않아도 되는 exception)

   ### Q-1) @Transactional 는 어떻게 구현되나요?
   - proxy 원리를 사용해서 구현됩니다. 
      - 프록시 패턴을 사용하는 이유 : 프록시 객체는 원래 객체를 감싸고 있는 객체로, 원래 객체와 타입은 동일합니다. 프록시 객체가 원래 객체를 감싸서 client의 요청을 처리하게 하는 패턴입니다.
      - 프록시 패턴을 통해 접근 권한을 부여할 수 있습니다.
      - 프록시 패턴을 통해 부가 기능을 추가할 수 있습니다.
   ### Q-2) @Transactional 이 붙지 않은 메소드의 내부에서  @Transactional 이 붙은 메소드를 사용할 시, 이 내부 메소드도 @Transactional이 적용될까요?
   - 적용되지 않습니다. 
   - 예시는 아래와 같습니다. 

   ```java
      public class BookImpl implements Books {
      public void addBooks(List<String> bookNames) {
         bookNames.forEach(bookName -> this.addBook(bookName));
      }
      
      @Transactional
      public void addBook(String bookName) {
         Book book = new Book(bookName);
         bookRepository.save(book);
         book.setFlag(true);
      }
   }
   ```
   - 위와 같은 상황에서 addBooks메서드의 내부에서 호출하는 addBook 메서드의 @Transactional 어노테이션이 적용되지 않습니다. 

   - Spring은 AOP를 이용해 `@Transactional` 어노테이션을 선언한 메서드가 실행되기 전 transaction begin을 삽입하고, 메서드 실행 후에 Transaction commit 코드를 삽입하여, 객체 변경감지를 수행하도록 유도합니다.

   - Spring의 코드 삽입 방식은 크게 2가지가 있습니다.

   - 1) 바이트 코드 생성(CGLIB)
   - 2) 프록시 객체 사용
   - 2가지 방법 중에 Spring은 기본적으로 프록시 객체 사용 방식을 선택합니다. (SpringBoot는 기본적으로 바이트 코드 생성 방식 사용)

   - 원리는 아래 코드와 같습니다. 프록시 객체로 우리가 만든 메서드를 한번 감싸서, 메서드 위 아래로 코드를 삽입합니다.

   ```java
      public class BooksProxy {
      private final Books books;
      private final TransactonManager manager = TransactionManager.getInstance();
      
      public BooksProxy(Books books) {
         this.books = books;
      }
      
      public void addBook(String bookName) {
         try {
            manager.begin();
            books.addBook(bookName);
            manager.commit();
         } catch (Exception e) {
            manager.rollback();
         }
      }
      }
   ```
   - 위와 같은 코드로 인해 우리가 BookImpl클래스를 사용할 때, 스프링이 제공하는 BookProxy 객체를 사용하게 되며, 프록시 객체가 제공하는 addBook 메서드를 사용해야만 트랜잭션 처리가 수행되게 됩니다.

   - **@Transactional이 수행되지 않은 이유**
      - BooksProxy 가 addBooks 메서드를 수행하면, 아래와 같은 순서로 작동됩니다. 
      - `BookProxy::addBooks -> BooksImpl::addBook`

      - 즉, **프록시 객체가 아닌 실제 BookImpl 객체의 함수를 호출하게 되므로 해당 메서드는 트랜잭션으로 감싸지지 않은 상태**로 @Transactional 어노테이션 기능이 수행되지 않는 것입니다.

   - **해결 방법**
   - 1. @Transactional 어노테이션 메서드는 클래스 내부적으로 사용하지 말고, 밖에서 사용합니다. (권장)
   - 2. 굳이 내부적으로 사용하려면, 자기 자신의 Proxy 객체를 사용하여 처리합니다. (아래 코드 참조)   
   
   ```java
      @Service
   public class BooksImpl implements Books {
   @Autowired
   private Books self;
   
   public void addBooks(List<String> bookNames) {
      bookNames.forEach(bookName -> self.addBook(bookName)); // this 가 아닌 변수 self 로
   }
   
   @Transactional
   public void addBook(String bookName) {
      Book book = new Book(bookName);
      bookRepository.save(book);
      book.setFlag(true);
   }
   }
   ```
   - 위 코드는 Books 인터페이스를 이용하여 BooksProxy 인스턴스를 주입할 수 있도록 유도합니다.
   - 그 후, 프록시 객체의 addBook 메서드 사용을 통해 @Transactional 어노테이션 기능을 사용할 수 있게 합니다.

#### 사진 & 내용 출처

https://steady-coding.tistory.com/583

https://velog.io/@chullll/Transactional-%EA%B3%BC-PROXY

https://velog.io/@ddongh1122/Spring-Transactional-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%82%B4%EB%B6%80-%ED%98%B8%EC%B6%9C-%EB%AF%B8%EC%9E%91%EB%8F%99-%EC%9D%B4%EC%8A%88
