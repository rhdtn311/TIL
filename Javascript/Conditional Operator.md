## 삼항연산자

삼항연산자는 자바스크립트에서 세 개의 피연산자를 취할 수 있는 유일한 연산자로 `if` 명령문의 단축 형태로 사용된다. 다음과 같은 형태로 사용된다.

``` javascript
condition ? exprIfTrue : exprIfFalse
```

- **condition** : 참 또는 거짓을 판별하는 조건
- **exprIfTrue** : `condition` 이 참(true)일 때 실행되는 구문
- **exprIfFalse** : `condition`이 거짓(false)일 때 실행되는 구문

<br>

> 예제 1 

num이 10보다 큰 수인지 확인하는 삼항연산자

```javascript
const num = 5;
const checkOverTen = (num > 10) ? true : false;

console.log(checkOverTen);	// false
```

<br>

> 예제 2 

변수의 값을 기준으로 다른 메세지를 보여주고자 할 때 사용하는 삼항연산자

```js
const checkVIP = true;
const fee = "The fee is" + (checkVIP ? " 100만원" : " 150만원";)

console.log(fee);	// "The fee is 100만원"
```

<br>

> 예제 3

다중 3항 연산자도 가능하다.

```js
var firstCheck = false,
    secondCheck = false,
    access = firstCheck ? "첫 번째 체크 성공" : secondCheck ? "두 번째 체크 성공" : "체크 실패";

console.log(access);	// "체크 실패"
```

<br>

> 예제 4

하나의 케이스로 둘 이상의 단일 작업시 쉼표(,)로 구분하고 괄호로 묶는다.

```js
var stop = false, age = 23;

age > 19 ? (
    alert("지나가셔도 좋습니다."),
    location.assign("location.html")
) : (
	stop = true,
    alert("이 곳에 가기엔 나이가 너무 어립니다.")
);
```

<br>

> 예제 5

삼항연산자를 반환할 수 있다.

```js
function checkOverTen() {
    const num = 5;
    return (num > 10 ? true : false);
}

checkOverTen();	// false
```

<br>

<br>

___

참고 : [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) 
