# 인터페이스(Interface)

## *인터페이스의 역할*

- 인터페이스는 개발 코드와 객체가 서로 통신하는 접점 역할을 한다.
- 개발 코드를 수정하지 않고 사용하는 객체를 변경할 수 있도록 하기 위해 인터페이스를 사용한다.

<br>

## *인터페이스 선언*

```java
[public] interface 인터페이스명 { ... }
```

- 인터페이스는 상수와 메소드만을 구성 멤버로 가진다
- 인터페이스는 객체로 생성할 수 없기 때문에 생성자를 가지지 않는다.

```java
interface 인터페이스명 {
    // 상수
    타입 상수명 = 값;
    // 추상 메소드
    타입 메소드명(매개변수, ... );
    // 디폴트 메소드
    default 타입 메소드명(매개변수, ... ); { ... }
    // 정적 메소드
    static 타입 메소드명(매개변수, ... ) { ... }
}
```

- **상수 필드**
  - 인터페이스의 필드는 상수 필드만이 선언 가능하다.
  - 반드시 초기값을 대입해야한다.
- **추상 메소드**
  - 매개값과 리턴 타입만 정의한다.
- **디폴트 메소드**
  - 구현 객체가 가지고 있는 인스턴스 메소드이다.
- **정적 메소드**
  - 객체가 없어도 인터페이스만으로 호출이 가능하다.

<br>

### 상수 필드 선언

인터페이스의 필드는 상수 필드만 선언 가능하다.

```java
// public, static, final을 생략하더라도 컴파일 과정에서 자동 생성됌
[ public static final ] 타입 상수명 = 값;
```

<br>

### 추상 메소드 선언

인터페이스를 통해 호출된 메소드는 최종적으로 객체에서 실행되기 때문에 인터페이스의 메소드는 추상 메소드로 선언한다.

```java
// public abstract를 생략하더라도 컴파일 과정에서 자동 생성됌.
[public abstract] 리턴타입 메소드명(매개변수, ... );
```

<br>

### 디폴트 메소드 선언

인터페이스를 확장해서 새로운 기능을 추가할 수 있는 메소드이다.

```java
// public을 생략하더라도 컴파일 과정에서 자동 생성됌.
[public] default 리턴타입 메소드명(매개변수, ... ) { ... }
```

<br>

### 정적 메소드 선언

```java
// public을 생략하더라도 컴파일 과정에서 자동 생성됌.
[public] static 리턴타입 메소드명(매개변수, ... ) { ... }
```

<br>

##  *인터페이스 구현*

코드가 인터페이스 메소드를 호출하면 인터페이스는 객체의 메소드를 호출한다. 객체는 인터페이스에서 정의된 추상 메소드와 동일한 메소드 이름, 매개 타입, 리턴 타입을 가진 실체 메소드를 가지고 있어야 한다. 이런 객체를 인터페이스의 **구현(implement) 객체**라고 하고, 구현 객체를 생성하는 클래스를 구현 클래스 라고 한다.

<br>

### 구현 클래스

인터페이스 타입으로 사용할 수 있다는 표시로 `implements`키워드를 추가한다.

```java
public class 클래스명 implements 인터페이스명 {
    // 구현 코드
}
```

그리고 인터페이스에 선언된 추상 메소드의 실체 메소드를 선언해야 한다.

```java
// Overwatch 인터페이스
public interface Overwatch {	
    // 상수
    static final int DAMAGE = 10;	
	
    // 추상 메소드
    public void leftClick();
    public void rightClick();
    public int damageOfLeftClick();
}

// Overwatch 인터페이스를 상속받은 McCree 클래스
public class McCree implements Overwatch {

    static final int MCCREE_BASIC_DAMAGE = 40;

    // 인터페이스의 추상 메서드를 오버라이딩
    @Override
    public void leftClick() {
        System.out.println("피스키퍼");
    }

    @Override
    public void rightClick() {
        System.out.println("연속 피스키퍼");
    }

    @Override
    public int damageOfLeftClick() {
        return DAMAGE * MCCREE_BASIC_DAMAGE;
    }
}

// Overwatch 인터페이스를 상속받은 D_VA 클래스
public class D_VA implements Overwatch {
    static final int D_VA_BASIC_DAMAGE = 10;

    // 인터페이스의 추상 메소드를 오버라이딩
    @Override
    public void leftClick() {
        System.out.println("융합포");
    }

    @Override
    public void rightClick() {
        System.out.println("방어 매트릭스");
    }

    @Override
    public int damageOfLeftClick() {
        return D_VA_BASIC_DAMAGE * DAMAGE;
    }
}

```

