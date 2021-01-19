# 상속

- 부모 클래스의 멤버를 자식 클레스에게 물려주는 것
- 상속 제한되는 경우
  - `private` 접근 제한을 갖는 필드, 메소드
  - 부모 클래스와 자식 클래스가 서로 다른 패키지에 있을 때 : `default` 접근 제한을 갖는 필드와 메소드

<br>

## *클래스 상속*

```java
class 자식클래스 extends 부모클래스 {
}
```

단 하나의 부모클래스만을 상속받을 수 있다.

<br>

## *부모 생성자 호출*

- 자식 객체를 생성하면 내부적으로 부모 객체가 먼저 생성되고 자식 객체가 그 다음에 생성된다.
  - 자식 생성자에 부모 객체를 생성할 수 있는 생성자가 포함되어 있다. (맨 첫 줄)

```java
class 자식클래스 extends 부모클래스 {
    // 생성자
    public 자식클래스() {
        super([매개값1, ... ]);	// 부모 객체의 기본 생성자 (부모 클래스 생성자에 매개값이 있으면 입력해야함)
    }
}
```

<br>

## *메소드 오버라이딩(Overriding)*

부모 클래스로부터 상속받은 메소드를 자식 클래스에서 재정의 하는 것

- 메소드 오버라이딩 시 주의할 점  
  - 부모 메소드와 **동일한 signature(리턴 타입, 메소드 이름, 매개 변수 리스트)**를 가져야 한다.
  - 접근 제한을 더 강화해서 오버라이딩 할 수 없다.(부모 : `public`, 자식 : `private` 는 안된다.  반대는 가능) 
  - 새로운 예외를 `throws`할 수 없다.

<br>

### 부모 메소드 호출(super)

자식 클래스에서 부모 클래스의 메소드를 오버라이딩해서 더 이상 부모 클래스의 메소드를 사용할 수 없다면 `super` 키워드를 입력하여 오버라이딩하지 않은 부모 클래스의 메소드를 자식 클래스 내에서 사용할 수 있다.

```java
// 부모 클래스
public class Parent {
    int firstMethod() { ... }
    void secondMethod() { ... }
}

// 자식 클래스
public class Child extneds Parent {
    int firstMethod() { ... } // 메소드 오버라이딩
    firstMethod() // 오버라이딩 된 메소드 호출
    super.firstMethod()	// 오버라이딩 전인 부모 클래스의 메소드 호출
}
```

<br>

## final 클래스와 final 메소드

`final` 키워드는 클래스, 필드 메소드 선언 시에 사용할 수 있다. 어디에 사용되느냐에 따라 해석이 달라진다.

<br>

### final 클래스

`final` 클래스는 최종적인 클래스로 보기 때문에 상속할 수 없게된다.

```java
public final class ClassName { ... }
```

<br>

### final 메소드

`final` 메소드는 최종적인 메소드이기 때문에 메소드 오버라이딩이 불가능해진다.

```java
public final 리턴타입 methodName([param1, param2, ... ]) { ... }
```

<br>

## *protected 접근 제한자*

`protected` 접근 제한자는 같은 패키지는 접근 허용하지만 다른 패키지에서는 자식 클래스만 접근을 허용한다.

<br>

## *타입 변환과 다형성*

타입 변환은 데이터 타입을 다른 데이터 타입으로 변환하는 것을 말한다. 기본 타입의 변환처럼 클래스 타입도 타입 변환이 있다. 클래스 타입의 변환은 자식 타입이 부모 타입으로 자동 타입 변환이 가능하다.

<br>

### 자동 타입 변환(Promotion)

프로그램 실행 중에 자동으로 타입 변환이 일어나는 것으로 클래스 타입의 타입 변환은 다음과 같다.

```java
// 부모 클래스
public class Parent {
}

// 자식 클래스
public class Child extneds Parent {
}
```

위와 같이 부모클래스(`Parent`)와 부모클래스를 상속받은 자식 클래스(`Child`)가 있다면 자식 클래스의 객체를 부모 클래스의 변수에 대입하면 자동 타입 변환이 일어난다.

