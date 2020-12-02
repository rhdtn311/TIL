# 반복문

반복문은 한 동작을 여러번 반복한다. 여러 종류의 반복문이 존재한다.



## *while문*

주어진 조건이 참(ture) 이라면 문장을 반복한다.

```javascript
while (조건) {
    문장;
}
```

while문이 반복되다가 조건이 거짓(false) 이 된다면 while문을 멈추고 빠져나온다.

<br>



#### 예시)

```javascript
while (true) {
    document.write("Hi");
}

>>> "Hi" 라는 문자열이 끊임없이 출력된다. (무한루프)
```



위 코드와 같이 반복문이 끊임 없이 출력되어 무한루프에 빠지지 않기 위해 조건문에는 아래와 같이 false 값을 유도하도록 조건문이 작성된다.



#### 예시2)

```javascript
var i = 0;

while (i < 5) {
    document.write(i);
    i++;
}

>>> 01234 가 출력된다.
```



<br>



## *for문*

for문은 어떤 특정한 조건이 거짓으로 판별될 때까지 반복한다. 



```javascript
for ( 초기값; 조건문; 증감문 ) {
    문장;
}
```



for문은 다음과 같은 과정으로 실행된다.

1. 초기값 ( 변수, 구문 ) 이 대입된다. 
2. 조건문이 참, 거짓을 판별한다. 조건문이 참이라면 문장이 실행되고 거짓이라면 for문은 종료되어 빠져나온다. 조건문이 생략된다면 참으로 추정된다.
3. 문장이 끝나면 증감문을 통해 값을 증가시키거나 감소시킨다.
4. 2번 단계로 넘어간다.



#### 예시

```javascript 
for (i = 0; i < 5; i++) {
    document.write(i);
}

>>> 01234 
```



<br>



## *Break & Continue*

***break문***은 반복문, switch문 등 결합되어있는 문장을 빠져나올 때 사용한다.



#### 예시

```javascript
for (i = 0; i < 5; i++) {
    if (i === 3) {
        break;			// i === 3 일 때 for문이 빠져나옴
    }
    document.write(i);
}

>>> 012 
```

<br>

continue문은 반복문 중 건너띄고 싶을 때 사용할 수 있다.



#### 예시

```javascript
for (i = 0; i < 5; i++) {
    if (i === 3) {
        continue;		// i === 3 일 때 이 부분에서 아래 문장을 실행하지 않고 증감문을 수행하여 i값을 증가시킴 
    }
    documnet.write(i);
}

>>> 0124
```

