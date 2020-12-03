# 객체 (object)

자바스크립트는 객체기반 패러다임 위에서 만들어졌다. 객체는 property의 집합으로 property는 이름(key), 값(value)의 연결로 구성되어있다. property의 값(value)로 함수가 될 수 있는데, 이런 property는 메소드라고 불린다. 브라우저 안에 미리 정의된 객체뿐만 아니라 사용자들이 직접 자신만의 객체를 정의할 수도 있다.  배열은 인덱스로 숫자를 사용하는 반면, 객체는 인덱스를 문자로 정의할 수 있다. 다른 언어에서는 연관배열, 맵, 딕셔너리라는 데이터 타입이 객체에 해당된다.

<br>

자바스크립트에서의 객체는 다른 프록래밍 언어에서와 비슷하게 현실 세계에서의 사물(objects)과 비교할 수 있다. 자바스크립트에서의 객체의 개념은 실세계상에서의 인식 가능한 사물로 이해될 수 있다. 객체는 단독으로 존재 가능한 개체(entity)며 property와 type을 가진다. 예를 들어 컵과 비교를 하면 컵은 사물 객체인데 색깔, 모양, 무게, 재료 등의 속성(property)를 가진다. 

<br>


## *객체와 property*

자바스크립트의 객체에는 그와 연관된 property가 있다. property는 객체와 연관된 변수라고 설명할 수 있다. 객체의 property는 일반 자바스크립트의 변수와 기본적으로 같으나, 객체에 속해있다는 차이가 있다. 객체의 property들이 객체의 특징을 규정하며 property에 접근할 때는 점(.) 표기법을 사용한다. 

```javascript
objectName.propertyName
```

변수와 마찬가지로 객체의 이름과 property의 이름 모두 대소문자를 구분한다. 

<br>

#### *객체와 property의 생성*

```javascript
var 객체이름 = new Object();    // 객체 생성
객체이름.property이름 = "값";

var 객체이름 = {'property이름(key)':값(value), ... }; // 객체와 property의 생성
```

예를 들어 grades라는 객체를 만들어보자 property는 사람이름이다.

```javascript
var scores = new Object();
scores.Kong = 100;
scores["Kim"] = 50;
scores.Park = 20;

var scores = {'Kong' : 100, 'Kim' : 50, "Park" : 20 };

// 위와 아래 모두 같은 scores라는 객체를 생성하는 방법이다.
```

property의 이름은 유효한 자바스크립트 문자열이거나 문자열로 변환이 가능한 것이라면 무엇이든지 가능하다. 

```javascript
var objName = new Object();

objName.var = "var";
objName[" "] = "enpty";
objName["Hi my name is"] = "Taehyun";
objName["One" + "Two"] = "OneTwo";

var fruit = "apple";
objName[fruit] = "delicious";    // objName이라는 객체에 fruit이라는 이름의 property가 생성
```

for ... in 반복문과 함께 사용할 수 있다.

``` javascript
var scores = {'Kong' : 100, 'Kim' : 50, "Park" : 20 };

for (key in scores) {	// key 에 scores 객체의 키 값인 'Kong','Kim','Park'가 순서대로 for문을 통해 대입
    document.write( key + ":" + scores[key] + "<br>"); 
}

>>> Kong:100
	Kim:50
	Park:20
```

<br>

#### *함수를 사용하여 객체 생성*

생성자 함수를 사용하여 객체를 생성할 수 있다. 

1. 생성자 함수를 작성하여 객체 타입을 정의한다. 객체 타입 이름의 첫 글자는 대문자를 사용한다.(관례상)
2. new를 이용하여 객체의 인스턴스를 생성한다.

객체의 타입을 정의하려면 타입의 이름, 속성(property), 메서드 등을 기술하는 함수를 만들어야 한다. 

``` javascript
function player (nationality, age, club) {
    this.nationality = "France";
    this.age = 30;
    this.club = "Arsenal"			// 여기서 this는 객체인 player를 뜻한다. 
}
```

이제 다음과 같이 player라는 이름의 객체를 생성할 수 있다.

```javascript
var thomas = new player("Ghana",27,"Arsenal");
var messi = new player("Argentina",30,"Barcelona");
```

<br>



#### *객체의 property의 값으로 함수를 사용 *

객체의 property의 value 값으로 객체나 함수가 들어올 수 있다.

```javascript
var grades = {
    'list' : {'Kong' : 100, 'Kim' : 50, 'Park' : 20},	// 값(value)으로 객체를 사용
    'show' : function() {
        alert('Hello World!');    // 값(values)으로 함수를 사용
    } 
}

grades['list'];    // grades의 list에 접근   >>> {'Kong' : 100, 'Kim' : 50, 'Park' : 20}
grades['list']['Kong'];    // grades의 list의 Kong에 접근   >>> 100
grades['show']();    // grades의 show 함수에 접근   >>> "Hello World!" 출력
```

하나의 grades라는 객체 안에 서로 관련있는 list와 show 함수를 grouping 해서 하나의 객체로 만듦.

이러한 것들을 **객체지향 프로그래밍** 이라고 한다.