```java
Child child = new Child();
Parent parent = child;
```

바로 위 부모가 아니더라도 상속 계층에서 상위 타입이라면 자동 타입 변환이 일어난다.

***부모 타입으로 자동 타입 변환된 이후에는 부모 클래스에 선언된 필드와 메소드만 접근 가능하다.  하지만 자식 클래스에서 메소드가 오버라이딩 되었다면 자식 클래스의 메소드가 대신 호출된다.***

```java
// 부모 클래스
public class Parent { 
	// 메소드
    void method1() { ... }	// 'A' 메소드
    void method2() { ... }	// 'B' 메소드
}

// 자식 클래스
public class Child {
    // 메소드
    void method1() { ... }	// 메소드 오버라이딩 'C' 메소드
    void method3() { ... }	// 'D 메소드'
}
```

```java
class Example {
    public static void main(String[] args) {
        Child child = new Child();
        Parent parent = child;	// 자동 타입 변환
        
        parent.method1()	// 오버라이딩한 'C' 메소드 호출 (O)
        parent.method2()	// 부모 메소드인 'A' 메소드 호출 (O)
        parent.method3()	// 자식 메소드에서 선언했기 때문에 호출 불가능 (X)
    }
} 
```

<br>

### 필드의 다형성

다형성이란, 동일한 타입을 사용하지만 다른 결과가 나오는 성질을 말한다. 주로 필드의 값을 다양화함으로써 실행 결과가 다르게 나오도록 구현하는데, 필드의 타입은 변함 없지만, 실행 도중에 어떤 객체를 필드로 저장하느냐에 따라 실행 결과가 달라질 수 있다.

다형성의 구현 방법은 클래스의 상속이나 인터페이스를 구현하는 자식 클래스에서 메서드를 오버라이딩하고 자식 클래스를 부모 타입으로 업캐스팅한다. 그리고 부모 타입의 개체에서 자식 멤버를 참조하여 다형성을 구현한다.

```java
interface LeagueOfLegend {	// 인터페이스
    // 추상 메소드
    void name();	
    void keyQ();
    void keyW();
    void keyE();
    void keyR();
}

class Ezreal implements LeagueOfLegend {	// 인터페이스 구현 클래스
    // 오버라이딩
    public void name() {	
        System.out.println("이름 : 이즈리얼");
    }
    public void keyQ() {
        System.out.println("신비한 화살");
    }
    public void keyW() {
        System.out.println("정수의 흐름");
    }
    public void keyE() {
        System.out.println("비전 이동");
    }
    public void keyR() {
        System.out.println("정조준 일격");
    }
}

class Ahri implements LeagueOfLegend {	// 인터페이스 구현 클래스
    // 오버라이딩
    public void name() {
        System.out.println("이즈리얼");
    }
    public void keyQ() {
        System.out.println("현혹의 구슬");
    }
    public void keyW() {
        System.out.println("여우불");
    }
    public void keyE() {
        System.out.println("매혹");
    }
    public void keyR() {
        System.out.println("혼령 질주");
    }
}

public class PlayLOL {
    pulbic static void main(String[] args) {
        LeagueOfLegend lol;	// 인터페이스 객체 선언
        System.out.println("캐릭터 선택 : 1. 이즈리얼 2. 아리");
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int(n == 1) {
            lol = new Ezreal();	// 업 캐스팅
        } else if (n == 2) {
            lol = new Ahri(); // 업 캐스팅
        }
        // 선택한 조건에 따라서 부모 개체로 자식 메소드 사용 (하나의 타입으로 다양한 결과 => 다형성)
        lol.name();
        lol.keyQ();
        lol.keyW();
        lol.keyE();
        lol.keyR();        
    }
}
```

<br>

###  매개 변수의 다형성

메소드를 호출할 때 매개값을 다양화하기 위해 매개 변수에 자식 타입 객체를 지정할 수 있다.

```java
// Skill 클래스
public class Skill {
    public void skill(Champion champion) {	
        champion.attack();
    }
}
```

