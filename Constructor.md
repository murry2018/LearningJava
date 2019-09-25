# 생성자 이모저모

## 명시적 생성자

생성자는 객체를 생성하는 과정에서 호출된다. 스펙상, 자바 생성자는 메서드가 아니다. 명시적 생성자는 코드 중복을 피하기 위한 syntactic sugar에 불과하므로 생성자와 같은 Rule을 적용받는다.

명시적 생성자로는 `this()`와 `super()`를 사용할 수 있다. `this()`는 현재 클래스를, `super()`은 부모 클래스를 가리킨다.

명시적 생성자 호출은 다음과 같은 제약사항을 갖는다.

- 명시적으로 생성자를 호출할 때는 반드시 생성자의 첫번째 문장으로 와야 한다.
- 생성자 인자로 현재 객체의 메소드나 필드를 참조할 수 없다. 객체 생성 중에는 객체가 존재하지 않기 때문이다.

## 기본 생성자

 별도의 생성자를 만들지 않을 경우에만, 자바는 인자를 갖지 않고 아무것도 하지 않는 기본 생성자를 만든다. 별도의 생성자를 만들지 않을 경우에만 기본생성자가 만들어지는 이유는 인자 없이 생성되는 것이 부적절한 클래스가 종종 있기 때문이다.

## non-public 생성자

생성자 역시 접근 제한자를 가질 수 있으며, 기본적으로 `package` 접근 제한자를 부여받는다. 이렇게 하면, 다른 패키지에서 이 클래스에 접근해 임의로 객체를 생성하는 것을 막을 수 있다. 다른 패키지에서 이 클래스에 접근해 객체를 생성하도록 하고 싶다면 `public` 선언을 해야 한다. 

 한편, `private` 생성자는 종종 싱글톤 패턴을 구현하는데 이용된다.
 
```java
/** Singleton 패턴의 naive 구현 */
public class Singleton {
    private static instance = null;
    
    private Singleton() {
	// do something
    }

    /** singleton 객체를 가져온다 */
    public static getInstance() {
	/* 여러 스레드가 동시에 이 메서드에 접근한다면 instance가
	 * 여러번 초기화될 수 있다. 하지만 이 예제에서는
	 * thread-safety에 대해서는 다루지 않고 넘어간다.
	 */
	if (instance == null) {
	    instance = Singleton();
	}
	return instance;
    }
}
```