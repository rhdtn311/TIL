# JSON

Javascript Object Notation의 약자로 ECMAScript 3rd에서 쓰여지는 오브젝트에서 영감을 받아 제작된 데이터 포멧이다. 그렇기 때문에 자바스크립트에서 오브젝트를 나타낼 때와 같이 {Key:Value}로 이루어져 있다.

Json은 다음과 같은 특징을 가지고있다.

- **데이터를 주고 받을 때 사용할 수 있는 가장 간단한 파일 포멧**
- **텍스트를 기반으로한 가벼운 구조**
- **읽기 쉽다.**
- **키-값쌍으로 이루어져있는 파일 포멧**
- **네트워크 간 데이터 직렬화 및 전송에 사용**
- **프로그래밍 언어 및 플랫폼에 상관없이 사용 가능**



```Json
{
    "class" : [
        {
            "name" : "Kong",
            "age" : 26,
            "number" : 2015177223
        },
        {
            "name" : "Kim",
            "age" : 25,
            "number" : 2014256789
        },
        {
            "name" : "Park",
            "age" : 21,
            "number" : 2019122455
        }
    ]
}
```



<br>

### *JSON 문법*

#### 리터럴 (literal)

리터럴은 해석되는 값 그 자체를 의미한다.

```json
10	// 숫자 리터럴
"Kong"	// 문자 리터럴
true	// 불리언 리터럴
```

<br>

#### 객체 (Object)

객체는 실생활에서 우리가 인식할 수 있는 사물을 의미한다.

JSON에서 객체는 키(key)와 값(value) 쌍으로 구성된 정렬되지 않은 집합이다.

```json
{
    "name" : "Park",
    "height" : 182,
    "weight" : 68
}
```

<br>

### *JSON 구조*

JSON은 자바스크립트 객체 표기법에서 영감을 받아 만들어졌기 때문에 자바스크립트 객체 표기법에 따른 구조로 구성된다.

1. JSON 데이터는 **키, 값 쌍**으로 이루어진다.
2. JSON 데이터는 쉼표(,)로 나열된다.
3. **객체(object)** 는 중괄호({})로 둘러싸여 표현한다.
4. **배열(array)** 은 대괄호([])로 둘러싸여 표현한다.

<br>

#### 데이터

JSON 데이터는 키 값의 쌍으로 구성되며 데이터 이름(키), 콜론(:), 값의 순서로 구성된다.

```Json
"데이터 키(key)" : 값(value)
```

데이터 이름도 문자열이기 때문에 큰타옴표(" ")와 함께 입력해야 한다.

데이터의 값으로는 다음과 같은 타입이 올 수 있다.

1. 숫자 (number)
2. 문자열 (string)
3. 불리언 (boolean)
4. 객체 (object)
5. 배열 (array)
6. NULL

<br>

#### [객체](https://github.com/rhdtn311/TIL/new/main/JavaScript#%EA%B0%9D%EC%B2%B4-object)

중괄호로 싸여 표현되며, 위에 적어놓은 내용과 같다.

<br>

#### 배열

JSON 배열은 대괄호([])로 둘러싸여 표현한다. 쉼표(,)를 사용하여 여러 JSON 데이터를 포함할 수 있다.

```js
"Arsenal" : [
    {"name" : "Partey", "age" : 27, "position" : "midfielder"},
    {"name" : "Saka", "age" : 20, "position" : "foward"},
    {"name" : "Gabriel", "age" : 21, "position" : "Defend"}
]
```

<br>

### *JSON의 사용

JSON은 데이터를 교환하기위하여 생성된 데이터 교환 표준이기 때문에 다음 두 가지에 유의하여 공부해야한다.

1. 객체를 직렬화 하여 JSON으로 변환
2. 직렬화된 JSON을 객체로 다시 변환



#### 객체를 JSON으로 변환

***JSON.stringify()*** 함수를 이용한다.

```js
// boolean 값을 JSON으로 변환
let json = JSON.stringify(true);
console.log(json)	

>>> true

// 배열을 JSON으로 변환
json = JSON.stringify(['Kong','Kim']);
console.log(json);	

>>> ["apple","banana"]

// 객체를 JSON으로 변환
const Kong = {
    age : 26,
    car : null,
    birthDate : new Date(),
    ability : () => {
        console.log('${this.name} can fight!');	// 함수는 객체에 있는 데이터가 아니기 때문에 JSON으로 변환되지 않는다.
    }
};
json = JSON.stringify(Kong);
console.log(json)

>>> {"age":26,"car":null,"birthDate":"2021-01-01T04:00:56.347Z"}
```

<br>

#### JSON을 객체로 변환

***JSON.parse()*** 함수를 이용한다.

```js
json = JSON.stringfy(Kong);	// 객체를 JSON으로 변환하여 json에 저장
const obj = JSON.parse(json);	// JSON으로 저장된 json을 객체로 변환하여 obj에 저장

console.log(obj)

>>> {age: 26, car: null, birthDate: "2021-01-01T04:17:18.075Z"}
```

위 예제에서 Kong이라는 객체에는 ability 라는 함수가 들어가있었지만 JSON으로 바꾸고 다시 객체로 변환하게 되면 함수가 사라진다. 

<br>

<br>

___

참고 : [드림코딩 엘리](https://www.youtube.com/watch?v=FN_D4Ihs3LE&ab_channel=%EB%93%9C%EB%A6%BC%EC%BD%94%EB%94%A9by%EC%97%98%EB%A6%AC), [TCP School](http://www.tcpschool.com/json/intro)

