## *transfrom*

엘리먼트의 크기, 회전, 비틀기와 같은 효과를 적용할 수 있다.

- scale : 요소를 확대 또는 축소할 수 있다.
- rotate : 요소를 회전시킨다.
- translate : 요소를 이동시킨다.

\>> [속성1](http://ianlunn.github.io/Hover/), [속성2](https://developer.mozilla.org/en-US/docs/Web/CSS/transform/) << 

<br>

## *transition*

- CSS의 속성을 변경할 때 애니메이션의 속도를 조절하는 방법을 제공한다. 속성 변화가 일정시간에 걸쳐 자연스럽게 일어날 수 있도록 한다.
- transition을 적용하기 위해 **두 가지**를 지정해줘야한다.  
  - **trasition-property** : 효과를 적용시킬 속성과 함께 시작시의 값과 완료시의 값 
  - **transition-duration** : 변화 하는데 걸리는 시간
- transition과 transform은 같이 사용되는 경우가 많다.
- **transition-property** : 변화를 주고자 하는 CSS 속성을 지정해준다. 복수의 값 지정 가능
  - none : 적용할 속성이 없음
  - all : 모든 속성에 변화 적용
  - 변화 줄 css속성 : 지정한 특정 속성에만 변화 적용
- **transition-duration** : 어느 정도의 시간 동안 변화를 줄 것인지 설정 (총 시간)
- **transition-delay** : 효과를 일정 시간 이후에 적용하도록 하는 것
- **transition-timing-function** : 장면 전환을 하는 시간을 가변적으로 설정
- **transition** :  transition-property, transition-duration, transition-timing-function, transition-delay 속성을 한 번에 정한다.

<br>

```css
<style>
    .box {
        background-color: aquamarine;
        height : 100px;
        width : 100px;
        transition-property : height,transform;
        transition-duration : 2s, 0.5s;
        transition-timing-function : ease-in-out;
    }

    .box:hover {
        height : 300px;
        transform : scale(0.5);
    }
</style>
```

div 태그로 만들어진 box에 마우스를 올려놓으면 높이가 300px이 되고, transform으로 요소의 크기가 반으로 되도록 애니메이션을 추가하였고, transition을 이용하여 마우스를 올려놓았을 때는 2초 동안, 마우스를 요소에서 거두었을 때는 0.5초 동안 애니메이션이 서서히 진행되도록 하였다. 결과는 다음과 같다.

![GIF](https://user-images.githubusercontent.com/68289543/103413938-0898cb00-4bbf-11eb-84aa-989d8b49df9e.gif)

<br>

<br>

___

참고 : inflearn 생활코딩 CSS

