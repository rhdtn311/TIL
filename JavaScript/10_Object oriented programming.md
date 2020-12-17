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

<br>



## *this*

자바스크립트에서 this는 함수 안에서 사용되는 것으로 그 함수를 어떻게 호출 하느냐에 따라 의미 (this가 가르키는 대상) 가 달라진다.

#### 함수에서의 this

``` javascript
function func() {
    if(window === this) {
        console.log("window === this");
    }
}
func()

>>> window === this
```

window 객체는 자바스크립트의 모든 전역 객체, 전역 함수, 전역 변수의 프로퍼티이다. 자바스크립트 객체의 계층 구조의 최상위에 위치하고 있다. 전역 함수 안에서의 this 는 전역 객체 ( window ) 를 의미한다.

<br>

#### 메소드에서의 this

```javascript
var a = {
    func : function() {
        if (a === this) {
            document.write("a === this")
        }
    }
}
a.func()

>>> a === this
```

메소드에서의 this는 그 메소드가 포함된 객체를 의미한다. 하지만 이 예제는 위의 토픽 ( 함수에서의 this ) 와 같다고 할 수 있다. 자바스크립트의 모든 객체는 window 라는 전역객체의 프로퍼티이기 때문이다. 즉, 위의 함수에서의 this에서 func()는 window라는 전역 객체 안에 포함된 메소드이기 때문에 this는 window를 나타내고, 이 예제에서의 func는 a라는 객체에 포함된 메소드이기 때문에 this는 a를 나타내는 것이다.

<br>

#### 생성자에서의 this

```javascript
var funcThis = null;

function Func() {
    funcThis = this;
}
var o1 = Func();
if(funcThis === window) {
    document.write('window <br />');
                   }
var o2 = new Func();
if(funcThis === o2) {
    document.write('o2 <br />');
}

>>> window
    o2   
```

위 코드는 Func() 객체를 생성자로 사용할 때와 함수로 사용할 때 this가 어떤 의미를 갖는 지 확인하기 위한 코드이다. 우선 Func() 가 변수 o1로 호출되어 함수로 사용될 때는 window 객체를 의미한다. 하지만 Func()가 생성자로 사용될 때는 (o2) 생성자를 통해 만들어진 객체를 의미한다. (o2)   

<br>

#### apply를 통한 this

``` javascript
var a = {}
var b = {}
function func() {
    switch(this) {
        case a :
            document.write('a<br />');
            break;
        case b :
            document.write('b<br />');
            break;
        case window :
            document.write('window<br />');
            break;
            }
}
func();
func.apply(a);
func.apply(b);

>>> window
    a
    b
```

함수를 호출하는 방법에는 apply() 를 이용하여 호출 하는 방법이 있는데 func() 와 같이 그냥 함수를 호출하게 되면 위 코드에서는 this는 window 객체를 의미하지만 apply(인자) 를 통하여 함수를 호출하게되면 this는 apply 함수의 첫번째 인자를 의미하게 된다. 

<br>

## *상속*

상속은 객체의 로직을 그대로 물려 받아 또 다른 객체를 만들 수 있는 기능을 의미한다. 덧붙혀 객체의 로직을 변형하여 새로운 객체를 만들 수 있다.



## *Prototype*

자바스크립트에는 클래스가 없는 대신 우리는 함수로 비슷하게 흉내 내었다. 하지만 여기에는 약간의 문제가 있을 수 있다.

```javascript
function Car() {
    this.wheel = 4;
    this.driver = 1;
}

var tico = new Car();
var sonata = new Car();

document.write(tico.wheel); >>> 4
document.write(tico.driver);	>>> 1

document.write(sonata.wheel);	>>> 4
document.write(sonata.driver);	>>> 1
```

위 예제에서 tico와 sonata는 같은 wheel, driver 값을 갖게된다. 하지만 메모리는 각각 할당하여 총 4개가 할당된다. 이러한 문제는 프로토타입으로 해결 가능하다.

```javascript
function Car() {}
Car.prototype.wheel = 4;
Car.prototype.driver = 1;

var tico = new Car();
var sonata = new Car();

document.write(tico.wheel);	>>> 4
document.write(tico.driver);	>>> 1

document.write(sonata.wheel);   >>> 4
document.write(sonata.driver);	>>> 1
```

위와 같이 Car 객체 안에는 prototype이라는 특수한 프로퍼티가 존재하는데 그 곳에 값을 저장하면 그 객체를 상속하거나 그 객체로부터 생성된 객체는 기존 객체의 prototype 안에 있는 값들을 모두 가져다 사용할 수 있다. 위 예제에서는 Car 객체 어딘가에 있는 prototype이라는 프로퍼티에 wheel 과 driver 라는 값을 저장하고 그 값을 Car를 생성자로 하여 생성된 객체인 tico와 sonata가 공유하여 사용하는 것이다.

```javascript
function Large() {}
Large.prototype.value = 10;

function Midium() {}
Midium.prototype = new Large();

function Small() {}
Small.prototype = new Midium();

var a = new Small();
alert(a.value);

>>> 10
```
위 코드를 보자. 우선 처음에 Large 라는 함수가 생성되었다. 그리고 Large의 프로토타입에 value라는 프로퍼티의 값을 10이라고 저장해두었다. 그리고 Midium의  프로토타입에 Large를 생성자로하는 객체를 저장하였고 Small도 Midium을 생성자로 하는 객체를 prototype에 저장하였다. 따라서 Small을 생성자로 하는 변수 a는 Small의 프로토타입 값을 받았으므로 a.value는 10을 반환하게 된다.


