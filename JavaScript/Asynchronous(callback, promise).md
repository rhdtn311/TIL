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

프로미스는 생성자 함수처럼 **new로 프로미스 객체**를 만들 수 있다. 이 때 인자로는 **executor**를 받고 executor는 **resolve**와 reject라는 두 개의 콜백함수를 파라미터로 받는 콜백함수이다. executor는 모든 작업을 끝낸 후, **작업이 성공적으로 수행되었으면 resolve 함수**를, **오류가 발생하여 실패하였으면 reject 함수**를 호출한다. 프로미스는 생성과 동시에 실행된다.

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

`then(), catch(), finally()`를 이용하여 프로미스로부터 수행된 값을 받아올 수 있다.

***then***

`then()` 메소드는 promise 객체를 리턴하고, 두 개의 콜백 함수를 인자로 받는다. 첫 번째 인자는 프로미스가 **성공적으로 수행했을 때(resolve)** , 두 번째 인자는 **프로미스가 실패했을 때(reject)** 호출하는 콜백 함수이다. 

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

<br>

***catch***

`catch()` 메소드는 에러 처리 하기 위한 메소드로 콜백함수를 인자로 받는데, 그 콜백함수는 프로미스가 실패했을 때 (reject) 호출된다. `then()`의 두 번째 인자와 같은 기능을 수행한다. (에러 처리)

```javascript
const failPromise = new Promise((resolve, reject) => {
    reject('실패!');
});

failPromise.catch((value) => {
    console.log(value);
});
```

<br>

***then vs catch***

그렇다면 then (두 번째 인자)과  catch 중 어떤 것으로 에러처리를 해야 더 효율적일까? 답은 `catch()`를 사용하는 것이다. 아래 예제를 통해 확인해보자.

```javascript
const promise = new Promise((resolve, reject) => {
    resolve('성공!');
})

promise.then((rsv) => {
    console.log(rsv);
    throw new Error("then 메소드 안에 에러가 있습니다.");
}, (rjt) => {
    console.log(rjt);
});

>>> 성공 !
    Uncaught (in promise) Error: then
```

promise의 프로미스에서 `resolve()` 메소드를 호출하여 정상적으로 로직을 처리하였지만('성공!' 메세지 호출) , then의 첫 번째 콜백 함수 내부에서 오류가 발생하였을 때 제대로 잡아내지 못한다. 따라서 코드를 실행하면 `Uncaught (in promise) Error: then (''에러를 잡지 못했습니다.')` 오류가 발생한다. 똑같은 오류를 `catch()` 로 처리해 보자.



```javascript
const promise = new Promise((resolve, reject) => {
    resolve('성공!');
})

promise.then((rsv) => {
    console.log(rsv);
    throw new Error("then 메소드 안에 에러가 있습니다.");
})
    .catch((rjt) => {
    console.log(rjt);
})

>>> 성공 !
    promise.js:66 Error: then 메소드 안에 에러가 있습니다.
```

`catch()` 매소드는 다음과 같이 성공적으로 에러를 콘솔에 출력하였다. 따라서 가급적이면 `catch()` 를 사용하여 에러를 처리하는 것이 좋다.

<br>

***finally***

`finally()` 메소드는 프로미스의 성공, 실패 여부와 상관 없이 마지막에 무조건 호출되는 메소드다.

```javascript
const promise = new Promise((resolve, reject) => {
    resolve('성공!');
})

promise.then((rsv) => {
    console.log(rsv);
}).catch((rjt) => {
    console.log(rjt);
}).finally(() => {
    console.log('finally')
}); 

>>> 성공!
    finally

const promise = new Promise((resolve, reject) => {
    reject('실패!');
})

promise.then((rsv) => {
    console.log(rsv);
}).catch((rjt) => {
    console.log(rjt);
}).finally(() => {
    console.log('finally')
}); 

>>> 실패!
    finally
```

<br>

***chaining***

promise에서는 메소드들끼리 chaining이 가능하다. 따라서 다음과 같이 값을 반환할 수 있다.

```javascript
const promise = new Promise((resolve, reject) => {
    resolve(1);
});

promise
.then((value) => value + 1)	// 2
.then((value) => {
// then은 또 다른 비동기인 Promise를 전달할 수 있다.
    return new Promise((resolve, reject) => {
        reject(value);
    } )
}).catch((value) => value + 10)	// 12
.then((value) => console.log(value));
    
```

<br>

## *async, await*

### async

콜백함수와 Promise의 단점 보완 및 코드를 더 간결하게 하기 위해 등장하였다. async는 다음과 같이 함수 앞에 async를 붙여서 표현하며 return 값으로 Promise를 반환한다. 원시값을 반환한다면 `Promise.resolve`로 래핑되어 반환되고, 함수 내에서 에러가 발생한다면 `Promise.reject()`로 래핑되어 반환된다.

```javascript
var promise = async function() {
    return 10;
}
console.log(promise())
>>> Promise {<fulfilled>: 10}

var promise = async function() {
    throw new Error('error');
    return 10;
}
console.log(promise())
>>> Promise {<rejected>: Error: error ... }
```

`async function`을 `Promise`로 변환하면 다음과 같이 표현할 수 있다.