`Skill` 클래스에는 `skill` 메소드의 매개값으로 `Champion` 타입을 받는다. 그리고 그 `Champion` 타입의 `attack` 매소드를 실행한다.

```java
// Champion 클래스
public class Champion() {
    public void attack() {
        System.out.println("적을 공격합니다.");
    }
}
```

`Champion` 클래스는 위와 같다. 부모클래스이다.

```java
public class Ezreal extends Champion {
    @Override
    public void attack() {
        System.out.println("정조준 일격!");
    }
}
```

`Champion` 클래스를 상속받은 `Ezreal` 클래스이다.  `Champion` 클래스의 `attack()` 메소드를 오버라이딩하였다.

```java
public class Ahri extends Champion {
    @Overrid
    public void attack() {
        System.out.println("정수의 구슬!");
    }
}
```

마찬가지로 `Champion` 클래스를 상속받은 `Ahri` 클래스이다. `Champion` 클래스의 `attack()` 메소드를 오버라이딩했다.

```java
public class AttackChampion {
    public static void main(String[] args) {
        Skill s = new Skill();	
        Champion champion = new Champion();
        Ezreal ezreal = new Ezreal();
        Ahri ahri = new Ahri();
        
        s.skill(champion);	// 적을 공격합니다.
        s.skill(ezreal);	// 정조준 일격!
        s.skill(ahri);	// 정수의 구슬!
    }
}
```

`Skill` 클래스의 `skill` 메소드를 사용하기 위해 `new` 연산자를 이용하여 `Skill` 개체를 생성하고 `skill`메소드의 매개값인 `Champion` 객체를 `s.skill()`의 매개변수로 넣었다. 그리고 그 `Champion`객체를 상속받은 클래스의 객체인 `ezreal`과 `ahri` 객체도 `s.skill()`의 매개변수로 넣어 각각 오버라이딩한 `ezreal.attack()`과 `ahri.attack()`이 실행되도록 하였다.

<br>

### 강제 타입 변환(Casting)

강제 타입 변환은 부모 타입을 자식 타입으로 변환하는 것을 말하며, 자식 타입이 부모 타입으로 자동 변환한 후, 다시 자식 타입으로 변환할 때 강제 타입 변환을 사용할 수 있다.

```java
자식클래스 변수 = (자식클래스) 부모클래스타입;	
// 여기서 부모클래스타입은 자식 타입이 부모 타입으로 변환된 상태이다.
```

자식 타입에서 부모 타입으로 자동 변환하면 부모 타입에 선언된 필드와 메소드만 사용가능한데, 자식 타입에 선언된 필드와 메소드를 꼭 사용해야 한다면 강제 타입 변환을 해서 다시 자식 타입으로 변환한 다음 자식 타입의 필드와 메소드를 사용한다.

 ```java
// 부모 클래스
public class Parent {
    String parentField;
    
    void parentMethod() { ... }
}

// 자식 클래스
public class Child extends Parent {
    String childField;
    
    void childMethod() { ... }
}

// main()
class Example {
    public static void main(String[] args) {
        Parent parent = new Child();	// 자동 타입 변환
        parent.parentField;	// 가능
        parent.parentMethod;	// 가능
        parent.childField;	// 불가능
        parent.childMethod();	// 불가능
        
        Child child = (Child) parent;	// 강제 타입 변환
        child.childField;	// 가능
        child.childMethod();	// 가능
    }
}
 ```

<br>

### 객체 타입 확인 (instance of)

강제 타입 변환은 자식 타입이 부모 타입으로 변환되어 있는 상태에서만 가능하다. 따라서 부모 변수가 참조하는 객체가 부모 객체인지 자식 객체인지 확인하기 위해 `instance of` 연산자를 사용할 수 있다.

```java
객체 instance of 타입	// 객체가 우항의 인스턴스이면 true
```

`instance of` 연산자는 매개값의 타입을 조사할 때 주로 사용되는데, 메소드 내에서 강제 타입 변환이 필요할 경우 `instace of` 연산자로 확인하고 강제 타입 변환을 해야 한다.

