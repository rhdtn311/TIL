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

## *배열 요소 검색*

**indexOf, lastIndexOf**

원하는 데이터의 인덱스를 검색한다.

- indexOf : 원하는 데이터의 첫 번째 인덱스를 검색한다.
- lastIndexOf : 원하는 데이터의 마지막 인덱스를 검색한다.

```javascript
array = ["닭", "토끼", "뱀", "호랑이","닭"]

console.log(array.indexOf("닭"));	>>> 0 
console.log(array.indexOf("강아지"));	>>> -1
console.log(array.lastIndexOf("닭"));	>>> 4
```

찾는 데이터가 배열 안에 없으면 -1을 출력한다.

<br>

**includes**

원하는 데이터가 배열 안에 포함 되어 있는지 검색하여 있으면 true, 없으면 false를 반환한다.

```javascript
array = ["닭", "토끼", "뱀", "호랑이"]

console.log(array.includes("닭"));	>>> true
console.log(array.includes("강아지"));	>>> false
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

unshift() 메서드는 배열의 앞에 새로운 요소를 추가하고 추가된 요소를 포함하여 반환한다. unshift는 배열 내 데이터들을 반복하여 이동시켜야 하기때문에 push보다 훨씬 느리다. 

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

shift() 메서드는 배열의 첫 번째 요소를 제거하고 제거된 요소를 반환한다. shift는 배열 내 데이터들을 모두 하나씩 움직여야 하기 때문에 pop보다 훨씬 느리다.

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

## *배열 요소를 하나씩 출력*

배열 내의 요소들을 하나씩 출력하는 방법에는 여러가지가 있다.

```javascript
array = [1,2,3]

// 기본적인 for문
for (let i = 0; i < array.length; i++) {
    console.log(array[i]);
}
>>> 1
	2
	3

// for of
for (let i of array) {
    console.log(i);
}
>>> 1
	2
	3
```

for문과 for of를 이용하는 방법 외에 forEach 함수를 이용하는 방법도 있다. forEach함수는 인자로 콜백함수를 받는데 그 콜백함수의 파라미터로 (요소,  인덱스, 배열전체) 를 받는다.

```javascript
array = ["닭","토끼","뱀"]

// for Each 
array.forEach(function (value, index, array) {
    console.log(value);
})
>>> 닭
    토끼
    뱀

array.forEach(function (value, index, array) {
    console.log(index);
})              
>>>	0
	1
	2
              
array.forEach(function (value, index, array) {
    console.log(array);
})
>>> ["닭","토끼","뱀"]
    ["닭","토끼","뱀"]
    ["닭","토끼","뱀"]

// for Each를 Arrow Function으로 표현
array.forEach((value) => console.log(value));
>>>	닭
	토끼
    	뱀
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

### *배열에 관한 유용한 APIs*

#### join

배열에 있는 모든 요소들을 더해서 string으로 출력해준다.

```javascript
const food = ['김밥', '떡볶이', '피자'];

const join_food = food.join();
console.log(join_food);	>>> "김밥,떡볶이,피자"

// 파라미터로 구분자를 전달할 수 있다.
const sepjoin_food = food.join('and');
console.log(sepjoin_food);	>>> "김밥and떡볶이and피자"
```

<br>

#### split

첫 번째 인자로 받은 구분자로 나누어 문자열을 배열로 바꾸어준다.

```javascript
const food = '김밥,떡볶이,피자';

const split_food = food.split(',');
console.log(split_food)	>>> ['김밥', '떡볶이', '피자']

// 두 번째 인자로 한계치를 정할 수 있다.
const limitsplit_food = food.split(',',2);
console.log(limitsplit_food);	>>> ['김밥','떡볶이']
```

<br>

#### reverse

배열 내 요소들을 거꾸로 뒤집는다.

```javascript
const num = [1,2,3,4,5];

const reverse_num = num.reverse();
console.log(reverse_num);	>>> [5,4,3,2,1]

// reverse는 기존 배열 자체를 변화시킨다.
console.log(num);	>>> [5,4,3,2,1]
```

<br>

#### find

인자로 전달된 콜백 함수가 true인 배열의 **첫 번째 원소**를 반환한다. 콜백함수의 파라미터로 (요소, 인덱스, 배열) 을 받는다.

```javascript
const num = [1,10,30,50,99]

const find_num = num.find(function(value) {return value > 50});
console.log(find_num)	>>> 99

const wrongFind_num = num.find((value) => value > 100);	
console.log(wrongFind_num)	>>> undefined
```

<br>

#### filter

인자로 전달된 콜백 함수가 true인 **모든 원소**를 배열로 반환한다. 콜백함수의 파라미터로 (요소, 인덱스, 배열)을 받는다.

```javascript
const num = [10,20,30,44,89,90,100];

const filter_num = num.filter((value) => value > 50);
console.log(filter_num);	>>> [89, 90, 100]
```

<br>

#### map

배열 안에 들어있는 요소들을 각각 콜백함수의 return값 따라 변환하고 변환된 값으로 이루어진 새로운 배열을 반환해준다.

```javascript
const num = [1,2,3,4,5,10];

let map_num = num.map((value) => value + 1);
console.log(map_num);	>>> [2,3,4,5,6,11]
console.log(num);	>>> [1,2,3,4,5,10]

let map_num = num.map((value) => {
    if (value % 2 === 0) {
        return '짝수';
    }
    else {
        return '홀수';
    }
});
console.log(map_num);	>>> ["홀수", "짝수", "홀수", "짝수", "홀수", "짝수"]
```

<br>

#### some

배열의 요소 중에서 some의 첫 번째 인자로 사용되는 콜백함수의 리턴 값이 true가 되는 요소가 있는지 확인해준다.

```javascript
const num = [1,2,3,4,5,10];

let some_num = num.some((value) => value > 9);
console.log(some_num);	>>> true

let some_num = num.some((value) => value > 10);
console.log(some_num)	>>> false
```

<br>

#### every

배열의 요소 중 every의 첫 번째 인자로 사용되는 콜백함수의 리턴 값이 모든 요소들이 true가 되는지 확인해준다.

```javascript
const num = [5,6,7,8,9];

let every_num = num.every((value) => value > 4);
console.log(every_num);	>>> true

let every_num = num.every((value) => value > 5);
console.log(every_num);	>>> false
```

<br>

#### reduce

모든 배열을 순회하며 요소들을 return 값을 기준으로 누적시킨다. reduce는 다음과 같은 형태를 띈다.

배열.reduce((누적값, 현재값, 인덱스, 요소) => {return 결과값}, 초기값);

```javascript
const num = [1,2,3,4,5];

// prev는 누적 값, curr은 현재 배열의 요소이다.
// 여기서 초기 값은 0번 인덱스 값인 1이고, 
let sum_num = num.reduce((prev,curr) => prev + curr);
console.log(sum_num);	>>> 15

// 여기서 ,5는 초기값이다. 초기 값으로부터 시작하여 0번째 인덱스부터 값을 빼주며 누적시킨다.
let sub_num = num.reduce((prev,curr) => prev - curr,15);
console.log(sub_num);	>>> 0
```

**reduceRight**은 배열의 뒤부터 순회를 시작한다.

<br>

___

참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Indexed_collections <br>
       inflearn 생활코딩 자바스크립트 기본
