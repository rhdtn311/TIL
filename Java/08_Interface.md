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