<br>

### 익명 구현 객체

- **익명 구현 객체** : 소스 파일을 만들지 않고도 구현 객체를 만들 수 있다.

```java
인터페이스 변수 = new 인터페이스() {
    // 인터페이스에 선언된 추상 메소드의 실체 메소드 선언
};	// 세미콜론이 와야됌
```

익명 구현 객체는 이름이 없고 `{}` 안에는 인터페이스에 선언된 모든 추상 메소드들의 실체 메소드를 작성 해야 한다. 필드와 메소드를 선언할 수 있지만 익명 함수 안에서만 사용 가능하다.

```java
public class Example {
    public static void main(String[] args) {
        Champion champion = new Champion() {
            public void leftClick() { 실행문 };
            public void rightClick() { 실행문 };
            public void leftClickDamage(int damage) { 실행문 };
        }
    }
}
```

<br>

### 다중 인터페이스 구현 클래스

하나의 객체는 다수의 인터페이스 타입으로 사용할 수 있다. 두 인터페이스가 하나의 객체의 메소드를 호출할 수 있으려면 객체는 두 인터페이스를 모두 구현해야 한다. 하나라도 없으면 추상 클래스로 선언해야 한다.

```java
public class 구현클래스명 implements 인터페이스1,  인터페이스2 {
    // 인터페이스1에 선언된 추상 메소드의 실체 메소드
    // 인터페이스2에 선언된 추상 메소드의 실체 메소드
}
```

<br>

## *인터페이스 사용*

인터페이스로 객체를 사용하려면 인터페이스 변수를 선언하고 구현 객체를 대입해야 한다.

```java
인터페이스 변수 = 구현 객체;
// 인터페이스 변수는 구현 객체의 번지를 저장 ( 참조 타입 )

// ex
Overwatch d_va = new D_VA();

d_va.leftClick();	// "융합포"
d_va.rightClick();	// "방어 매트릭스"
System.out.println(d_va.damageOfLeftClick());	// 100
```

<br>

### 디폴트 메소드 사용

디폴트 메소드는 인터페이스에 선언된다. 하지만 디폴트 메소드는 추상메소드가 아니라 인스턴스 메소드이다. 따라서 구현 객체가 따로 있어야 사용할 수 있다.  만약 앞서 선언한 `Overwatch` 인터페이스에 다음과 같은 디폴트메소드가 있다고 하면

```java
public interface Overwatch {
    public default void delete() {
        System.out.println("캐릭터를 삭제합니다.")
    }
}
```

다음과 같이 객체를 만들어서 사용할 수 있다.

```java
Overwatch d_va = new D_VA();	// Overwatch 인터페이스를 상속받는 클래스의 객체를 생성하여 사용

d_va.delete();	
```

디폴트 메소드는 인터페이스의 모든 구현 객체가 기본적으로 가지고 있어야할 메소드이다. 디폴트 메소드는 **오버라이딩** 할 수 있다.

<br>

### 정적 메소드 사용

인터페이스의 정적 메소드는 바로 호출 가능하다.

```java
public interface Overwatch() {
    public static void change() {
        System.out.println("캐릭터를 변경합니다.")
    }
}

public class Example() {
    public class void main(String[] args) {
        Overwatch.change();	// "캐릭터를 변경합니다.""
    }
}
```

<br>

## 타입 변환과 다형성

- 인터페이스 타입에 어떤 구현 객체를 대입하느냐에 따라 실행 결과가 달라진다. 
- 인터페이스는 메소드의 매개 변수로 많이 사용되는데, 인터페이스 타입으로 매개 변수를 선언하면 메소드 호출 시 매개값으로 여러 가지 종류의 구현 객체를 줄 수 있기 때문에 메소드 실행 결과가 다양하게 나온다. 

