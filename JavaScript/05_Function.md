# 함수 (Function)

함수는 하나의 로직을 재실행 할 수 있도록 하는 것으로 코드의 재사용성을 높여준다.

<br>



## *함수의 형식 (정의)*

```javascript
function 함수명 (매개변수) {
    코드;
    return 반환 값;
}
```

함수의 이름을 지어주고 함수가 호출될 때 어떤 작업을 수행하는지 정해준다. 

매개변수를 입력받고 매개변수를 이용하여 정해진 작업을 수행하고 하나의 반환 값을 반환한다.

<br>

## *함수의 호출*

```javascript
함수명(인자);
```



#### 예시

```javascript
function plus(number1, number2) 		// plus라는 이름의 함수를 정의함
    return number1 + number2
}

plus(1,2);// plus라는 함수에 인자로 number1에는 1, number2에는 2를 대입하여 함수를 호출함

>>> 3 
```

<br>

## *함수 표현식 ( 익명 함수 )*

이름을 가지지 않는 함수

``` javascript
var plus = function(number1,number2){return number1 + number2};    // plus 라는 변수에 number1과 number2를 더하는 함수가 정의됌.
var x = plus(1,2);

>>> 3 
```

함수 표현식에 이름을 지정할 수 있고 이는 함수 내에서 자신을 참조하는데 사용하는데 유용하다.



```javascript
var factorial = function fac(n) {if (n<2) { return 1 } else { return n*fac(n-1)}};
factorial(5) ;

>>> 120
```

위 코드처럼 재귀함수를 이용하여 자기 자신을 참조하는데 사용된다. 위 코드는 factorial(!) 을 표현한 함수이다.

<br>

또, 함수를 다른 함수의 매개변수로 전달할 때 편리하다. 

```javascript
function map(f,a) {		// map이란 함수를 선언하여 매개변수로 함수로 지정될 f와 배열 a를 받음
    var result = [],
        i
    for (i = 0; i != a.length; i++)		// i가 0부터 배열a의 모든 원소의 크기만큼 증가함
        result[i] = f(a[i]);		// result라는 새로 정의한 배열에 배열 a의 모든 원소에 함수f를 수행한 반환값을 저장
    return result;	// 배열 result 반환
}
var three_multiply = function(x) {	// f로 지정될 함수를 정의 (함수표현식)
    return x * x * x;
}
var numbers = [1,2,3,4,5];	// a로 지정될 배열을 선언
var cube = map(three_multiply,numbers);	// map함수의 매개변수로 함수표현식으로 정의된 three_multiply 함수를 사용
ducument.write(cube);

>>> [1,8,27,64,125]
```
<br>


## *전역변수와 지역변수*

**전역변수**는 함수 외부에서 선언된 변수로 프로그램 전체에서 접근할 수 있는 변수

**지역변수**는 함수 내부에서 선언된 변수로 함수가 실행되면 생성되고 함수가 종료되면 사라지는 변수이다. 함수 외부에서 접근할 수 없다.

```javascript
var glo_v = 10	// 함수 밖에서 선언하면 전역변수가 된다.

function f() {
    var local_v = 20	// 함수 안에서 선언하면 지역변수가 된다.
}

console.log(glo_v);		>>> 10
console.log(local_v);	>>> VM1286:8 Uncaught ReferenceError: local_v is not defined
```

<br>

#### var

함수 밖에서 var를 사용하여 변수를 선언하면 전역변수로 선언되지만 함수 안에서 var를 사용하여 변수를 선언하면 지역변수가 된다. 하지만 함수 안에서 var를 사용하지 않고 변수를 선언하면 그 함수가 호출된 후 그 변수는 전역변수가 된다.

```javascript
function f() {
    local_v = 20
}

f()
console.log(local_v)	>>> 20
```

<br>

#### 정적 유효 범위

``` javascript
var i = 5;

function a() {
    var i  = 10;
    b();
}

function b() {
    document.write(i);
}

a()  >>> ? 
```

위 코드에서 먄악 a함수를 호출한다면 b함수도 호출될 것이고 그렇다면 b함수를 호출할 때 i 는 함수 a의 지역변수 i (10) 가 호출될까 아니면 전역변수인 i(5) 가 호출될까 ? 

정답은 전역변수 i (5)가 호출된다. 그 함수가 사용될 때가 아니라 정의될 때의 전역변수가 참조된다. 이런 것을 정적 유효범위라고 한다. 

<br>


## *함수의 용도*

#### 값으로서의 함수

