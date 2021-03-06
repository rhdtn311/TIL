## *변수* 

- 숫자 또는 문자열과 같은 값의 컨테이너 ( 값 그 자체가 아님 )
- 변수 안에 포함된 값이 변경될 수 있다.

- 숫자, 문자 뿐만 아니라 함수와 같은 기능을 수행하는 것 까지 포함될 수 있다.

<br>

### *변수의 선언*

변수를 사용하기 위해 우선 변수 선언을 해야한다. 

JavaScript에서 변수는 var로 시작한다. var는 변수를 선언하겠다는 것을 위미하며 생랼 할 수도 있지만 유효범위라는 것에 영향을 미친다. 

변수는 $, _ , 특수문자를 제외한 모든 문자로 시작할 수 있다.

``` javascript 
var 변수명;
```

<br>

### *변수의 초기화*

변수를 선언한 후에는 값으로 초기화를 할 수 있다. 변수 이름 다음에 등호(=)와 값을 입력하여 초기화한다.

``` javascript
var myName;
myName = 'Chris';
```

변수를 선언함과 동시에 초기화 할 수 있다.

```javascript
var myName = 'Chris';
```

<br>

### *변수 이름 규칙*

변수의 이름은 임의로 규정할 수 있지만 제한이 있다. 일반적으로는 숫자(0~9), 대소문자 알파벳(a~z,A~Z) 과 밑줄 문자(_) 를 사용해야된다.

- 오류가 발생하거나 다른 사람이 이해하기 어려울 수 있으므로 다른 문자를 사용하면 안된다.
- 변수 이름의 시작 부분에 밑줄 문자(_) 를 사용하면 안된다. JavaScript 구문에서 밑줄문자로 시작하는 것은 특별한 의미를 가지고 있기 때문에 혼란을 가져올 수 있다.
- 변수 이름의 시작부분에 숫자를 사용하면 오류가 발생한다.
- 안전한 병법으로 "lower camel case" 문법을 사용한다. 여러 단어를 하나로 묶고 첫 단어의 시작은 소문자로 사용하며 그 다음 단어의 시작은 대문자로 사용한다. 
- 포함된 데이터를 쉽게 파악할 수 있도록 변수 이름은 직관적으로 사용한다.
- 변수는 대소문자를 구분한다. *(myage와 myAge는 다른 변수이다.)*
- JavaScript 예약어를 변수 이름으로 사용하면 안된다. (var, function, let, for 등)

<br>

### *변수의 종류* 

변수에 저장할 수 있는 데이터의 유형

<br>

#### 숫자

30과 같은 정수나 1.2323과 같은 부동소수점을 모두 변수에 저장할 수 있다. 다른 일부 언어들처럼 숫자 유형에 따른 다른 데이터 유형을 가지고 있지 않는다.

``` javascript
var myAge = 17;
```

<br>

#### 문자열

