## Localstorage

로컬 스토리지(Local Storage)는 데이터를 브라우저에 저장하는 저장소이다. 웹 페이지의 세션이 끝나도 데이터가 지워지지 않는 특성을 가지고 있으며, 읽기 전용 프로퍼티이다. 로컬 스토리지는 다음과 같은 특징을 가지고있다.

- 자바스크립트로 조작 가능하다.
- 키(key)와 값(vlaue) 쌍으로 구성되어 있다.
- 값은 반드시 문자열(string)으로 저장된다.

<br>

#### APIs

***setItem***

`setItem()`은 로컬 스토리지에 데이터를 저장한다.

```javascript
localStorage.setItem(키, 값);	// syntax

localStorage.setItem("Kong", 26);
```

![image](https://user-images.githubusercontent.com/68289543/104345747-08df8180-5542-11eb-8bf8-68e04a785a0b.png)

<br>

***getItem***

`getItem()`은 로컬 스토리지에 저장된 값을 불러온다.

```js
localStorage.getItem('키') -> '값'이 반환됌 // syntax

const name = localStorage.getItem('Kong');
console.log(name);	// 1
```

<br>

***removeItem***

`removeItem()`은 로컬 스토리지에 저장된 데이터를 삭제한다.

```js
localStorage.removeItem('키') //syntax

localStorage.removeItem('Kong');
```

![image](https://user-images.githubusercontent.com/68289543/104346402-b8b4ef00-5542-11eb-9f59-e4d64634e27b.png)

<br>

***clear***

`clear()`은 로컬 스토리지에 저장된 모든 데이터를 삭제한다.

```js
localStorage.clear();
```

<br>

<br>

___

참고 : [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
