# 객체지향 프로그래밍 

객체지 프로그래밍 (OOP) 이란 서로 연관된 변수나 메소드를 그루핑하여 하나의 객체로 만들어 프로그래밍하는 기법을 말한다.

<br>

객체지향을 학습하기 위해서는 **문법**과 **설계**에 대해 잘 알아야한다.

#### 문법

객체지향을 편하게 할 수 있도록 언어가 제공하는 기능을 익히는데, 이러한 기능들은 if, for문 처럼 문법적인 구성을 띄고있다. 이러한 문법을 이해하고 숙지해야한다.



#### 설계

설계는 좋은 객체를 만드는 법이다.  좋은 설계를 위해서는 현실을 잘 반영해야 한다.  이러한 현실은 매우 복잡하기 때문에 있는 그대로 반영할 수 없으므로 **추상화**를 거쳐 소프트웨어에 반영해야한다.  추상화는 불필요한 특성들을 제거하고 내가 원하는 정보만 추출해내는 기법이다.

<br>

#### 부품화 

객체지향은 부품화의 정점이라 할 수 있다. 메소드를 생각해보자 메소드는 연관되어 있는 로직들을 결합하여 내가 필요로 하는 기능을 구현해낸 것으로 이 메소드를 사용하게되면 코드의 양을 줄일 수  있고 메소드 별로 기능이 분류되어 있기 때문에 필요한 코드를 찾기도 쉽고 오류 시 진단도 빠르게 할 수 있다. 

하지만 프로그램의 규모가 커질 수록 메소드의 양이 많아질 것이다. 그렇기 때문에 이 메소드를 관리하는 것에 또 어려움을 겪을 것이며 이는 메소드를 사용하는 이유가 퇴색 되기까지 할 것이다. 

<br>

#### 은닉화, 캡슐화

성공적인 부품화를 위해서는 내부 동작 방법을 모르더라도 사용할 수 있게 해야한다. 즉 내부 동작 방법을 외부로 드러내지 않도록 하고 사용자에게는 그 부품의 사용방법만을 노출하는 것이다. 이러한 특징을 정보의 은닉화, 캡슐화 라고 한다. 

<br>

## *생성자와 new*



#### 객체

객체는 서로 연관된 변수와 함수를 그룹핑한 그릇이라고 할 수 있다. 객체 내의 변수를 프로퍼티(property), 함수를 매소드(method)라고 부른다. 객체의 생성 방법은 다음과 같다.

```javascript
var player = {}

player.name = 'Ramsey';
player.position = 'midfielder'
player.information = function() {
    return 'His name is ' + this.name + ' and His position is ' + this.position;
}
alert(player.information());
```

하지만 위와 같이 객체를 생성하게 되면 var player 부분과 player라는 객체에 값을 입력하는 부분이 분산되어 있으므로 다음과 같이 바꿔줄 수 있다.

```javascript
var player = {
    name : 'Ramsey',
    position : 'midfielder',
    information : function() {
        return 'His name is ' + this.name + ' and His position is ' + this.position;
    }
}
alert(player.information())
```

<br>

#### 생성자

생성자(constructor)는 객체를 만드는 역할을 하는 함수로 자바스크립트에서의 함수는 재사용 가능한 로직의 묶음이 아니라 객체를 만드는 창조자이다.

```javascript
function Player() = {}
var p = new Player());	>>> 새로운 빈 객체가 생성된다. p = {}

p.name = 'Ramsey';
p.position = 'midfielder';
p.information = function() {
    return 'His name is ' + this.name + ' and His position is ' + this.position;
}
```

위 코드는 앞서 설명했던 객체를 생성하여 만드는 방법과 똑같다. 이제 아래 코드를 보자.

```javascript
function Player() {}

var p1 = new Player();
p1.name = 'Ramsey';
p1.position = 'midfielder';
p1.information = function() {
    return 'My name is ' + this.name + ' and my position is ' + this.position;
}

var p2 = new Player();
p2.name = 'Martinelli';
p2.position = 'forward';
p2.information = function() {
    return 'My name is ' + this.name + ' and my position is ' + this.position;
}
```

위 코드에서 Player() 함수를 통해 생성된 객체인 p1과 p2는 name과 position은 다르지만 information() 매서드는 같다는 것을 알 수 있다.  이는 프로그래밍시 코드의 단순화에 영향을 미치는 코드의 중복이 일어난 것으로 매우 좋지 않은 코드라고 할 수 있다. 따라서 중복을 없애기 위해 생성자를 다음과 같이 사용한다.

```javascript
function Player(name,position) {
    this.name = name;	// Player 생성자를 통해 생성된 객체의 속성 name의 값은 인자로 받는 name 변수이다.
    this.position = position;	// Player 생성자를 통해 생성된 객체의 속성 position의 값은 인자로 받는 position 변수이다.
    // 중복이 됐던 매소드는 한 번만 정의돼도 생성자를 통해 객체를 생성할 때마다 자동으로 생성되도록 하였다.
    this.information = function() {
        return 'My name is ' + this.name + ' and my position is ' + this.position;
    }	
}
var p1 = new Player('Ramsey','midfielder');
var p2 = new Player('Martinelli','forward');
```

우리가 Player라는 생성자가 만들어 놓은 빈 객체가 어떠한 프로퍼티와 매서드를 가져야 하는 지 생성자 함수 안에다 기술함으로써 중복을 방지하게 되는데 이러한 것을 **초기화(init, initialize)** 라고 한다.
