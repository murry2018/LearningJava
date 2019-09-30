# 메소드의 제한자

- 어노테이션(annotation)
- 접근 제한자(access modifier)
- `static` 키워드
- `final` 키워드 - 서브 클래스에 의해 override될 수 없다.
- `abstract` 키워드 - 서브 클래스에서의 구현을 요구한다.
- `synchronized` 키워드 - 동시성 제어와 관련한 기능을 수행한다.
- `native` 키워드
- `strictfp` 키워드 - 모든 부동소수점 연산이 엄격하게 처리된다.

추상 메서드<sub>abstract method</sub>는 static, final, synchronized,
native, 혹은 strictfp일 수 없다. native method는 abstract나 strictfp일
수 없다.

## native 메소드에 대하여

native 메소드는 자바가 아닌 다른 언어 (특히, C/C++)에서 작성된
메서드를 자바 클래스에서 사용하기 위해 사용한다. 함수의 본체는
네이티브 코드로 구현되어 있기 때문에, 아래의 \<예시\>와 같이 선언 시
메소드 몸체를 세미콜론으로 지정해야 한다. 네이티브 메소드는 자바 가상
머신을 제작한 사람들이 제공한 API를 사용해 구현할 수 있다. 그 중
JNI(Java Native Interface)는 C 프로그래머를 위한 표준 중 하나이다.

**예시**

``` java
public native int getCPUID();
```