문자열은 텍스트로 변수에 문자열 값을 대입할 때 작은따옴표(')나 큰따옴표(")로 묶는다.

``` javascript
var dolphinGoodbye = "So long and thanks for all the fish";
```

<br>

#### 불리언(Booleans)

불리언(Booleans) 은 true 나 false 라는 값을 가지는 참/거짓을 표현하는 데이터 유형이다. 일반적으로 조건을 테스트 하는 데 사용된다.

```javascript
var iAmAlive = true;
```

일반적으로 다음과 같은 방식으로 더 많이 사용된다.

``` javascript
var test = 6 < 3;
```

위 코드는 6은 3보다 크므로 false를 반환한다.

<br>

#### 배열

배열은 대괄호로 묶이고 쉼표로 구분 된 여러 값을 포함하는 단일 객체이다.

```javascript
var myNameArray = ['Chirs','Bob','Jim'];
var myNumberArray = [10,15,40];
```

위와 같이 배열을 정의하고 그 안의 개별 값에 대해 접근할 수 있다.

```javascript
myNameArray[0];    >>> 'Chris'
myNumberArray[2];  >>> 40
```

배열 안의 값들은 0부터 인덱스 값이 지정되어 있다.

<br>

#### 객체

실제 사물을 모델링하는 코드 구조로 예를 들어 사람 객체는 이름, 키, 몸무게, 사용하는 언어 등의 정보를 가지고 표현 할 수 있다.

```javascript
var dog = { name : 'Spot', breed : 'Dalmatian'};
```

위와 같이 저장된 객체에 대한 정보를 검새갛기 위해서는 아래 구문을 사용한다.

```javascript
dog.name    >>> Spot
```

<br>

#### 지정되지 않은 타입

Javascript는 '느슨한 언어'이다. 즉, 다른 언어와 달리 변수에 포함될 데이터의 유형을 지정할 필요가 없다.

예를 들어 변수를 선언하고 그 변수의 값을 따옴표로 묶은 값을 지정하면 브라우저는 변수의 값을 문자열로 인식한다.;

``` javascript
var myString = "Hello"
```

따옴표 안에 숫자가 포함되어 있어도 문자열로 인식하기 때문에 주의해야한다.

``` javascript
var a = "10";
typeof(a);    >>> String
a = 10;
typeof(a)    >>> Number
```

<br>

## *숫자*

JavaScript는 다른 언어와 달리 수를 표현 하는데 있어 한 가지의 데이터 타입만을 가지고 있다. (Number)

(거대한 정수를 표현하는 BigInt 라는 숫자 타입이 있지만, 간단한 JavaScript에서는 Number만 사용해도된다.)

 <br>

#### *수의 타입*

JavaScript에서 변수에 정수를 대입하고, 부동소수점을 대입한 뒤 타입을 확인해보자

``` javascript
var myInt = 5;
var myFloat = 1.123;
typeof myInt;    >>> number
typeof myFloat;  >>> number
```

<br>

#### *수의 형변환*

수의 연산을 하기 위해서는 변수가 string이 아닌 number 형태로 선언되어야 한다. 그렇게 하기 위해서는 앞에서 살펴본 것대로 number 값을 변수에 대입하고 작은따옴표로 감싸는 실수를 하지 말아야한다.



```javascript
var myNumber = '74';
myNumber + 3;    >>> 743
```

위의 코드에서 myNumber 변수에 74를 대입했지만 작은따옴표로 감싸 string 형태이기 때문에 원하던 숫자의 연산 결과가 나오지 않는다. 따라서

``` javascript
var myNumber = 74;
muNumber+3;    >>> 77
```

<br>

## *산술연산자*

산술연산자는 JavaScript에서 연산을 할 수 있게해주는 기본적인 연산자이다.

- \+ (덧셈) : 수를 더해줌
- \- (뺄셈) : 연산자의 왼쪽 수에서 오른쪽 수를 빼줌
- \* (곱셈) : 두 수를 곱해줌
- / (나눗셈) : 연산자의 왼쪽 수를 오른쪽 수로 나눈 몫을 반환
- % (나머지) : 연산자의 왼쪽 수를 오른쪽 수로 나눈 후 나머지를 반환
- \** (지수) : 왼쪽수를 오른쪽 수만큼 거듭제곱 해준다. 
  - Math.pow() 메소드로도 표현할 수 있다. 

``` javascript
var num1 = 10;
var num2 = 20;
num1 + num2;    >>> 30
num1 * num2;    >>> 200
num2 / num1;    >>> 2
```

<br>

#### *산술연산자의 우선순위*

산술연산자의 우선순위는 사칙연산을 따른다. 따라서 곱셈 = 나눗셈 > 덧셈 = 뺄셈 순이 된다. 하지만 곱셈, 나눗셈보다 덧셈, 뺄셈을 먼저 연산하고 싶다면 ( ) 로 그 연산을 묶으면 먼저 수행된다.

```javascript
var num1 = 10;
var num2 = 20;
num1 + num2 * 2 - 40 >>> 10    // 우선순위에 따라 num2 * 2가 먼저 수행된다.
(num1 + num2) * 2 - 40 >>> 20    // 괄호로 묶어 주었기 때문에 num1+num2가 먼저 수행되어 값이 달라진다.
```

<br>

## *증감연산자*

증가 연산자는 피연산자를 증가 (1을 더해줌) 시키고 그 값을 반환한다.

- 피연산자 뒤에 증가연산자를 사용하면 (ex) x++) 증가 하기 전의 값을 반환하고 증가
- 피연산자 앞에 증가연산자를 사용하면 (ex) ++x) 증가한 후의 값을 반환한다.

``` javascript
var x = 3;
y = x++;    // y = 3, x = 4 

var a = 2;
b = ++a;    // a = 3, b = 3
```

<bar>

감소 연산자는 피연산자를 감소(1을 빼줌) 시키고, 그 값을 반환한다.

- 피연산자 뒤에 감소연산자를 사용하면(ex) x--) 감소하기 전의 값을 반환하고 감소
- 피연산자 앞에 감소연산자를 사용하면(ex)--x) 감소한 후의 값을 반환한다.

