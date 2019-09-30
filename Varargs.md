# 가변인자 메소드

가변인자 메서드(혹은 Varargs 메서드)는 자바 5.0 버전부터 추가되었다.

## 같은 타입의 인자를 여러 개 받을 수 있다.

가변인자는 타입과 이름 사이에 생략 문자(`...`)를 표시함으로써 나타낸다.

**예시 1** 가변 인자 메서드 선언

```java
class Body {
    public void setOrbiters(Body... bodies) {
	// ... store the values
    }
}
```

위와 같이 선언한 가변인자 메서드는 다음과 같이 쓸 수 있다.

**예시 1.1** 가변 인자 메서드 사용

```java
Body sun = new Body(),
    earth = new Body(), moon = new Body();
earth.setOrbiters(moon);      // 한 개의 가변 인자
sun.setOrbiters(sun, earth);  // 두 개 이상의 가변 인자
moon.setOrbiters();           // 0개의 가변 인자
```

## Varargs의 타입은 배열이다.

가변 인자를 위한 또 다른 클래스가 있을 지 궁금할 수 있다. 가변 인자를
위한 특수한 타입이 있는 것은 아니다. 가변 인자 메서드는 가변 인자들을
배열로서 받는다.

또한, 자바에서는 매우 긴 목록의 가변 인자를 전달하기 위한 syntactic
sugar도 제공한다. 다음 \<예시 2\>에서 볼 수 있듯이, 배열을 직접 가변
인자로 넘길 수 있다.

**예시 2** 배열로 가변 인자 전달

```java
Body jupiter = new Body(),
    io = new Body(),
    europa = new Body(),
    callisto = new Body();

Body[] jupiterMoons = {io, europa, callisto};
jupiter.setOrbiters(jupiterMoons);
```

## 위험성

가변 인자를 다룰 때 몇 가지 상황에 조심히 대처해야 한다. 그 중 하나는
특히 `null`과 관련된 것이다. Varargs로 `null`을 전달하면, 가변 인자
개개의 오브젝트로서 `null`이 전달된 것인지, 0개의 가변인자를
전달하겠다는 의미인지 자바 컴파일러는 추정할 수 없다. 문법적 모호성을
피하기 위해서, 명시적인 타입 캐스팅을 해 주어야 한다.

**예시 3** 모호함을 피하기 위한 타입 캐스팅

```java
// (1) 문법적으로 모호함
moon.setOrbiters(null);

// (2) 개개의 인자로 전달
moon.setOrbiters((Body) null);

// (3) 가변인자 배열로서 전달
moon.setOrbiters((Body[]) null);
```

한 편, 메서드 오버로딩 시에도 모호함이 발생한다.

**예시 3.1** 오버로딩 시 발생하는 모호함

```java
public static void print(String title) {
    // ...
}
public static void print(String title, String... message) {
    // ...
}
public static void print(String... message) {
    // ...
}
```

물론 이렇게 모호한 경우에도 메소드 호출에는 우선순위가 있다. 어떤
경우에는 컴파일 에러 없이 무사히 돌아갈지도 모르고, 어떤 경우에는
"ambiguous invocation"라는 컴파일 오류를 발생시킬지도 모른다.

지금 당장은 그러한 상황을 정확히 파악할 수 있다고 해도, 나중에 코드를
볼 때(혹은 다른 사람이 코드를 볼 때), 코드의 의도를 명확히 해석하기는
어려울 것이다. 따라서 이런 식의 오버로딩을 할 때는 신중을 기해야 한다.

컴파일러의 빈 틈을 사람이 메꾸어야 한다는 점이 Hack 처럼 느껴질지
모르겠지만, Varargs는 어디까지나 프로그래머의 편의를 위한 기능이므로
어느 정도의 trade-off로써 받아들이자.
