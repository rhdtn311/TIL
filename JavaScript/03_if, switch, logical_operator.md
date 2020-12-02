# 조건문

주어진 조건이 참(true) 일 때 원하는 문장을 실행하는 구문으로 자바스크립트에서는 [ if...else문] , [witch문] 이 존재한다.

<br>



## *if ... else 문*

특정 조건이 참인 경우 원하는 문장을 실행하기 위해 if문을 사용하며 선택적으로 조건이 거짓인 경우 원하는 문장을 실행하기 위해서 else절을 사용한다.



``` javascript
if (조건) {
    문장1;
}
else {
    문장2;
}
```



조건이 참(true)인 경우 문장1이 실행되고 거짓(false)인 경우 문장2가 실행된다.

더 나아가 ***else if문***을 통하여 조건문을 더 복잡하게 할 수 있다.



<br>



#### else if문

```javascript
if (조건1) {
    문장1;
}
else if (조건2) {
    문장2;
}
else if (조건3) {
    문장3;
}
else {
    문장4;
}
```



조건1이 참(true)인 경우 문장1이 실행되고 조건2가 (true)인 경우 문장2가 실행되고 조건3이 참(true)인 경우 문장3이 실행되고 조건1,조건2,조건3 모두 거짓(false)인 경우 문장4가 실행된다.

<br>

## *거짓으로 취급되는 값*

[if ... else 문]에서 조건이 참이 되는 경우와 거짓이 되는 경우 실행되는 문장이 달랐다. 여기서 조건절에 사용할 수 있는 참인 경우와 거짓인 경우를 살펴본다.

- false
- undefined
- null
- 0
- NaN
- the enpty string(" ") 
  - 여기서 빈 배열인 [] 는 [] == false 인데, Boolean([ ]) 는 true이며 조건으로 취급할 때 true로 되어 문장이 실행된다.



<br>



## *논리 연산자*

논리 연산자는 조건문을 더 간결하고 다양한 방법으로 구사할 수 있도록 도와준다.

<br>

### &&

&&는 좌항과 우항이 모두 참(true)일 때 참이된다. ( and 연산자 )

```javascript
Boolean(true && true)    >>> true
Boolean(true && false)   >>> false
boolean(false && false)  >>> false
```

<br>

### ||

||는 좌항과 우항 중 하나라도 참(true)일 때 참이된다. ( or 연산자 )

```javascript
Boolean(true || false)    >>> true
Boolean(true || true)     >>> true
Boolean(false || false)   >>> false
```

<br>

### !

' ! ' 는 부정의 의미로 Boolean 값을 역전시킨다. true를 false로, false를 true로 바꾼다. ( not 연산자 )

```javascript
Boolean(!true)    >>> false
Boolean(!false)   >>> true
```



<br>

### 예시

논리 연산자를 조건문에 사용하여 간결하게 코드를 작성할 수 있다.

```javascript
var id = prompt("아이디를 입력하세요.");
var password = prompt("비밀번호를 입력하세요.");

if ((id === 'apple311' || id === 'banana12') && password === '123456') {
    alert(" 성공적으로 로그인 되었습니다. ");
} else {
    alert(" 로그인에 실패했습니다. ");
}
```

<br>

## *switch문*

switch문은 프로그램이 표현식의 값이 case의 값과 같으면 그 case의 문장부터 하위문장의 값들까지 실행된다.



```javascript
switch (표현식) {
    case 값1 :
        문장1;
    case 값2 :
        문장2;
    case 값3 : 
        문장3;
       ...
    default : 
    	문장
}
```





간단히 예를 들어보면

```javascript
switch (1) {
    case (0) :
        alert(0);
    case (1) :		// switch의 값과 case의 값이 같기 때문에 여기서부터 문장이 수행됌
        alert(1);
    case (2) :
        alert(2);
    case (3) :
        alert(3);
    default :
    	alert(4);    
}
>>> alert(1), alert(2), alert(3), alert(4)가 순차적으로 실행
```



하위 문장은 배제하고 switch의 값과 case의 값이 같을 때만 문장을 수행하고 싶다면 **break** 를 통해 하위 구문을 배제 시킬 수 있다.

```javascript
switch (1) {
    case (0) :
        alert(0);
    case (1) :		
        alert(1);
        break;		>>> break를 통해 alert(1) 이 수행되고 switch문을 빠져나감
    case (2) :
        alert(2);
    case (3) :
        alert(3);
    default :
    	alert(4);    
}
```

<br>
<br>

참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Control_flow_and_error_handling <br>
참고 : inflearn 나도코딩 자바스크립트 언어 기본편 강의