```javascript
async function AsyncFunction() {
    return console.log("async");
}

function PromiseFunction() {
    return new Promise((resolve, reject) => {
        return resolve("promise");
    })
}

AsyncFucntion().then((rsv) => console.log(rsv));
>>> async
PromiseFunction().then((rsv) => console.log(rsv));
>>> promise
```

<br>

### await

async function 내부에서만 사용할 수 있는 연산자로 `await`은 반환된 Promise가 **resolve 상태가 될 때 까지 대기**하며 Promise의 resolve 값이 반환된다. 즉, `await`을 사용하면 비동기 처리 처럼 실행되는 동안 다음 라인으로 넘어가는 것이 아니라, 실행이 완료될 때 까지 대기한다.

```javascript
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve("완료"),2000)
    });

    let result = promise.then((value) => console.log(value));
    console.log(result);
    console.log("Hi!");
}

f();
>>> Hi! 
    완료
```

위 예제는 `await`을 사용하기 위해 async function을 만들고 그 안에 비동기 처리를 할 수 있는 `Promise` 객체를 만들고 promise 변수에 할당하였다. 그리고 result에 promise로부터 받은 결과값을 할당하고 result 먼저 출력하고 그 다음 "Hi" 라는 문자열을 출력하였다. 결과는 비동기 처리로 인해 Hi, 완료 순으로 출력되었다. 그럼 다음 예제를 보자

```javascript
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve("완료"),2000)
    });

    let result = await promise;
    console.log(result);
    console.log("Hi!");
}

f();
>>> 완료
	Hi!
```

이번엔 `then` 대신 `await` 을 사용하였다. `then`을 사용하여 값을 받아왔을 때는 비동기 처리로인해 "Hi" 가 먼저 출력되었지만 `await`은 프로미스가 처리될 때 까지 함수 실행을 기다리게 하기 때문에 "완료" 라는 `resolve` 값을 받을 때까지 대기하였다. 따라서 ""완료""가 먼저 출력되고 "Hi!"가 그 다음에 출력되었다. 

<br>

#### await의 병렬처리

```javascript
// (ms / 1000)초 후에 Promise를 생성하는 함수
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

// 1초 후에 resolve 값으로 apple을 반환하는 async 함수
async function getApple() {
    await delay(1000);
    return 'apple';
}

// 1초 후에 resolve 값으로 banana를 반환하는 async 함수
async function getBanana() {
    await delay(1000);
    return 'banana';
}

// 함수가 실행되고 getApple() 함수가 끝나면 getBanana() 함수가 실행되고 그것마저 끝나면 resolve 값으로 apple + banana를 반환하는 async 함수
async function pickFruits() {
        const apple = await getApple();	// apple에는 getApple() 함수의 반환 값인 resolve값이 할당
        const banana = await getBanana(); // banana에는 getBanana() 함수의 반환 값인 resolve값이 할당
    return `${apple} + ${banana}`;
}

pickFruits().then(console.log);	>>> apple + banana // 총 2초 소요
```

위 예제에서 `getApple()` 함수와 `getBanana()` 함수는 서로 연관되어 있지 않은 함수인데도 불구하고 불필요하게 시간을 낭비하고있다. 이러한 단점을 보완하기 위해 `await` 을 병렬적으로 사용하는 것이 가능하다.

```javascript
async function pickFruits() {
    // Promise 객체가 동시에 생성됌
    const applePromise = getApple();
    const bananaPromise = getBanana();
    
    // 동시에 생성된 Promise 객체가 resolve를 반환할 때 까지 await
    const apple = await applePromise;
    const banana = await bananaPromise;
    
    return `${apple} + ${banana}`
}

pickFruit().then(console.log);	>>> apple + banana // 총 1초 소요
```

위와 같은 병렬 처리 방식은 Promise의 API를 이용하여 간단하게 할 수 있다.

<br>

#### all

프로미스 배열을 전달하게 되면 모든 프로미스들이 병렬적으로 다 받을 때 까지 모아준다.

```javascript
function pickAllFruits() {
    return Promise.all([getApple(), getBanana()]);
}
pickAllFruits().then(console.log); >>> ["apple", "banana"]

// 따라서 위에 병렬처리 방식을 사용한 예제를 다음과 같이 표현할 수 있다.
function pickAllFruits() {
    return Promise.all([getApple(), getBanana()])
    .then(fruits => fruits.join(' + '));
}
pickAllFruits().then(console.log);	>>> apple + banana
```



<br>

<br>

___

참고 : [드림코딩 엘리](https://www.youtube.com/watch?v=JB_yU6Oe2eE&t=1054s&ab_channel=%EB%93%9C%EB%A6%BC%EC%BD%94%EB%94%A9by%EC%97%98%EB%A6%AC) <br>

https://joshua1988.github.io/web-development/javascript/promise-for-beginners/ <br>

https://velog.io/@cyranocoding/2019-08-02-1808-%EC%9E%91%EC%84%B1%EB%90%A8-5hjytwqpqj<br>

https://pks2974.medium.com/javascript-%EC%99%80-async-await-111fdad3c20d<br>

https://ko.javascript.info/async-await

<br>

<br>


