## 콜백 (Callback)

콜백 함수는 다른 함수의 인자로 사용되거나 이벤트에 의해 호출되어지는 함수를 말한다. 즉, 어떤 함수의 요청으로 처리되어 나온 응답(값)을 콜백하여 다음 함수에서 사용할 수 있는 것을 말한다.

### *동기 (Synchronous)*

- 자바스크립트는 **synchronous**한 언어이다.
  - 동기(synchronous) : 요청 처리가 완료 된 후 다음 요청을 처리 하는 방식으로 이전 요청을 처리하는 시간이 다음 요청에 영향을 준다.
    - A 요청 -> A결과 -> B요청 -> B결과 -> C요청 -> C결과 -> D요청 -> D 결과
  - 즉 호이스팅이 된 이후부터 우리가 작성한 순서에 맞춰서 코드가 하나씩 실행된다.
    - 호이스팅 : var 변수, 함수 선언들이 자동적으로 제일 위로 올라가는 것

```javascript
console.log(1);
console.log(2);
console.log(3);

>>> 1
	2
	3
```

<br>

### *비동기 (Asynchronous)*

- 하나의 요청 처리가 완료되기 전에 다음 요청을 처리하는 방식. 요청과 응답이 다른 시간대에 일어날 수 있다.
  - A요청 -> B요청 -> A결과 -> C요청 -> D 요청 -> D 결과 -> B 결과 -> C 결과

```javascript
console.log(1);

// setTimeout 함수는 첫 번째 인자를 두 번째 인자(ms)만큼 이후에 실행해준다.
setTimeout(function () {	
    console.log(2);
}, 1000);

console.log(3);

>>>	1
	3
	2
```

<br>

### *동기적 콜백 (Synchronous callback)*

콜백함수를 동기적으로 호출하는 방법

```javascript
console.log(1);

// 콜백함수를 동기적으로 호출
function printImmediately(print) {
    print();
}
printImmediately(() => console.log(2));

console.log(3);

>>> 1
	2
	3
```

<br>

### *비동기적 콜백(Asynchronous callback)*

콜백함수를 비동기적으로 호출하는 방법

````javascript
console.log(1);

// 콜백함수를 비동기적으로 호출
function printLater(print, time) {
    setTimeout(print,time);
}
printLater(() => console.log(2),1000);

console.log(3);

>>> 1
	3
	2
````

<br>

## 프로미스 (Primise)

자바스크립트에서 비동기를 간편하게 처리할 수 있도록 도와주는 오브젝트이다. 프로미스는 정해진 장시간의 기능을 수행하고나서 정상적으로 기능이 수행되었다면 성공했다는 메세지와 함께 결과값을 전달해주고, 문제가 발생하여 기능을 수행하지 못했다면 에러 메세지를 전달해준다.

<br>

#### *Promise의 상태*

프로미스는 다음 중 하나의 상태를 가진다. 

- **pending** : 프로미스가 만들어져서 우리가 지정한 오퍼레이션을 수행 중인 상태 
- **fulfilled** : 오퍼레이션을 성공적으로 수행
- **rejected** : 오퍼레이션 수행에 실패함

<br>

#### *Producer, Consumer*

- **Producer** : 우리가 프로미스로부터 원하는 기능을 수행하여 해당하는 데이터를 만들어 내는 오브젝트
- **Consumer** : 우리가 원하는 데이터를 소비하는 오브젝트

<br>

#### *Promise 생성*

프로미스는 생성자 함수처럼 new로 프로미스 객체를 만들 수 있다. 이 때 인자로는 executor를 받고 executor는 resolve와 reject라는 두 개의 콜백함수를 파라미터로 받는 콜백함수이다. executor는 모든 작업을 끝낸 후, 작업이 성공적으로 수행되었으면 resolve 함수를, 오류가 발생하여 실패하였으면 reject 함수를 호출한다. 프로미스는 생성과 동시에 실행된다.

```javascript
// Producer
// Promise는 클래스이기 때문에 new 키워드를 통해 오브젝트를 생성한다.
// Promise의 생성자에는 executor라는 콜백함수를 전달해 주어야한다. 그런데 이 콜백함수 안에는 또 다른 콜백함수인 resolve와 reject를 받는다.
// resolve : 기능을 정상적으로 수행한 후 최종 데이터를 전달하는 콜백함수
// reject : 기능을 수행하다가 중간에 문제가 생기면 호출하는 콜백함수

const promise = new Promise((resolve, reject) => {
    console.log(" 결과는 .. ?! ")
    setTimeout(() => {
        resolve("성공!");
    // or reject("실패!");
    },2000);
});
>>> 결과는 .. ?!
// promise가 만들어지는 순간 excutor가 바로 실행된다.
```

<br>

#### *Promise 사용*

then, catch, finally를 이용하여 프로미스로부터 수행된 값을 받아올 수 있다.

***then***

then 메소드는 promise 객체를 리턴하고, 두 개의 콜백 함수를 인자로 받는다. 첫 번째 인자는 프로미스가 성공적으로 수행했을 때(resolve) , 두 번째 인자는 프로미스가 실패했을 때(reject) 호출하는 콜백 함수이다. 

```javascript
// Consumer

promise.then(
  (resolveCallback) => {
      // 성공했을 때(resolve) 실행
    alert(resolveCallback);},
  (rejectCallback => {
      //실패했을 때(reject) 실행
    alert(rejectCallback);}
))

>>> "성공!" (위 예제에서는 resolve를 받았기 때문에)
```

***chaining***

then 메소드는 chaining이 가능하다. 따라서 다음과 같이 값을 반환할 수 있다.

```javascript
var promise = new Promise((resolve, reject) => {
    setTimeOut(() => {
        resolve(1);
    }, 2000);
});

promise.then((value) => {
    console.log(value);	>> 1
    return value + 1;
}).then((value) => {
    console.log(value);	>> 2
})
```

<br>
<br>
