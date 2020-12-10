# 정규표현식

특정한 규칙을 가진 문자열의 집합을 표현하는데 사용하는 형식 언어. 많은 텍스트 편집기와 프로그래밍 언어에서 문자열의 검색과 치환을 위해 지원하고 있다.

<br>

## *정규표현식의 사용*

컴파일과 실행 단계로 이루어진다.

<br>

#### 컴파일

어떤 작업을 하기 위해서 문자를 치환 하거나 혹은 문자의 유무를 판단 하는 등 일련의 작업을 하기 위해 우리가 필요한 대상을 찾는 것 (= 패턴을 찾는 것)

<br>

#### 실행

우리가 찾은 패턴(대상)에 대하여 어떠한 구체적인 작업을 하는 것

<br>

### *정규표현식 객체 생성*

우리가 찾고자하는 것(a)을 pattern 이라는 변수를 통해 사용할 수 있게 된다.

```javascript
var pattern = /a/;
```

```javascript
var pattern = new RegExp('a');
```

둘 다 같은 의미를 가지고 있다. (= 우리가 찾고자하는 정보(a)를 pattern 이라는 변수에 저장했다.)

<br>

### *정규표현식 메소드 실행*

정규표현식으로 하는 대표적인 작업은 다음과 같다.

- 원하는 정보를 **추출**
- 필요로 하는 정보가 있는지 **테스트**
- 검색된 정보를 다른 정보로 **치환**

정규표현식을 컴파일해서 객체를 만들었다면 이제 문자열에서 원하는 문자를 찾아내야한다.



#### RegExp.exec()

정규표현식이 찾고자하는 대상을 첫 번째 인자로  전달하여 패턴이 찾는 정보를 대상에서 찾아서 있으면 배열로 반환해주는 메소드(**추출**)

```javascript
var pattern = /a/;		// 찾고자하는 정보(a)를 pattern이라는 변수에 넣음

console.log(pattern.exec('a'));		// exec라는 메소드를 사용하여 패턴에 맞는 문자열을 탐색	>>> [a]
console.log(pattern.exec('bcdef')); // 원하는 패턴(a)가 없으므로 >>> null
```



#### RegExp.test()

검색의 대상이 되는 첫 번째 인자 안에 우리가 찾고자하는 패턴이 존재한다면 boolean 값으로 반환해주는 메소드(**테스트**)

```javascript
var pattern = /a/;

console.log(pattern.test('abcde'));		>>> true
console.log(pattern.test('bcdef'));		>>> false
```

<br>

### *문자열 메소드 실행*

문자열에서 정규표현식 메소드와 같이 사용할 수 있는 메소드가 있다.



#### String.match()

찾고자하는 정보가 대상 **문자열**에 존재한다면 그 값을 배열로 반환해주는 메소드

```javascript
var pattern = /a/;

console.log('abcde'.match(pattern));		>>> [a]
console.log('bcdef'.match(pattern));		>>> null
```



#### String.replace()

찾고자하는 정보가 대상 문자열에 존재한다면 그 값을 원하는 값으로 치환하여 문자열로 반환해주는 메소드

``` javascript
var pattern = /a/;

console.log('abcde'.replace(pattern,'A'));		>>> 'Abcde'
console.log('bcedf'.replace(pattern,'A'));		>>> 'bcedf'
```

<br>

### *특수문자를 이용햔 정규표현식 표현*

#### \

**일반 문자** 앞에 사용시 이스케이프 문자로 해석하고 **특수 문자** 앞에 사용시 특수 문자를 통해 새로운 기능을 수행하는 것이 아닌 특수 문자 그대로 문자열처럼 해석된다. ( 예를들어 /a\*/는 정규표현식에서 a로 시작하는 0개 이상의 문자열을 뜻하지만 /a\\*/는 문자열 "a\*" 그 자체를 뜻한다.)

```javascript
var pattern = /a\*/

console.log('bcda*'.match(pattern));		>>> ['a*']
```

