## Element.classList

`Element.classList`속성은 자바스크립트의 DOM 객체의 클래스를 조작할 수 있다. `className`은 요소에 클래스가 존재하지 않는다면 추가하고 있으면 기존 클래스를 변경하지만, classList를 이용하면 새로운 클래스를 추가하거나 제거할 수 있다.

<br>

| 메서드                | 설명                                             |
| --------------------- | ------------------------------------------------ |
| `add('클래스 명')`    | 입력한 클래스를 추가한다.                        |
| `remove('클래스 명')` | 입력한 클래스를 제거한다.                        |
| `toggle('클래스 명')` | 입력한 클래스가 있으면 제거하고 없으면 추가한다. |



> 예시

버튼 3개를 만들어 각각 `add()`를 이용하여 클래스를 추가하고, `remove()`를 이용하여 클래스를 지우고, `toggle()`을 이용하여 클래스를 추가하거나 지운다. 



``` html
// HTML

<body>
    <h1 class = "btnOne">Click me !</h1>
    <span><button id ="addbtn">add</button></span>
    <span><button id = "removebtn">remove</button></span>
    <span><button id = "togglebtn">toggle</button></span>
</body>
```




```CSS
//CSS

.btnOne {
  color: royalblue;
}

.btnTwo {
  color: salmon;
}
```




```javascript
//Javscript

const click = document.querySelector('.btnOne');
const addButton = document.querySelector('#addbtn');
const removeButton = document.querySelector('#removebtn');
const toggleButton = document.querySelector('#togglebtn');

function add() {
    click.classList.add('btnTwo');
}

function remove() {
    click.classList.remove('btnTwo');
}

function toggle() {
    click.classList.toggle('btnTwo');
}

addButton.addEventListener("click",add);
removeButton.addEventListener("click",remove);
toggleButton.addEventListener("click",toggle);
```

<result>

![GIF](https://user-images.githubusercontent.com/68289543/104093109-bdbc3900-52cb-11eb-946b-cbb12d8c248b.gif)

___

참고 : [MDN](https://developer.mozilla.org/ko/docs/Web/A
