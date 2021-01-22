## 중첩 클래스 & 중첩 인터페이스

만약 클래스가 특정 클래스와 관계를 지을 경우에는 관계 클래스를 클래스 내부에 선언하는 것이 좋다. 이 때, 중첩 클래스를 사용하는데, 클래스 내부에 선언된 클래스를 **중첩 클래스** 라고 한다. 

```java
class OutClass {
    class NestedClass{
        
    }
}
```

클래스 안에 선언된 인터페이스는 **중첩 인터페이스** 라고 한다.

```java
class OutClsas {
    interface NestedInterface {
        
    }
}
```

<br>

## *중첩 클래스*

- **멤버 클래스** : 클래스의 멤버로서 선언되는 중첩 클래스
  - 클래스나 객체가 사용 중이라면 언제든지 재사용 할 수 있다.
- **로컬 클래스** : 메소드 내부에서 선언되는 중첩 클래스
  - 메소드 실행 시에만 사용되고, 메소드가 종료되면 사라진다

```java
// 멤버 클래스
class OutClass{
 	class MemberClass { ... }   
}

// 로컬 클래스
class OutClass {
    void Method() {
        class LocalClass { ... }
    }
}
```

<br>

### 인스턴스 멤버 클래스

인스턴스 멤버 클래스는 `static` 없이 선언된 클래스로 정적 필드와 정적 메소드는 선언할 수 없다.

```java
class OutClass {
    class InstanceClass {
        int field1;
        static int field2;	// 불가능
        void method() {...}
        static void method() {...}	// 불가능
    }
}
```

`OutClass` 클래스 외부에서 인스턴스 멤버 클래스인 `InstanceClass`의 객체를 생성하려면 `OutClass`객체를 먼저 생성하고 `InstanceClass`객체를 생성해야 한다.

```java
OutClass outerclass = new OutClass();
OutClass.InstanceClass instanceClass = outclass.new InstanceClass();
instanceClass.field1; // 0
instanceClass.method();	// 메소드 실행
```

<br>

### 정적 멤버 클래스

`static` 키워드로 선언된 클래스이다.

```java
class OutClass {
    static class NestedClass {
        int field1 = 5;
        void method() { System.out.println("This is NestedClass's method") }
    }
}
```

정적 멤버 클레스인 `NestedClass` 의 객체를 생성하기 위해서는 `OutClass`의 객체를 생성할 필요가 없다.

```java
OutClass.NestedClass nestedClass = new OuterClass.NestedClass();
System.out.println(nestedClass.field1);	// 5
nestedClass.method1();	// "This is NestedClass's method"
```

<br>

#### 로컬 클래스

- 메소드 내에 선언된 중첩 클래스를 말한다.
- 로컬 클래스는 **접근제한자**와 `static`을 붙일 수 없다.
- 로컬 클래스 내부에는 인스턴스 필드와 메소드만 선언 가능하다.

```java
class OutClass {
    void method() {
        class LocalClass {
            LcalClass() { ... };	// 생성자
            int field1;
            static int fiedl2;	// 불가능 
            void method2 () { ... };
            static void method3 () { ... };	// 불가능
        }
        LocalClass localClass = new LocalClass();	// LocalClass 객체를 생성
        localClass.field1 = 5;
        localClass.method();
    }
}
```

<br>

## *중첩 클래스의 접근 제한*

### 바깥 필드와 메소드에서 사용 제한

- 인스턴스 멤버 클래스는 바깥 클래스의 인스턴스 필드의 초기값이나 인스턴스 메소드에서 객체를 생성할 수 있으나, 정적 필드의 초기값이나 정적 메소드에서는 객체를 생성할 수 없다.
- 정적 멤버 클래스는 모든 필드의 초기값이나 모든 메소드에서 객체를 생성할 수 있다.

<br>

### 멤버 클래스에서 사용 제한

- 인스턴스 멤버 클래스 안에서는 바깥 클래스의 모든 필드와 메소드에 접근 할 수 있다.
- 정적 멤버 클래스 안에서는 바깥 클래스의 정적 필드와 메소드에만 접근할 수 있고 인스턴스 필드와 메소드는 접근할 수 없다.

<br>

### 로컬 클래스에서 사용 제한

- 로컬 클래스 내부에서는 바깥 클래스의 필드나 메소드를 제한 없이 사용할 수 있다.
- 하지만 메소드의 매개 변수나 로컬 변수를 로컬 클래스에서 사용할 때 문제가 발생한다.
  - 로컬 클래스에서 사용 가능한 것은 `final`로 선언된 매개 변수와 로컬 변수뿐이다.
    - `final` 키워드를 생략해도 값을 수정할 수 없는 `final`의 특성을 갖는다.
      - `final` 키워드가 있을 때 : 로컬 클래스의 메소드 내부에 지역 변수로 복사
      - `final` 키워드가 없을 때 : 로컬 클래스의 필드로 복사

```java
void OutMethod(final int arg1, int arg2) {	// int arg1 : 로컬 변수로 복사, int arg2 : 필드로 복수
    final int var1 = 0;	// int var1 : 로컬 변수로 복사
    int var2 = 1;	// int var2 : 필드로 복사
    class LocalClass {
        void method() {
            int result = arg1 + arg2 + var1 + var2
        }
    }
}
```

즉, 로컬 클래스에서 사용된 매개 변수와 로컬 변수는 모두 `final` 특성을 갖는다.