<br>

#### ^

정규표현식에서 입력의 시작 부분에 대응된다.

```javascript
var first = /^a/

console.log("cbad".match(first))		>>> null
console.log("acbad".match(first))		>>> ["a"]
```

<br>

#### $

정규표현식에서 입력의 끝 부분에 대응된다.

```javascript
var last = /a$/

console.log("abcd".match(last));		>>> null
console.log("bcda").match(last));		>>> ["a"]
```

<br>

#### *

바로 앞의 문자가 0번 이상 나타나는 경우를 검색한다. (/{0,}/ 와 같다. )

```javascript
var zeroTo = /ap*/		// 문자 'a' 다음 문자 'p'가 0번 이상 나타나는지 탐색

console.log("I like apple".match(zeroTo));		>>> ["app"]
console.log("I like avocado".match(zeroTo));	>>> ["a"]

var zeroTo = /app*/		// 문자 'ap' 다음 문자 'p'가 0번 이상 나타나는지 탐색
console.log("I like apple".match(zeroTo));		>>> ["app"]
console.log("I like avocado".match(zeroTo));	>>> null

var zeroTo = /ap*p*/	// 문자 'a' 다음 문자 'p'가 0번 이상, 문자 'p' 0번 이상 나타나는지 탐색
console.log("I like apple".match(zeroTo));		>>> ["app"]
console.log("I like avocado".match(zeroTo));	>>> ["a"]
```

<br>

#### +

바로 앞의 문자가 1번 이상 나타나는 경우를 검색한다. (/{1,}/ 와 같다.)

```javascript
var oneTo = /ap+/

console.log("I like apple".match(oneTo));		>>> ["app"]
console.log("I like avocado".match(oneTo));		>>> null

var oneTo = /av+c+/
console.log("I like avocado".match(oneTo));		>>>	null

var oneTo = /av+o+/
console.log("I like avocado".match(oneTo))l		>>> ["avo"]
```

<br>

#### ?

바로 앞의 문자가 0 또는 1번만 나타나는 경우를 검색한다. (/{0,1}/ 와 같다.)

```javascript
var oneTo = /ab+/
var zeroOne = /ab?/

console.log("abbbbb".match(oneTo));		>>> ["abbbbb"]
console.log("abbbbb".match(zeroOne));	>>>	["ab"]
```

<br>

#### \d , \D

\d는 숫자를 검색하고 \D는 숫자가 아닌 모든 문자를 검색한다.

<br>

#### \w, \W

\w는 영문자, 숫자, 언더바를 검색한다. [A-Za-z0-9_] 과 동일하다.

\W는 영문자, 숫자, 언더바를 제외한 문자를 검색한다.

<br>

#### \s

띄어쓰기, tab, 줄바꿈 등 공백문자를 제외한 모든 문자를 검색한다.

<br>



### *정규표현식의 옵션*

정규표현식 패턴을 만들 때 옵션을 설정할 수 있으며 옵션 설정을 통해 검출되는 데이터를 달리할 수 있다.

#### i

문자를 찾을 때 대소문자를 구분하지 않도록 하는 옵션

```javascript
var pattern = /a/;
var useI = /a/i;	// i 옵션을 적용

console.log(pattern.exec("ABCDE"));		>>> null
console.log(useI.exec("ABCDE"));		>>> ["A"]
```

<br>

#### g

global의 약자로 패턴과 일치하는 모든 문자열을 배열로 반환해준다.

```javascript
var pattern = /a/;
var useG = /a/g;

console.log('abcda'.match(pattern));		>>> ['a']
console.log('abcda'.match(useG));		>>> ['a','a']
```

<br>
<br>
<br>
정규표현식이 헷갈릴 때 직관적으로 참고할 수 있는 사이트 : https://regexr.com/
<br>
참고 :<br> 
inflearn 생활코딩 javascript<br>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions

