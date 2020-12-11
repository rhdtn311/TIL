# 배열 

배열(array)은 연관된 데이터를 모아서 관리하기 위해 사용하는 데이터 타입이다. 변수가 하나의 데이터를 저장하기 위한 것이라면 배열은  여러 개의 데이터를 하나의 변수에 저장하기 위한 것이다. 자바스크립트에서 배열의 길이와 데이터의 자료형은 고정되어 있지 않다. 그렇기 때문에 배열의 길이가 언제든지 늘어나거나 줄어들 수 있다.

<br>

## *배열선언* 

```javascript
var array = [item1, item2, ... , item]
```

<br>

## *인덱스*

배열 안의 요소들은 인덱스로 구분할 수 있는데 배열의 왼쪽 요소부터 차례대로 0번 인덱스, 1번 인덱스, ... ,  n번 인덱스( 배열의 원소수가 n+1) 로 표현되며 잘못된 인덱스를 사용하면 undefined를 반환한다.

```javascript
var music = ['classic', 'newage', 'hiphop']

music[0]    >>> classic
music[2]    >>> hiphop
```

<br>

## *length*

length는 배열의 길이를 구하는 매소드이다.

```javascript
var music = ['classic', 'newage', 'hiphop']

music.length    >>> 3
```



자바스크립트에서는 처음 지정한 배열의 범위를 넘어가는 속성을 입력한다면 length의 크기는 그만큼 커진다. 

```javascript
var music = ['classic', 'newage', 'hiphop']
music.length    >>> 3

var music[4] = 'pop'	// ['classic', 'newage', 'hiphop', , 'pop']
music.length    >>> 5
```

length를 직접 늘릴 수도 있다.

```javascript
var music = ['classic', 'newage', 'hiphop']
music.length = 5;    >>> 5
```

length의 크기를 줄이면 배열 안의 데이터가 삭제된다.

```javascript
var music = ['classic', 'newage', 'hiphop']
music.length = 2;

music    >>> ['classic', 'newage']
```

<br>

## *배열 요소 추가*

#### push

push() 메서드는 하나 이상의 요소를 배열의 마지막에 추가하고 추가된 요소를 포함하여 반환한다.

```javascript
var music = ['classic', 'newage', 'hiphop']
music.push('pop', 'r&b');

document.write(music);    >>> ['classic', 'newage', 'hiphop', 'pop', 'r&b']
```

<br>

#### concat

concat() 메서드는 두 개의 배열을 합쳐 새로운 배열을 반환한다. 

``` javascript
var music = ['classic', 'newage', 'hiphop']
var new_music = music.concat('pop','r&b');

document.write(music);    >>> ['classic', 'newage', 'hiphop']
document.write(new_music) >>> ['classic', 'newage', 'hiphop', 'pop', 'r&b']
```

<br>

#### unshift

unshift() 메서드는 배열의 앞에 새로운 요소를 추가하고 추가된 요소를 포함하여 반환한다.

```javascript
var music = ['classic', 'newage', 'hiphop']
music.unshift('pop','r&b');

document.write(music)    >>> ['pop', 'r&b', 'classic', 'newage', 'hiphop']
```

<br>

## *배열 요소 제거*

#### pop

pop() 메서드는 배열의 마지막 요소를 제거하고 제거된 요소를 반환한다.

```javascript
var music = ['classic', 'newage', 'hiphop']
music.pop();

document.write(music);    >>> ['classic', 'newage']
```

<br>

#### shift

shift() 메서드는 배열의 첫 번째 요소를 제거하고 제거된 요소를 반환한다.

```javascript
var music = ['classic', 'newage', 'hiphop']
music.shift();

document.write(music);    >>> ['newage', 'hiphop']
```

<br>

#### splice

splice( 시작 인덱스, 시작 인덱스부터 삭제할 데이터의 수(n),  추가할 배열 ) 는 시작 인덱스부터 n개 만큼의 데이터를 삭제하고 추가할 배열들을 배열에 추가한다.

```javascript
var music = ['classic', 'newage', 'hiphop']
music.splice(1,2,'pop','r&b');

document.write(music);    >>> ['classic','pop','r&b']
```

<br>

#### slice

slice(시작 인덱스, 마지막 인덱스) 는 시작 인덱스를 포함하여 마지막 인덱스 전 까지 (마지막 인덱스는 포함하지 않는다.) 의 데이터들을 t새로운 배열로 반환한다.

```javascript
var music = ['classic', 'newage', 'hiphop']
var new_music = music.slice(1,3);

document.write(music)      >>> ['classic','newage', 'hiphop']
document.write(new_music)  >>> ['newage','hiphop']
```

<br>

## *배열의 정렬*

#### sort

sort()는 배열의 데이터들을 오름차순으로 정렬한다. 알파벳의 경우 a부터 순서대로 오름차순으로 정렬하며 대문자가 소문자보다 앞쪽으로 정렬된다. 아스키코드를 기준으로 정렬되기 때문에 위와 같이 정렬되는 것이다. 숫자는 크기순으로 오름차순이 아니라 1부터 9까지 앞이 1인 것부터 9인 것 까지 정렬된다.

```javascript
var num = [5,4,2,1,3,10,11,20]
var str = ['D','b','E','A','z','C']
num.sort();
str.sort();

document.write(num)    >>> [1,10,11,2,20,3,4,5]
document.write(str)    >>> ['A','C','D','E','b','z']
```
sort함수는 인자로 함수를 받을 수 있는데 이 함수는 **콜백함수**라고 한다. **sort(compareFunction(a,b))** 는 다음과 같은 원리로 정률 순서가 결정된다.

- *compareFunction(a,b) 의 값이 0보다 작은 경우 a가 b보다 먼저 정렬된다.*
- *compareFunction(a,b) 의 값이 0이면 a와 b의 순서를 변경하지 않는다.*
- *compareFunction(a,b) 의 값이 0보다 큰 경우 b가 a보다 먼저 정렬된다.*

``` javascript
var num = [5,4,2,1,3,10,20,11]

function asc(a,b) {	// 오름차순
    return a-b
}

function desc(a,b) {	// 내림차순
    return b-a
}

num.sort(asc)	>>> [1,2,3,4,5,10,11,20]
num.sort(desc)	>>> [20,11,10,5,4,3,2,1]
```

위 코드에서 함수 asc는 배열의 원소인 a에서 b를 뺀 후 그 값이 양수이면 b가 a 앞에 정렬될 것이고, 음수이면 a가 b 앞에 정렬될 것이다. 함수 desc에서는 배열의 원소인 b에서 a를 뺀 후 그 값이 양수이면 b가 a 앞에 정렬될 것이고, 음수이면 a가 b 앞에 정렬될 것이다.

<br>
<br>

#### reverse

reverse() 는 배열의 데이터들의 순서를 거꾸로 뒤집는다.

```javascript
var num = [2,3,6,5,3,4]

num.reverse() 
document.write(num)    >>> [4,3,5,6,3,2]
```

<br>
<br>
참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Indexed_collections <br>
       inflearn 생활코딩 자바스크립트 기본