```java
public void method(Parent parent) {
    if (parent instance of Child) {	// 즉 Parent parent = new Child();
        Child child = (Child) parent;
    }
}
```

<br>

## *추상 클래스*

- **실체 클래스** : 객체를 직접 생성할 수 있는 클래스
- **추상 클래스** : 실체 클레스들의 공통적인 특성을 추출해서 선언한 클래스
- 추상 클래스와 실체 클래스는 상속 관계를 가진다.
  - 추상 클래스가 부모 클래스, 실체 클래스가 자식 클래스이다.
- 추상 클래스는 객체를 직접 생성할 수 없다. (`new` 연산자 불가능)

<br>

### 추상 클래스의 용도

1. 실체 클래스들의 공통된 필드와 메소드의 이름을 통일
2. 실체 클래스 작성 시간 절약

<br>

### 추상 클래스 선언

추상 클래스는 클래스 선언에 `abstract` 키워드를 붙인다.

```java
public abstract class 추상클래스 {
    // 필드
    // 생성자
    // 메소드
}
```

추상 클래스의 생성자는 추상 클래스의 자식 클래스에서 `super` 키워드를 사용하여 추상 클래스 객체를 생성하게 한다.

<br>

### 추상 메소드와 오버라이딩

추상 메소드는 추상 클래스에서만 선언할 수 있는데, 메소드의 선언부만 있고 메소드 실행 내용(중괄호)은 없는 메소드를 말한다. 추상 클래스를 상속 받은 클래스가 추상 클래스 안에 있는 추상 메소드를 오버라이딩 하지 않으면 오류가 발생한다. 추상 메소드는 다음과 같이 선언한다.

```java
[public|protected] abstract 리턴타입 메소드명(매개변수, ... );
```

<br>

```java
// 추상 클래스 
public abstract class Champion {
    // 필드
    public String name;
	
    // 생성자
    public Champion(String name){
        this.name = name;
    }
	
    // 추상 메소드
    public abstract void qSkill();
    public abstract void wSkill();
    public abstract void eSkill();
    public abstract void rSkill();
}
```

```JAVA
public class Jhin extends Champion {	// 추상 클래스를 상속받은 클래스
    Jhin(String name) {	
        super(name);	// 추상 클래스의 생성자
    }

    // 추상 메소드를 오버라이딩
    @Override
    public void qSkill() {
        System.out.println("춤추는 유탄");
    }

    @Override
    public void wSkill() {
        System.out.println("살상연희");
    }

    @Override
    public void eSkill() {
        System.out.println("강제 관람");
    }

    @Override
    public void rSkill() {
        System.out.println("커튼 콜");
    }
}

// 추상 클래스를 상속 받은 클래스 
public class Varus extends Champion {
    public Varus(String name) {
        super(name);	// 추상 클래스의 생성자
    }
    
    // 추상 메소드를 오버라이딩
    @Override
    public void qSkill() {
        System.out.println("꿰뚫는 화살");
    }

    @Override
    public void wSkill() {
        System.out.println("역병 화살");
    }

    @Override
    public void eSkill() {
        System.out.println("퍼붓는 화살");
    }

    @Override
    public void rSkill() {
        System.out.println("부패의 사슬");
    }
}
```

```java
public class ExAbstractClass {
    public static void main(String[] arg) {
       
        Jhin jhin = new Jhin("진");	
        System.out.println(jhin.name);	// "진"

        jhin.qSkill();	// "춤추는 유탄"
        jhin.rSkill();	// "커튼 콜"

        Varus varus = new Varus("바루스");	
        System.out.println(varus.name);	// "바루스"

        varus.wSkill();	// "역병 화살"
        varus.eSkill();	// "퍼붓는 화살"

        Champion champion = new Jhin("진");	// 자동 타입 변환
        champion.qSkill();	// "춤추는 유탄"
        
    }
}
```

<br>

<br>

<br>

___

출처 : 한빛미디어 < 이것이 자바다 > 신용권