<br>

### 자동 타입 변환

- 구현 객체가 인터페이스 타입으로 변환되는 것

```java
인터페이스 변수 = 구현객체;	// 자동 타입 변환
```

<br>

### 필드의 다형성

```java
public interface Champion {
    public abstract String ultSkill();
}
```

위와 같이 `ultSkill()` 추상 메소드를 가지고 있는 `Champion` 인터페이스를 선언하였다.

``` java
public class Ezreal implements Champion {
    @Override
    public String ultSkill() {
        return "정조준 일격";
    }
}

public class Jhin implements Champion {
    @Override
    public String ultSkill() {
        return "커튼 콜";
    }
}
```

인터페이스 `Champion`의 구현 클래스인 `Ezreal`과 `Jhin`을 작성하였다. `Ezreal`과 `Jhin`은 `Champion`의 추상메소드인 `ultSkill()`을 오버라이딩하였다.

```java
public class MakeChampion() {
    // 필드
    Champion currentChampion = new Ezreal();	// 자동 타입 변환
    
    // 메소드
    public void useSkill() {
        System.out.println( currentChampion.ultSkill() + " 스킬을 사용합니다. ");
    }
}
```

`MakeChampion()` 클래스를 생성하여 그 클래스의 필드값으로 `Champion` 인터페이스를 선언하고 그 인터페이스의 구현 객체인 `Ezreal` 객체를 대입하였다. 그 과정에서 자동 타입 변환이 일어났다. 그리고 메소드로 `useSkill()` 을 생성하여 `Champion` 인터페이스에 선언된 `ultSkill()` 메소드를 호출하였다. 위 상태에서는 `currentChampion`이 `Ezreal` 객체이기 때문에 `Ezreal.ultSkill`인 "정조준 일격" 값을 가질 것이다.

```java
public class Example {
    public static void main(String[] args) {
	    MakeChampion champion = new MakeChampion();
        champion.useSkill();	// "정조준 일격 스킬을 사용합니다."
        
        champion.currentChampion = new Jhin();
        champion.useSkill();	// "커튼 콜 스킬을 사용합니다."
    }
}
```

`MakeChampion` 타입의 변수 `champion`에 `MakeChampion` 클래스를 참조하는 객체를 대입하였다. `MakeChampion` 객체는 필드 값으로 `Ezreal` 객체를 갖고있고,  `useSkill()` 메소드를 호출하면 `Ezreal`의 `ultSkill()`의 값이 리턴되고, `champion`의 `currentChampion` 필드를 `Jhin` 객체로 바꾸면 `Jhin` 의 `ultSkill()` 의 값이 리턴되어 `useSkill()` 메소드를 변경할 필요 없이 필드 값을 바꿈으로써 다양한 실행 결과를 얻을 수 있게된다.

<br>

### 인터페이스 배열로 구현 객체 관리

이전 예제에서 만약 `MakeChampion` 클래스에서 여러 인터페이스 객체를 필드값으로 갖는다면 다음과 같이 배열로 나타낼 수 있다.

```java
public class MakeChampion {
    Champion champions[] = {	// 필드를 배열로 선언
        new Ezreal(),
        new Jhin()
    };
    
    public void useSkill() {
        for (Champion champ : champions) {
            System.out.println(champ.ultSkill() + " 스킬을 사용합니다.");
        }
    }
}
```

<br>

### 매개 변수의 다형성

매개값을 다양하게 하기 위해서 매개 변수를 인터페이스 타입으로 선언하고 구현객체로 호출한다.

```java
public class Program {
    public void occurError(Machine muchine) {	// Machine는 인터페이스
        machine.format();	
    }
}
```

`Program` 클래스 안에 `occurError` 라는 메소드가 정의되어 있는데, 그 메소드의 매개값은 `Machine` 타입이고, `Machine`은 인터페이스이다.

```java
public interface Machine {
    public void format();
}
```