자바스크립트에서는 함수도 객체이다. 즉 값이다. 거의 모든 언어가 함수를 가지고 있다. 자바스크립트의 함수가 다른 언어의 함수와 다른 점은 함수가 값이 될 수 있다는 점이다.

```javascript
function a() {}    
var a = function() {}  
```

위 두 표현은 같은 것이다. 즉 함수는 변수에 담겨져 값으로 표현된다.

<br>

```javascript
a = {
    b:function() {
    }
}
```

객체 안에서 키의 값으로 함수가 사용될 수 있는데 이 때는 **메소드**라고 불린다.	

<br>

``` javascript
function cal(func,num) {
    return func(num)
}
function increase(num) {
    return num+1
}
function decrease(num) {
    return num-1
}
alert(cal(increase,1))	>>> 2
alert(cal(decrease,1))	>>> 0
```

함수는 다른 함수의 인자로 전달 될 수도 있다. 위 코드에서 cal이라는 함수의 첫 번째 파라미터로 함수를 받아 두 번째 파라미터를 그 함수의 인자로 받는데 사용된다.

<br>

```javascript
function cal(mode) {
    var funcs = {
        'plus' : function(left, right) {return left + right}
        'minus' : function(left, right) {return left - right}
    }
	return funcs[mode];
}
alert(cal('plus')(2,1));	>>> 3
alert(cal('minus')(2,1));	>>>	1
```

함수는 다른 함수의 리턴 값으로 사용될 수 있다. cal('plus')(2,1) 를 호출하게 되면 우선 cal('plus')를 통해 funcs['plus'] 를 반환 하여 funcs['plus']의 값인 함수가 호출되고 (2,1)가 그 함수의 인자로 사용되어 3이라는 값을 반환하게된다.

<br>

```javascript
var process = [
    function(input) {return input + 9;},
    function(input) {return input * input;},
    function(input) {return input / 2;}    
];
var input = 1;
for(var i = 0; i < process.length; i++) {
    input = process[i](input);
}
alert(input)
```

함수는 배열의 값으로도 사용될 수 있다. 위 코드에서 process라는 배열 안에 함수들이 값으로 들어왔는데 코드를 실행해보면 결과 값으로 50이 잘 출력된다. 

<br>

이처럼 함수는 값으로서 변수, 매개변수, 리턴 값으로 사용될 수 있는데 이러한 용도로 사용될 수 있는 형태의 데이터를 프로그래밍에서는 **first-class citizen(object)** 라 부른다.

<br>

## *콜백*

함수가 수신하는 인자가 함수인 경우를 콜백이라고 한다. 배열에서 배웠던 sort 함수의 인자가 대표적인 콜백함수이다. 비동기처리를 하는데 사용된다.

[\>>>콜백 <<<](https://github.com/rhdtn311/TIL/blob/main/JavaScript/06_array.md)

<br>

## *클로저 (closure)*
클로저는 내부함수가 외부함수의 맥락에 접근할 수 있는 것을 가르킨다.



### 내부함수와 외부함수

자바스크립트는 함수 안에서 또 다른 함수를 선언할 수 있다.

```javascript
function outter() {
    var title = 'Hello World!'
    function inner() {
        alert(title);
    }
    inner();	>>> 'Helo World!'
}
outter();	>>> 'Hello World!''
```

위 코드에서 inner() 함수는 내부함수이고 outter() 함수는 외부함수이다.<br>

위 코드에서 inner() 함수 내부에는 어떤 변수도 선언해주지 않았다. 하지만 외부함수에 선언된 title이라는 변수를 내부함수에서 호출했을 경우 정상적으로 호출이 된다. 즉, 내부함수는 외부함수의 지역변수에 접근할 수 있다.
<br>
#### private variable

```javascript
function factory_movie(title) {
    return {
        get_title : function() {
            return title;
        },
        set_title : function(_title) {
            title = _title
        }
    }
}
totoro = factory_movie("Totoro");	

totoro.get_title()	>>> "Totoro" // 외부함수의 매개변수를 참조
totoro.set_title("이웃집 토토로");	// factory_movie("Totoro").set_title("이웃집 토토로")로 title이 "이웃집 토토로"가 됌 

alert(totoro.get_title());	>>> 이웃집 토토로	
```

위 코드에서 title이라는 변수는 get_title() 메소드를 통해서만 호출될 수 있고 set_title() 메소드를 통해서만 값이 변경될 수 있다.  즉, 외부에서 값을 변경할 수 없다. 그렇기 때문에 private하다 할 수 있다. 
<br>
<br>
<br>
참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%ED%95%A8%EC%88%98 <br>
      inflearn 생활코딩 자바스크립트 언어 기본편