``` javascript 
var x = 3;
y = x--;    // y = 3, x = 2 

var a = 2;
b = --a;    // a = 1, b = 1 
```

<br>

## *할당연산자*

오른쪽 피연산자의 값을 왼쪽 피연산자의 값에 할당한다. 기본적인 할당 연산자는 오른쪽의 피연산자 값을 왼쪽 피연산자 값에 할당하는 등호(=) 이다.

복합 할당 연산자도 존재한다.

| 이름                              | 복합 할당 연산자 | 뜻          |
| --------------------------------- | ---------------- | ----------- |
| 할당                              | x = y            | x = y       |
| 덧셈 할당                         | x += y           | x = x + y   |
| 뺄셈 할당                         | x -= y           | x = x - y   |
| 곱셈 할당                         | x *= y           | x = x * y   |
| 나눗셈 할당                       | x /= y           | x = x / y   |
| 지수 연산 할당                    | x **= y          | x = x ** y  |
| 왼쪽 시프트 연산 할당             | x <<= y          | x = x << y  |
| 오른쪽 시프트 연산 할당           | x >>= y          | x = x >> y  |
| 부호 없는 오른쪽 시프트 연산 할당 | x >>>= y         | x = x >>> y |
| 비트 AND 할당                     | x &= y           | x = x & y   |
| 비트 XOR 할당                     | x ^= y           | x = x ^ y   |
| 비트 OR 할당                      | x \|= y          | x = x \| y  |

<br>

## *비교연산자*

비교 연산자는 피연산자들을 비교하고 그 결과에 따라 논리 값을 반환한다. 피연산자로는 숫자, 문자열, 논리형, 객체를 사용할 수 있다. 문자열은 유니코드 값을 사용하여 표준 사전순서를 기반으로 비교한다.

| 연산자                   | 설명                                                         | 참인 예제             |
| ------------------------ | ------------------------------------------------------------ | --------------------- |
| 동등 ( == )              | 피연산자들이 같으면 참을 반환한다.                           | 3=="3"<br />3==3      |
| 부등 ( != )              | 피연산자들이 다르면 참을 반환한다.                           | 3 != 4                |
| 일치 ( === )             | 피연산자들이 같고 피연산자들이 같은 형태인 경우 참을 반환한다. | 3 === 3               |
| 불일치 ( !=== )          | 피연산자들이 다르거나 형태가 다른 경우 참을 반환한다.        | 3 !== "3"             |
| ~보다 큰 ( > )           | 좌변의 피연산자가 우변의 피연산자보다 크면 참을 반환한다.    | 10 > 1                |
| ~보다 크거나 같음 ( >= ) | 좌변의 피연산자가 우변의 피연산자와 같거나 더 크면 참을 반환한다. | 10 >= 1<br />10 >= 10 |
| ~보다 작음 ( < )         | 좌변의 피연산자가 우변의 피연산자보다 작으면 참을 반환한다.  | 1 < 10                |
| ~보다 같거나 작음 ( <= ) | 좌변의 피연산자가 우변의 피연산자와 같거나 더 작으면 참을 반환한다. | 1 <= 10<br />1 <= 10  |

<br>

### *== VS ===* 

== 와  ===는 둘 다 양쪽 피연산자가 같은지 다른지를 비교하는 연산자이지만 서로 구체적으로 다른 성질을 가지고 있다.

' == ' 는 서로 다른 유형의 두 변수의 [값]을 비교하며

' === ' 는 [값] 과 [자료형] 모두 비교한다.

ex ) 

1. number 타입의 숫자와 string 타입의 숫자를 비교

```javascript
10 == "10"    >> true  

10 === "10"   >> false  // 10의 타입은 number이고, "10"의 타입은 string이기 때문에 false
typeof(10)    >> number
typeof("10")  >> string
```



2. 숫자와 boolean 을 비교

``` javascript 
0 == false    >>> true   // 0값은 false를 나타내기 때문에 true

0 === false   >>> false  // 0의 타입은 number이고 false의 타입은 boolean이기 때문에 false
typeof(0)     >>> number
typeof(false) >>> boolean  
```

 

3. null 과 undefined 를 비교

``` javascript
null == undefined    >>> true

null === undefined   >>> false
typeof(null)    // object
typeof(undefined)    // undefined
```



4. NaN ( Not a Number) 과 비교

``` javascript
NaN == NaN    >>> false
NaN === NaN   >>> false
```

NaN은 어느 것과도 같지 않다.


참고 : https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/Variables
