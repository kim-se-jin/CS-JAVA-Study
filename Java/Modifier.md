# Modifier
- 제어자란(modifier) ? 
   - 클래스, 변수, 메서드의 선언부에 사용되어 부가적인 의미를 부여합니다.
   - 접근제어자 : public, protected, default, private
   - 그 외 제어자 : static, final, abstract, native, transient, synchronized, volatile .. 
- 하나의 대상에 여러 개의 제어자를 조합해서 사용할 수 있으나, 접근제어자는 단 하나만 사용할 수 있습니다.

- 1. static :  메모리를 공유하여 사용
- '클래스의' 또는 '공통적인' 의미를 가지고 있다.
- static이 붙은 멤버변수와 메서드, 초기화 블럭은 인스턴스를 생성하지 않고도 사용할 수 있다.
   - static 멤버변수
      - 모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다.
      - 클래스변수는 인스턴스를 생성하지 않고도 사용가능하다.
      - 클래스가 메모리에 로드될 때 생성된다.

   - static 메서드
      - 인스턴스를 생성하지 않고도 호출이 가능한 static 메서드가 된다.
      - static메서드 내에서는 인스턴스멤버들을 직접 사용할 수 없다. 

- 2. final : 해당 변수는 값이 저장되면 최종적인 값이 되므로, 수정이 불가능
- '마지막의' 또는 '변경될 수 없는' 의미를 가지고 있다. 
    - final 클래스 
        - 변경 될 수 없는 클래스, 확장될 수 없는 클래스가 된다.
        - 다른 클래스의 조상이 될 수 없다.
    - final 메서드
        - 변경 될 수 없는 메서드, 오버라이딩을 통해 재정의 될 수 없다.
    - final 멤버변수, final 지역 변수
        - 변경 할 수 없는 상수가 된다.
- final이 붙은 변수는 상수이므로 보통은 선언과 초기화를 동시에 하지만, 인스턴스변수의 경우 생성자에서 초기화 할 수 있다.

- Static Final
   - 두개를 합쳐서 생각해보면 고정되어 최종적으로 사용된다고 보면된다.
   - 즉, 클래스 자체에 존재하는 단 하나의 상수이다.(클래스자체로 존재하여 접근가능하고 불변하다)
   - 따라서 클래스의 선언과 동시에 반드시 초기화가 필요한 클래스 상수이다.

### Q) 메소드 parameter 에 final 에 붙이는 경우를 어떻게 생각하시는지 설명해주세요.
- 매개변수가 변경 불가능한 상황을 의미합니다.
- 매개변수에 final 을 붙이면, 넘어온 매개변수를 변경하지 못하도록 강제하므로 매개변수를 변경하지 말아야 하는 경우, 이를 명시하고 싶을 때 사용하면 적합할 것이라고 판단합니다.

- 아래 코드는 컴파일 에러 (The final local variable website cannot be assigned. It must be blank and not using a compound assignment ) 가 발생합니다. 
- 이와 같이 넘어온 매개변수의 변경 방지를 강제할 때 사용한다면 유용할 것입니다. 

```java
	 static class FinalParameterTest{
		 
		public void show(final String website){
			website = "java.com"; // 변경하려고 시도라면 
			System.out.println("website = " + website);
		}
	}
	
	public static void main(String args[]){
		//creating object of FinalParameterTest Class
		FinalParameterTest obj = new FinalParameterTest();
		obj.show("w3spoint.com");
	}
```

![image](https://user-images.githubusercontent.com/76711238/236809825-4ba53339-6f14-4d5c-9821-ded4140f76e2.png)


#### 사진 & 내용 출처
https://guccin.tistory.com/155

https://stackoverflow.com/questions/2236599/final-keyword-in-method-parameters
