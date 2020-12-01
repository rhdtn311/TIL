## *탐색* 
- 많은 양의 데이터 중에서 원하는 데이터를 찾는 과정
- 대표적인 탐색 알고리즘으로 DFS와 BFS가 있음
<br>

## *자료구조*
 - 데이터를 표현하고 관리하고 처리하기 위한 구조
 - 대표적으로 스택, 큐가 있음 
	 - **스택의 핵심 함수** : 
		 - **삽입 (Push)** : 데이터를 삽입한다.
		 - **삭제(Pop)** : 데이터를 삭제한다.
	 - **스택의 오버플로와 언더플로** : 
		 - **오버플로** : 특정한 자료구조가 수용할 수 있는 데이터의 크기를 이미 가득 찬 상태에서 삽입 연산을 수행할 때 발생
		 - **언더플로** : 특정한 자료구조 에 데이터가 전혀 들어가있지 않은 상태에서 삭제 연산을 수행하면 언더플로 발생
<br>
		
## *스택* 
- LIFO 방식으로 후입선출 방식이라고 한다.
- 박스 쌓기와 같이 먼저 들어간 데이터가 가장 나중에 나오는 자료구조
``` python
start = []

stack.append(1)
stack.append(2)
stack.append(3)

stack.pop()
stack.pop()

print(stack)

>>> [1]		# 가장 먼저 들어간 1이 가장 마지막에 삭제됌
``` 
<br>

## *큐*
- FIFO 방식의 선입선출 구조 알고리즘
- 줄 서는 것과 같이 먼저 들어간 데이터가 가장 먼저 나오는 방식
``` python
from collections import deque

queue = deque()

queue.append(1)
queue.append(2)
queue.append(3)
queue.append(4)

queue.popleft()
queue.popleft()

queue.reverse()

print(queue)

>>> deque([4, 3])  # 가장 나중에 삽입된 4가 맨 앞에 위치
```
- 위 코드에서 append 대신에 appendleft() 함수를 사용하면 reverse()를 해주지 않아도 된다.
- deque는 스택과 큐의 장점을 모두 채택한 것인데 데이터를 넣고 빼는 속도가 리스트 자료형에 비해 효율적이며 queue 라이브러리를 이용하는 것보다 더 간단하다.

<br>

## *재귀함수* 
- 자기 자신을 다시 호출하는 함수

``` python 
def recursive_function() : 
	print("재귀 함수를 호출합니다.)
	recursive_function()
	
recursive_function()	>>> "재귀 함수를 호출합니다." 라는 말이 무한 반복된다.
```
**재귀 함수를 문제 풀이에서 사용할 때는 재귀 함수가 언제 끝날지 종료 조건을 꼭 명해줘야한다. 위와 같이 무한 호출을 할 수 있기 때문이다.**
<br>
``` python
def  recursive_function(i) :
	if i == 3 :
	return

	print(i, "번째 재귀 함수에서 ", i+1 ,"번째 재귀함수를 호출합니다.")	
	recursive_function(i+1)
	print(i,"번째 재귀 함수를 종료합니다.")
	
recursive_function(1)
>>> 1 번째 재귀 함수에서 2 번째 재귀함수를 호출합니다.
	2 번째 재귀 함수에서 3 번째 재귀함수를 호출합니다.
	2 번째 재귀 함수를 종료합니다.
	1 번째 재귀 함수를 종료합니다.
```

- 위 코드로 미루어 보았을 때 재귀 함수의 수행은 **스택 자료구조**를 이용한다는 것을 알 수 있다. 이유는 함수를 계속 호출 했을 때 가장 마지막에 호출한 함수가 먼저 수행을 끝내야 그 앞의 함수 호출이 종료되기 때문이다.
- 따라서 스택 자료구조를 사용해야하는 상당수 알고리즘은 재귀 함수를 이용하여 간편하게 구현될 수 있다. (DFS)
- 재귀함수를 이용하는 대표적인 예제는 **팩토리얼(n!) 문제**가 있다.
-    아래 예는 일반적인 반복문으로 팩토리얼을 구현한 것과 재귀함수로 구현한 것이다.
<br>

*<일반적인 for문>*
``` python
result = 1
n = 5

for i in  range(1,n+1) :
result *= i

print(result) >>> 120
```
<br>

*<재귀함수를 이용>*
``` python
def  factorial_recursive(n) :
	if n<=1 :
	return  1

	return n * factorial_recursive(n-1)

print(factorial_recursive(5)) >>> 120
```
<br>

-   재귀 함수를 이용한 방법을 단계별로 살펴보면

	factorial+recursive(5)<br>
	= 5 x factorial_recursive(4)<br>
	= 5 x 4 x factorial_recursive(3)<br>
	= 5 x 4 x 3 x factorial_recursive(2)<br>
	= 5 x 4 x 3 x 2 x factorial_recursive(1)<br>
	= 5 x 4 x 3 x 2 x 1<br>
	= 120

- 두 방법은 실행결과는 같지만 재귀 함수를 사용했을 때 더 간결한 코드를 얻을 수 있다. 이유는 재귀 함수가 수학의 점화식(재귀식) 을 그대로 소스코드로 옮겼기 때문이다. 점화식은 특정한 함수를 자신보다 더 작은 변수에 대한 함수와의 관계로 표현한 것이다. 팩토리얼을 수학적 점화식으로 표현하면 다음과 같다.
1.  n이 0 혹은 1일 때 : factorial(n) = 1
2.  n이 1보다 클 때 : factorial(n) = n x factorial(n-1)
