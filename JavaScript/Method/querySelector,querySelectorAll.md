## querySelector()

`.querySelector()`는 css 선택자로 요소를 선택한다. 한 개의 요소만 선택할 수 있으며 동일한 이름의 선택자를 가진 객체가 있을 경우 html 문서 내에서 첫 번째 요소를 선택한다. 일치하는 요소가 없으면 null을 반환한다.



> 예제 1

```html
<body>
    <div class="classOne">This is querySelector 1 </div>
    <div class="classOne">This is querySelector 2 </div>
    <div class="classOne">This is querySelector 3 </div>
    <script>
        document.querySelector(".classOne").style.color="blue";
    </script>
</body>
```

![image](https://user-images.githubusercontent.com/68289543/103983165-28844c00-51c8-11eb-99f2-d84749d875c3.png) 



> 예제 2

``` html
<body>
    <div class="classOne">This is querySelector 1 </div>
        <section>
            <div class="classOne">This is querySelector 2 </div>
        </section>
    <div class="classOne">This is querySelector 3 </div>
    <script>
        document.querySelector("section .classOne").style.color="blue";
    </script>
</body>
```

![image](https://user-images.githubusercontent.com/68289543/103983600-dbed4080-51c8-11eb-8523-44410ba53dba.png) 

<br>

## querySelectorAll()

`querySelectorAll()`은 특정 CSS 선택자를 가진 모든 요소를 선택한다. 이 때 반환 타입은 **리스트 타입**이다. 따라서 인덱스를 이용하여 제어할 수 있다.



> 예제 1

``` html
<body>
    <div class="classOne">This is querySelector 1 </div>
    <div class="classOne">This is querySelector 2 </div>
    <div class="classOne">This is querySelector 3 </div>
    <script>
        const selector = document.querySelectorAll(".classOne");
        selector[1].style.color = "blue";
        selector[2].style.color = "red";
    </script>
</body>
```

![image](https://user-images.githubusercontent.com/68289543/103984186-012e7e80-51ca-11eb-935f-0c835eda3b55.png) 

> 예제 2

```html
<body>
    <div class="classOne">This is querySelector 1 </div>
    <div class="classOne">This is querySelector 2 </div>
    <div class="classOne">This is querySelector 3 </div>
    <script>
        const selector = document.querySelectorAll(".classOne");
        for (var i = 0; i < selector.length; i++) {
            selector[i].style.color = "green"
        }
    </script>
</body>
```

![image](https://user-images.githubusercontent.com/68289543/103984478-92055a00-51ca-11eb-8ed4-b202bb3df231.png) 

<br>

<br>

___

참고 : https://www.codingfactory.net/10410
