# 예외 처리

예외(exception)란, 사용자의 잘못된 조작이나, 코딩으로 인해 발생하는 프로그램 오류이다. 예외가 발생하면 프로그램이 바로 종료되지만 ***예외처리(Exceotion Handling)***를 통해 프로그램을 종료하지 않고 정상적으로 프로그램이 동작하도록 할 수 있다.

- **일반 예외(Exception)** : 자바 소스를 컴파일 하는 과정에서 예외 처리 검사
- **실행 예외(Runtime Exception)** : 컴파일 하는 과정에서 예외 처리 코드를 검사하지 않는 예외

모든 예외 클래스는 `java.lang.Exception` 클래스를 상속 받는다.

<br>

## *실행 예외*

실행 예외는 자바 컴파일러가 체크를 하지 않기 때문에 개발자의 경험에 의해서 예외 처리 코드를 삽입해야 한다.

<br>

### NullPointerException

객체 참조가 없는 상태, 즉 `null` 값을 갖는 참조 변수로 객체 접근 연산자인 도트(.)를 사용했을 때 발생한다.

```java
String str = null;
System.out.println(str.length());	// java.lang.NullPointerException
```

<br>

### ArrayIndexOutOfBoundsException

배열에서 인덱스 범위를 초과하여 사용할 경우 발생한다.

```java
int array[] = new int[] {1,2,3,4,5};
System.out.println(array[5] = 5);
```

<br>

### NumberFormatException

문자열이 숫자로 변환될 수 없을 때, 문자열을 숫자로 변환하려한다면 발생한다.

<br>

### ClassCastException

타입 변환은 상위 클래스와 하위 클래스, 또는 인터페이스와 구현객체 사이에 이루어지는데, 억지로 타입 변환을 하게 되면 `ClassCastException`이 발생한다.

<br>

## *예외 처리 코드*

프로그램에서 예외가 발생했을 경우 프로그램의 갑작스러운 종료를 막고, 정상 실행을 유지할 수 있도록 처리하는 코드로 `try-catch-finally` 블록을 이용한다.

```java
try {
    // 예외 발생 가능 코드
} catch(예외클래스 e) {
    // 예외 처리 ( try 블록에서 예외가 발생하면 실행)
    // 만약 예외클래스에 작성한 타입의 예외가 try블록에서 발생할 경우 catch 구문을 실행한다.
} finally {
    // 항상 실행 (생략 가능)
}
```

`ArrayIndexOutOfBoundsException` 예외가 발생할 경우 예외를 처리해주는 코드

```java
public class HelloJava {
    public static void main(String[] args) {
        int array[] = new int[] {1,2,3,4,5};
        try {
            array[array.length] = 20;
        } catch(ArrayIndexOutOfBoundsException e ) {
            System.out.println("배열의 인덱스 값을 초과했습니다.");
            array[array.length-1] = 20;
        } finally {
            System.out.println("값을 출력합니다.");
            for(int i : array) {
                System.out.print(i + " ");
            }
        }

    }
}
```

<br>

## *예외 종류에 따른 처리 코드*

### 다중 catch

`try` 블록 내부에 여러 종류의 예외가 발생할 경우 다중 `catch` 블록을 작성한다. 

```java
try {
    
} catch (ClassCastException e) {
    // try 블록에서 ClassCastException이 발생할 겨웅 실행
} catch (NullPointerException e) {
    // try 블록에서 NullPointerException이 발생할 경우 실행
}
```

만약 `try` 블록에서 `ClassCastException`이 발생하면 즉시 실행을 멈추고 첫 번째 `catch` 블록으로 이동한다. 따라서 `try` 블록에 여러 종류의 예외가 있더라도 가장 먼저 발생하는 예외에 대한 단 하나의 `catch` 블록이 실행된다.

<br>

### catch 순서

다중 `catch` 블록을 작성할 때, 상위 예외 클래스가 하위 예외 클래스보다 아래쪽에 위치해야 한다.

<br>

### 멀티 catch

하나의 `catch` 블록에서 여러 개의 예외를 처리하는 방법이다.

```java
try {
    
} catch (에러클래스1 | 에러클래스2 e) {
    // 에러클래스1또는 에러클래스2 발생시 동일하게 처리
} catch (에러클래스3 ... ) {
    // 에러클래스3 발생시 이 구문 실행
}
```

<br>

### 예외 떠넘기기

`throws` 키워드는 메소드 선언부 끝에 작성되어 메소드에서 처리하지 않은 예외를 호출한 곳으로 떠넘기는 역할을 한다. `throws` 키워드 뒤에는 떠넘길 예외 클래스를 쉼표로 구분해서 나열해준다.

```java
리턴타입 메소드명(parm,... ) throws 예외클래스1, 예외클래스2, ... {
}
```

`throws` 키워드가 붙어있는 메소드는 반드시 `try` 블록 내부에서 호출되어야 한다.

```java
public class Parent {
    public void method(int[] array) throws ArrayIndexOutOfBoundsException {
        array[5] = 20;
    }
}
```

호출한 곳에서 예외를 처리한다.

```java
public class HelloJava {
    public static void main(String[] args) {
        Parent parent = new Parent();
        try {
            parent.method(new int[]{1, 2, 3, 4, 5});
        } catch(ArrayIndexOutOfBoundsException e) {
            System.out.println("배열의 범위를 초과했습니다.");
        }
    }
}
```

<br>

## *사용자 정의 예외와 예외 발생*

사용자가 직접 예외를 정의하여 만들 수 있다.

<br>

### 사용자 정의 예외 클래스 선언

사용자 정의 예외 클래스는 컴파일러가 체크하는 **일반 예외** 또는 컴파일러가 체크하지 않는 **실행 예외** 둘 다 선언할 수 있다. 일반 예외로 선언할 경우 `Exception`을 상속하고 , 실행 예외로 선언할 경우 `RuntimeException`을 상속한다.

```java
public class XXXException extends [Exception | RuntimeException] {
    // 기본 생성자
    public XXXException() { }
    // 예외 메시지를 전달하기 위한 매개 변수를 갖는 생성자
    public XXXException(String message) { super(message); }
}
```

<br>

### 예외 발생시키기

예외를 고의적으로 발생시키는 방법은 다음과 같다.

```java
throw new XXXException();
throw new XXXException("메세지");
```

<br>

### 예외 정보 얻기

`getMessage()` 메소드를 이용하여 예외 메시지를 `String` 으로 변수에 할당할 수 있고, `printStackTrace()` 메소드를 이용하여 예외 발상 코드를 추적해서 콘솔에 출력할 수 있다.

<br>

<br>

<br>

___

출처 : 한빛미디어 < 이것이 자바다> 신용권
