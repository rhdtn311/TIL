# Optional 클래스



## *java.util.Optional<T> 클래스*

- `T` 타입의 객체를 포장해 주는 **래퍼 클래스** 이다.
- `Optional` 인스턴스는 모든 타입의 참조 변수를 저장할 수 있다.
- 예상치 못한 `NullPointerException` 예외를 제공되는 메소드로 회피할 수 있다.
  - 복잡한 조건문 없이도 널값으로 인해 발생하는 예외 처리 가능

<br>

## *Optinal 객체의 생성*

`of()` 메소드나 `ofNullable()` 메소드를 사용하여 `Optinal` 객체를 생성할 수 있다.

- `of()` : `null`이 아닌 명시된 값을 가지는 `Optional` 객체를 반환한다.
  - `of()` 메소드를 통해 생성된 `Optional` 객체에 `null`이 저장되면 `NullPointerException`예외가 발생한다.
- `ofNullable()` : 명시된 값이 `null`이 아니면 명시된 값을 가지는 `Optional` 객체를 반환하며, 명시된 값이 `null`이라면, 비어있는 `Optional` 객체를 반환한다.
  - 참조변수의 값이 `null`이 될 가능성이 있다면, `ofNullable()` 메소드를 사용하여 `Optional` 객체를 생성한다.

```java
Optional<String> opt = Optional.ofNullable("자바 Optional 객체");
System.out.println(opt.get());	// 자바 Optional 객체
```

<br>

## *Optinal 객체에 접근*

- `get()` 메소드를 사용하여 `Optional` 객체에 저장된 값에 접근할 수 있다.
- `Optional` 객체에 저장된 값이 `null` 이면, `NoSuchElementException` 예외가 발생한다.
- `get()` 메소드를 호출하기 전에 `isPresent()` 메소드를 사용하여 `Optional` 객체에 저장된 값이 `null`인지 판단한다.

```java
Optional<String> opt = Optional.ofNullable("자바 Optional 객체");
if(opt.isPresent()) {
    System.out.println(opt.get());
}
```

<br>

<br>

<br>

___

참고 : http://www.tcpschool.com/java/java_stream_optional





