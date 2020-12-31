## *overflow*

overflow 속성은 요소 내의 컨텐츠가 너무 커서 요소 내에 모두 보여주기 힘들 때 어떻게 보여줄지를 지정한다. 일반적으로 컨텐츠를 포함하고 있는 요소의 크기가 고정되어 있지 않다면 컨텐츠를 모두 포함할 수 있도록 요소의 크기가 거지지만, 크기가 고정 되어 있다면  overflow 속성에 지정된 값에 따라 보여지게 된다.



- visible : 기본 값으로, 컨텐츠의 크기가 넘칠 경우 상자 밖으로 보여진다.
- hidden : 넘치는 부분은 잘려서 보이지 않는다.
- scroll : 스크롤 바가 추가되어 스크롤 할 수 있다.
- auto : 컨텐츠 크기에 따라 스크롤 바를 추가할지 자동으로 결정된다.



```css
.box {
    background-color:cornflowerblue;
    height : 200px;
    width : 150px;
    overflow : visible | hidden | scroll | auto ;
}
```

***\<visible>***

![image](https://user-images.githubusercontent.com/68289543/103414559-d5a40680-4bc1-11eb-96db-ceb9948eaf33.png)

***\<hidden>***

![image](https://user-images.githubusercontent.com/68289543/103414643-1a2fa200-4bc2-11eb-9003-17f2df6c98f2.png)

***\<scroll>***

![GIF](https://user-images.githubusercontent.com/68289543/103414694-5400a880-4bc2-11eb-84d1-d039f5f213af.gif)

***\<auto>***

![GIF](https://user-images.githubusercontent.com/68289543/103414738-89a59180-4bc2-11eb-886c-13e041253603.gif)

auto는 컨텐츠와 요소의 크기를 확인하고 스크롤이 필요하면 필요한 부분만 (가로 or 세로) 자동으로 추가해준다. 

<br>

<br>

___

참고 : https://developer.mozilla.org/ko/docs/Web/CSS/overflow
