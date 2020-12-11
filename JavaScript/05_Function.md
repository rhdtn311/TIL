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

참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%ED%95%A8%EC%88%98 <br>
      inflearn 생활코딩 자바스크립트 언어 기본편
