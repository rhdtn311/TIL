# Event

이벤트란, 웹 브라우저가 알려주는 HTML 요소에 대한 어떠한 사건이 발생함을 의미한다. 자바스크립트를 이용하여 발생한 이벤트에 반응하여 특정 동작을 수행할 수 있다.

## *Event listener*

**이벤트 리스너**는 이벤트가 발생하였을 때 처리를 담당하는 함수이다. 지정된 타입의 이벤트가 특정 요소에서 발생하면 웹 브라우저는 그 요소에 등록된 이벤트 리스너를 실행시킨다.



#### addEventListener()

`addEventListener()` 메소드는 대부분의 브라우저에서 지원하는 이벤트 리스너 등록을 위한 메소드이다.

```javascript
대상객체.addEventListener(이벤트 명, 이벤트 리스너, 이벤트 전파 방식)

// 이벤트 명 : 이벤트 리스너를 등록할 이벤트 타입을 문자열로 전달한다. 
// 이벤트 리스너 : 지정된 이벤트가 발생했을 때 실행할 이베트 리스너를 전달한다.
// false면 버블링(bubbling) 방식으로, true면 캡처(capturing)링 방식으로 이벤트를 전달한다.
```

**이벤트 목록**

| 이벤트 명 | 설명                                     |
| --------- | ---------------------------------------- |
| change    | 변동이 있을 때 발상                      |
| click     | 클릭 시 발생                             |
| focus     | 포커스가 되었을 때 발생                  |
| keydown   | 키가 눌렸을 때 발생                      |
| keyup     | 키에서 손을 땟을 때 발생                 |
| load      | 로드가 완료 되었을 때 발생               |
| mousedown | 마우스를 클릭 했을 때 발생               |
| mouseout  | 마우스가 특정 객체 밖으로 나갔을 때 발생 |
| mouseover | 마우스가 특정 객체 위로 올려졌을 때 발생 |
| mousemove | 마우스가 움직였을 때 발생                |
| select    | option 태그 등에서 선택을 했을 때 발생   |



> 예시

```html
<body>
    <h2>Click me !</h2>
    <script>
        const tag= document.querySelector('h2');
        tag.addEventListener("mouseover",() => { tag.style.color = "red"});
    </script>
</body>

```

![GIF](https://user-images.githubusercontent.com/68289543/104092111-26ec7e00-52c5-11eb-83ab-9b987bf8634e.gif)

<br>

<br>

___

참고 : https://chlolisher.tistory.com/10

http://www.tcpschool.com/javascript/js_event_eventListenerRegister

