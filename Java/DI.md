# DI(Dependency Injection)

- 하나의 객체가 다른 객체의 의존성을 제공하는 기술로 **의존성 주입** 이라고 한다.
- 의존성 주입의 의도는 객체의 생성과 사용의 관심을 분리하는 것이다.
- 의존성 주입을 통해 다음과 같은 이점이 생긴다.
  - 단일 테스트가 용이해진다.
  - 코드의 재활용성을 높여준다.
  - 객체 간의 의존성이 감소한다.
  - 결합도가 낮아진다.

<br>

## *의존성*

- 예를 들어 서비스로 사용할 수 있는 객체이다. 클라이언트가 어떤 서비스를 사용할 것인지 지정하는 대신, 클라이언트에게 무슨 서비스를 사용할 것인지를 말해주는 것이다.

```java
class Programmer {
    private Coffee coffee;
    
    public Programmer() {
        this.coffee = new Coffee();
    }
    
    public stratProgramming() {
        this.coffee.drink();
        ...
    }
}
```

위 코드에서 `Progremmer` 클래스에서 `startProgramming` 함수가 호출되기 위해서는 `Coffee` 클래스를 필요로 하는데, 이것을 **`Programmer` 클래스는 `Coffee` 클래스의 의존성을 가진다고 말한다.**

위와 같이 의존성을 가지게 코드를 설계한다면 `Coffee` 클래스가 수정될 때, `Programmer` 클래스도 함께 수정되어야 한다는 문제가 생긴다.

<br>

## *주입*

- 의존성(서비스)을 사용하려는 객체(클라이언트)로 전달하는 것을 의미한다.

<br>

## *의존성 주입을 통한 해결*

만약 **DI**를 사용하지 않고 `Coffee` 클래스의 상속을 받은 `Cappuccino`나 `Americano` 클래스를 사용해야 한다면 다음과 같이 직접 수정해줘야 한다.

```java
class Coffee { ... }

class Cappuccino extends Coffee { ... }
class Americano extends Coffee { ... }

class Programmer {
    private Coffee coffee;
    
    public Programmer() {
        this.coffee = new Cappuccino();	// 직접 수정
    }
}
```

하지만 의존성 주입을 통해 다음과 같이 바꿀 수 있다.

```java
class Programmer {
    private Coffee coffee;
    
    public Programmer(Coffee coffee) {
        this.coffee = coffee;
    }
    
    public stratProgramming() {
        this.coffee.drink();
    }
}
```

위와 같이 필요한 클래스를 직접 생성하는 것이 아닌, 주입함으로써 객체 간의 결합도를 줄이고 유연한 코드를 작성할 수 있다.

<br>

<br>

<br>

___

참고 : https://velog.io/@wlsdud2194/what-is-di

https://ko.wikipedia.org/wiki/%EC%9D%98%EC%A1%B4%EC%84%B1_%EC%A3%BC%EC%9E%85