그리고 `Computer`가 `Machine`의 구현 클래스라면 `Computer` 의 객체가 `occurError`의 매개값으로 사용될 수 있다. 

```java
public class Computer implements Machine {
	public void format() {
        System.out.println("컴퓨터를 포멧합니다.");
    }
}
```

```java
public class Mobile implements Machine {
    public void format() {
        System.out.println("스마트폰을 포멧합니다.");
    }
}
```

이제 매개변수의 다형성을 이용하여 `Program` 의 `occurError` 메소드를 다양하게 호출할 수 있다.

```java
public class Example {
    public static void main(String[] args) {
        Program program = new Program();
   	    Computer computer = new Computer();
        
        program.occurError(computer);	// "컴퓨터를 포멧합니다."
        // Mobile mobile = new Mobile(); 이기 때문에 대체 가능
        program.occurError(new Mobile());	// "스마트폰을 포멧합니다."
    }
}
```

<br>

### 강제 타입 변환

구현 객체가 인터페이스 타입으로 자동 변환하면, 인터페이스에 선언된 메소드만 사용 가능하다.  하지만 구현클래스에만 선언된 멤버를 사용해야 할 경우 **강제 타입 변환** 을 해서 구현 클래스의 필드와 메소드를 사용할 수 있다.

```java
구현클래스 변수 = (구현클래스) 인터페이스 변수;
```

```java
public interface Machine {
    public abstract void occurError();
}

public class Computer implements Machine {
    public void occurError() { ... }; 
    public void turnOn() { ... };
}

public class Example {
    public static void main(String[] args) {
        Machine machine = new Compter();
        
        machine.occurError();	// 호출 가능
        machine.turnOn();	// 호출 불가능
        
        Computer computer = (Computer) machine;	// 강제 타입 변환
        
        computer.occurError();	// 호출 가능
        computer.turnOn();	// 호출 가능
    }
}
```

<br>

### 객체 타입 확인 (instance of)

강제 타입 변환은 구현 객체가 인터페이스 타입으로 변환되어 있는 상태에서 가능하다. 그렇기 때문에 강제 타입 변환을 하기 전에 해당 구현 객체가 인터페이스 타입으로 변환되어 있는지 확인할 필요가 있다. 그것을 위해 `instance of`를 사용할 수 있다.

```java
        Computer computer = new Computer();	// Computer 클래스의 객체
        computer.format();	// 호출 가능
        computer.turnOn();	// 호출 가능

        Machine machine = new Computer();	// Machine 인터페이스의 구현 객체
        machine.format();	// 오버라이딩 했으므로 호출 가능
        // machine.turnOn(); // 인터페이스에 없는 추상클래스이므로 < 오류 발생! >

        if (machine instanceof Computer) {	// Machine 인터페이스의 타입 machine이 Computer의 객체라면
            Computer com = (Computer) machine;	// 강제 타입 변환
            com.turnOn();	// 호출 가능
        }
```

<br>

## *인터페이스 상속*

인터페이스는 다른 인터페이스를 상속할 수 있다. 인터페이스 끼리의 상속은 다중 상속이 가능하다.

```java
public interface 하위인터페이스 extends 상위인터페이스1, 상위인터페이스2 { ... }
```

하위 인터페이스를 구현하는 구현 클래스는 상위 인터페이스의 모든 추상 메소드에 대한 실체 메소드를 가지고 있어야 한다. 그렇기 때문에 하위 인터페이스의 타입의 객체는 상위 인터페이스 타입으로 변환이 가능하다.

하위 인터페이스 타입으로 변환되면 상위 인터페이스와 하위 인터페이스에 선언된 모든 메소드를 사용할 수 있지만, 상위 인터페이스 타입으로 변환되면 상위 인터페이스에 선언된 메소드만 사용 할 수 있다.

```java
public interface FirstParent {
    public abstract void firstMethod();
}
```

```java
public interface SecondParent {
    public abstract void secondMethod();
}
```