```java
public class OutClass {
    public void method(int arg) {
        int localVal = 30;
        arg = 10;	// X (fianl이기 때문에 값 변경 X)
        localVal = 50;	// X (final이기 때문에 값 변경 X)
        
        class InClass {
            public void innerMethod() {
                int result = arg + localVal;	// 매개 변수 arg와 로컬 변수 localVal(fianl 특성 가짐)
            }
        }
    }
}
```

<br>

### 중첩 클래스에서 바깥 클래스 참조 얻기

- 중첩 클래스에서 `this` 키워드를 사용하면 바깥 클래스의 객체가 아니라, 중첩 클래스의 객체를 참조하게 된다.
- 만약 중첩 클래스 내부에서 바깥 클래스의 객체 참조를 얻으려면 바깥 클래스의 이름을 `this` 앞에 붙여준다.

```java
바깥 클래스.this.필드(메소드());
```

```java
public class OuterClass {
    String outerString = "This is OuterStringField";
    void method1() {
        class NestedClass {
            final String nestedString = "This is NestedStringField";
            public void innerMethod() {
                System.out.println(this.nestedString);
                System.out.println(OuterClass.this.outerString);
            }
        }
        NestedClass nestedClass = new NestedClass();
        nestedClass.innerMethod();
    }
}
```

`OuterClass`는 바깥 클래스이고 `NestedClass`는 `method1()` 메소드 안에 존재하는 로컬중첩클래스이다. `method1()`을 실행하면 `NestedClass` 객체를 생성하여 `innerMethod()` 메소드를 실행하도록 했다.

```java
public class Example {
    public static void main(String[] args) {
        OuterClass outerClass = new OuterClass();	// This is NestedStringField
        outerClass.method1();	// This is OuterStringField
    }
}
```

<br>

## *중첩 인터페이스*

중첩 인터페이스는 클래스의 멤버로 선언된 인터페이스이다. 해당 클래스와 긴밀한 관계를 맺는 구현 클래스를 만들기 위해 사용된다.

<br>

## *익명 객체*

이름이 없는 객체를 말한다. 클래스를 상속하거나 인터페이스를 구현해야만 생상할 수 있다.

<br>

### 익명 자식 객체 생성

자식 클래스가 재사용되지 않고, 오로지 해당 필드와 변수의 초기값으로만 사용할 경우라면 익명 자식 객체를 생성해서 초기값으로 대입하는게 좋다.

```java
부모클래스 [필드|변수] = new 부모클래스(param, ... ) {
    // 필드
    // 메소드
    // << 생성자는 선언할 수 없다 >>
};
```

필드를 선언할 때 초기값으로 익명 객체를 생성해서 대입

```java
class A {
    Parent field = new Parent() {	// A 클래스의 필드 선언
       int childField;
       void childMethod() { }
       @Override
       void parentMethod() { }
    };
}
```

메소드 내에서 로컬 변수를 선언할 때 초기값으로 익명 자식 객체를 생성해서 대입

```java
class A {
    void method() {
        Parent localVar = new Parent() {
            int childField;
            void childMethod() { }
            @Override
            void parentMethod() { }
        }
    }
}
```

메소드의 매개 변수가 부모 타입일 경우 메소드 호출 코드에서 익명 자식 객체를 생성해서 매개값으로 대입할 수도 있다.

```java
class A {
    void method1(Parent parent) { }
    
    void method2() {
        void method1(
        new Parent() {
            int childField;
            void childMethod() { }
            @Override
            void parentMethod() { }
        }
      );
    }
}
```

익명 자식 객체는 부모 타입 변수에 대입되므로 부모 타입에 선언된 것만 사용할 수 있다. 그래서 익명 자식 객체에 새롭게 정의된 필드와 메소드는 익명 자식 객체 내부에서만 사용 가능하다.

<br>

### 익명 구현 객체 생성

인터페이스 타입으로 필드나 변수를 선언하고, 구현 객체를 초기값으로 대입하는 경우에, 만약 구현 객체가 해당 필드와 변수의 초기값으로만 사용하는 경우라면 익명 구현 객체를 사용하는 것이 좋다.

```java
인터페이스 [필드|변수] = new 인터페이스() {
    // 실체 메소드
    // 필드
    // 메소드
}
```

`{}`에는 인터페이스에 선언된 모든 추상 메소드들의 실체 메소드를 작성해야 한다. 필드와 메소드는 선언할 수 있지만, 실체 메소드에서만 사용이 가능하다.

```java
class Outter {
    AnnoInterface field = new AnnoInterface() {	// Outter 클래스의 필드
        @Override
        void interMethod() { }	// AnnoInterface 인터페이스의 추상메소드의 실체 메소드
    };
}
```

```java
class Outter { 
    void method() {
        AnnoInterface locarVar = new AnnoInterface() {	// 로컬 변수
            @Override
            void interMethod() { }	
        };
    }
}
```

```java
class Outter {
    void method(AnnoInterface annoInterface) { }
    void method2() {
        method(new AnnoInterface() {
            void interMethod()
        })
    }
}
```

<br>

### 익명 객체의 로컬 변수 사용

익명 객체 내부에서 메소드의 매개 변수나 로컬 변수를 사용할 경우, 이 변수들은 `fianl` 특성을 가진다. 앞서 말한 로컬클래스에서의 사용제한과 같다. 즉, 익명 객체에서 사용된 매개 변수와 로컬 변수는 모두 `final` 특성을 가진다.

<br>

<br>

<br>

___

출처 : 한빛미디어 < 이것이 자바다> 신용권









