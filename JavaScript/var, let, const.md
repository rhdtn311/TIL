## *var, let, const* 

자바스크립트에서 변수를 선언하는 방식에는 var, let, const 총 세 가지 방식이 있다.

<br>

#### var

var는 변수 선언 방법 중 하나인데 매우 단점이 많은 선언 방식이다.

```javascript
a = 10;
var a;

console.log(a);	>>> 10
```

변수를 선언도 하기 전에 값을 대입했더니 오류 없이 정상적으로 출력되었다.  이는 var **호이스팅(hoisting)** 때문이다.  호이스팅은, 어디에 선언했느냐에 상관없이 항상 제일 위로 끌어 올려주는 것을 말한다. 

```javascript
var a = 10;
console.log(a);	>>> 10

var a = 20;
console.log(a)	>>> 20
```

이미 선언했던 변수를 다시 선언했더니 오류 없이 정상적으로 출력되었다.

위 문제들은 자바스크립트에서 매우 유연한 방식의 코드 선언으로 코드가 커지면 문제를 발생시킬 수 있다. 이런 var의 문제점을 해결하기 위해 ES2016에서 새로운 변수 선언 방식인 let, const가 추가되었다.

<br>

#### let

let은 var와 다르게 변수를 선언하기 전에 할당 할 수 없으며 **변수의 재선언이 불가능**하다.

```javascript
console.log(b);	>>> Uncaught ReferenceError: a is not defined
let b = 10;
```



```javascript
let b = 10;	>>> 10
let b = 20;	>>> Uncaught SyntaxError: Identifier 'b' has already been declared 
```

하지만 let은 **변수의 재할당은 가능**하다. 

```javascript
let b = 10;	>>> 10
b = 20;	>>> 20
```

<br>

#### const

반면에 const는 **변수의 재선언, 재할당 모두 불가능**하다.

```javascript
const c = 10;	>>> 10
const c = 20;	>>> Uncaught SyntaxError: Identifier 'e' has already been declared
c = 30;	>>> Uncaught TypeError: Assignment to constant variable.
```

그리고 const는 변수를 선언과 동시에 값을 할당 해야한다.

```javascript
const c;	>>> Uncaught SyntaxError: Missing initializer in const declaration
const c = 10;	>>> 10
```

<br>

<br>

___

참고 : 

- Youtube 드림코딩 엘리(https://www.youtube.com/watch?v=OCCpGh4ujb8&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=3&ab_channel=%EB%93%9C%EB%A6%BC%EC%BD%94%EB%94%A9by%EC%97%98%EB%A6%AC)
- https://poiemaweb.com/es6-block-scope

​		