```java
public interface Child extends FirstParent, SecondParent{
    public abstract void childMethod();
}
```

 여기에 세 인터페이스가 있는데 `FirstParent` 인터페이스와 `SecondParent` 인터페이스가 있고 그 둘을 상속 받는 `Chlid` 인터페이스가 있다. 그렇다면 만약 `Child` 인터페이스를 구현하는 구현객체는 `Chlid` 인터페이스의 상위 인터페이스인 `FirstParent`와 `SecondParent`의 메소드까지 구현해야 한다.

```java
public class ImplementationChild implements Child {
    @Override
    public void firstMethod() {	// firstParent()의 구현 메소드
        System.out.println("This is FirstParent method");
    }

    @Override
    public void secondMethod() {	// secondParent()의 구현 메소드
        System.out.println("This is SecondParent method");
    }
    
    @Override
    public void childMethod() {	// childMethod()의 구현 메소드
        System.out.println("This is Child Method");
    }
}
```



```java
public class HelloJava {
    public static void main(String[] args) {
        Child child = new ImplementationChild();
        FirstParent firstParent = new ImplementationChild();
        SecondParent secondParent = new ImplementationChild();

        child.firstMethod();	// "This is FirstParent method"
        child.secondMethod();	// "This is SecondParent method"
        child.childMethod();	// "This is Child method"

        firstParent.firstMethod();	 // "This is FirstParent method"
        // firstParent.secondMethod(); < 호출 불가능 >
        // firstParent.childMethod(); < 호출 불가능 >

        // secondParent.firstMethod(); < 호출 불가능 >
        secondParent.secondMethod();	// "This is SecondParent method"
        // secondParent.childMethod(); < 호출 불가능 >
    }
}
```

<br>

## *디폴트 메소드와 인터페이스 확장*

디폴트 메소드를 사용하면 기존 인터페이스를 확장해서 새로운 기능을 추가할 수 있다. 인터페이스를 구현한 구현 객체는 인터페이스의 메소드를 사용하기 위해서 오버라이딩 해줘야 하는데, 디폴트 메소드는 오버라이딩을 해줄 필요 없이 바로 사용할 수 있어서 새로운 기능을 추가하기에 용이하다. 

```java
public interface Child {
    public void childMethod();
}
```

만약 인터페이스 `Child`에 다음과 같이 `childMethod()` 가 선언되어있다고 하자

```java
public class ImplementationChild implements Child {
    @Override
    public void childMethod() {
        System.out.println("This is Child Method");
    }
}
```

그리고 `ImplementationChild` 클래스는 `Child` 인터페이스의 구현 클래스이다. `childMethod()`를 오버라이딩하였다. 그리고 이렇게 사용되던 와중에 만약 `Child` 인터페이스에 새로운 기능을 추가해야되는데 오버라이딩할 수가 없다면

```java
public interface Child {
    public void childMethod();
    public default void defMethod() {
        System.out.println("This is default method");
    } 
}
```

위와 같이 `Child` 인터페이스에 `default` 메소드인 `defMethod()`를 선언하여 `Child` 인터페이스의 구현 클래스에 오버라이딩하지 않아도 객체에서 사용할 수 있게 메소드를 만든다.

```java
public class HelloJava {
    public static void main(String[] args) {
        ImplementationChild child = new ImplementationChild();
        child.childMethod();	// "This is Child Method"
        child.defMethod();	// "This is default method"
    }
}
```

디폴트 메소드도 오버라이딩 가능하다. 

```java
@Override
public void defMethod() {
    System.out.println("이것은 재정의한 defMethod 입니다.");
}
```

<br>

### 디폴트 메소드가 있는 인터페이스 상속

만약 부모 인터페이스에 디폴트 메소드가 존재한다면 상속할 때 디폴트 메소드도 같이 상속 받는다. 이것을 활용하는 방법에는 다음과 같이

1. **디폴트 메소드를 그대로 상속 받는다.**
2. **디폴트 메소드를 오버라이딩해서 내용을 변경한다.**
3. **디폴트 메소드를 추상(abstract)메소드로 재선언한다.**
   - 이 때는 구현 객체에서 오버라이딩 해줘야 한다.

<br>

<br>

<br>

___

출처 : 한빛미디어 < 이것이 자바다 > 신용권









<br>























