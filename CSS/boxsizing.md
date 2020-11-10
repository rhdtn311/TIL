# box-sizing 



CSS 박스 모델의 기본 값에서, 지정한 너비와 높이는 요소의 콘텐츠 박스 크기에만 적용된다. 즉 요소에 테두리나 안쪽 여백이 있으면 너비와 높이에 더해서 화면에 그려진다.

따라서 크기를 설정할 때, 원하는 크기를 얻으려면 테두리(border)나 안쪽여백(padding) 값을 고려해야 한다.



이 과정이 번거롭다면 box-sizing 속성을 이용하면 쉽다.

</br>

## *box-sizing : content-box*

기본 CSS 박스 크기 결정법을 사용한다. 

요소의 너비를 100px로 설정하면 콘텐츠 영역이 100px 너비를 가지고, border과 padding 값은 이에 더해진다.

즉,

``` css
.box {
    box-sizing : content-box;
    width: 350px;
    border: 10px solid black;
}
```

의 width 값은 370px이다. ( 350 + 10 + 10 )

</br>

## box-0sizing : border-box 

width 와 height 속성이 padding과 border을 포함하고 margin은 포함하지 않는다.

즉,

```css
.box {
    box-sizing : border-box;
    width : 350px;
    border : 10px solid black;
    padding : 5px;   
}
```

을 적용한 width의 값은 350px이다.

요소의 크기는 

너비 = 테두리(border) + 안쪽여백(padding) + 콘텐츠 너비,

높이 = 테두리(border) + 안쪽여백(padding) +콘텐츠 높이 

로 계산한다.



</br>

<img src="https://cssgurubd.files.wordpress.com/2015/01/box-model_css2_vs_css3.png">
