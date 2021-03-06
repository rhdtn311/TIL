# 다이나믹 프로그래밍

- 연산속도를 비약적으로 증가시킬 수 있는 방법
- 특정 조건이 성립해야 사용 가능
  - 큰 문제를 작은 문제로 나눌 수 있다.
  - 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일하다.

<br>


### *피보나치 문제*

![예시](https://user-images.githubusercontent.com/68289543/99351325-b5efa200-28e3-11eb-99bb-bf849df88943.png)

이전 두 항의 합을 현재의 항으로 설정하는 수열로 위와 같은 형태로 끝없이 이어진다.

피보나치 수열의 점화식은 다음과 같이 나타낼 수 있다.

![점화식](https://user-images.githubusercontent.com/68289543/99351327-b720cf00-28e3-11eb-9cdf-addfa4555f9a.png)

이를 해석하면 다음과 같다.

- *n번째 피보나치 수 = (n-1)번째 피보나치 수 +(n-2)번째 피보나치 수*
- *단, 1번째 피보나치 수 = 1 , 2번째 피보나치 수 = 1* 

이를 파이썬 코드로 나타내면 다음과 같이 간단하게 나타낼 수 있다.

<br>

``` python
def fibo(x) :
    if x == 1 or x == 2 :
        return 1
    return fibo(x-1) + fibo(x-2)
```

그런데 이렇게 소스코드를 작성하면 심각한 문제가 생긴다. x의 값이 커질수록 수행시간이 기하급수적으로 늘어나기 때문이다. 

위 코드의 시간복잡도는 일반적으로 빅오 표기법을 이용하여 $O(2^n)$ 의 지수 시간이 소요된다고 표현한다.

![피보나치](https://user-images.githubusercontent.com/68289543/99347733-247c3200-28db-11eb-9380-6d1e0d8f421b.png)

x=5 일 때 호출 과정을 그림으로 보면 위와 같다.

F(3)이 2번 호출된 것을 볼 수 있다. 이미 한 번 계산했지만, 계속 호출할 때마다 계산하는 것이다.

즉,  F(N)에서 N의 크기가 커질수록 반복해서 호출하는 수가 많아진다.

피보나치 수열은 앞서 말한 다이나믹 프로그래밍의 구현 조건을 만족하는 대표적인 예이다.

이 문제를 **메모이제이션 (Memoization) 기법**을 통해 해결해볼 수 있다.

<br>

메모이제이션은 다이나믹 프로그래밍을 구현하는 방법 중 한 종류로, 한 번 구한 결과를 메모리 공간에 메모해두고 같은 식을 다시 호출하면 메모한 결과를 그대로 가져오는 기법을 의미한다. 메모이제이션은 값을 저장하는 방법이므로 캐싱이라고도 한다.

메모이 제이션은 한 번 구한 정보를 리스트에 저장하는 방법으로 구현할 수 있다. 다이나믹 프로그래밍을 재귀적으로 수행하다가 같은 정보가 필요할 때는 이미 구한 정답을 그대로 리스트에서 가져오면 된다. 소스코드로 나타내면 다음과 같다.

```python
# 한 번 계산된 결과를 메모이제이션(Memoization)하기 위한 리스트 초기화
d = [0] * 100

# 피보나치 함수를 재귀함수로 구현 (탑다운 다이나믹 프로그래밍)
def fibo(x) :
    # 종료 조건 (x=1 혹은 x=2일 때 1을 반환)
    if x == 1 or x == 2 :
        return 1
    # 이미 계산한 적 있는 문제라면 그대로 반환
    if d[x] != 0 :
        return d[x]
    # 아직 계산하지 않은 문제라면 점화식에 따라서 피보나치 결과 반환
    d[x] = fibo(x-1) + fibo(x-2)
    return d[x]
```

<br>

정리 하자면 다이나믹 프로그래밍이란,

**큰 문제를 작게 나누고, 같은 문제라면 한 번씩만 풀어 문제를 효율적으로 해결하는 알고리즘 기법**이다.

<br>

- 시간 복잡도 : O(N)
  - F(1) 을 구한 다음 그 값이 F(2)를 푸는 데 사용되고, F(2)의 값이 F(3)을 푸는 데 사용되는 방식으로 이어지기 때문

<br>

### *다이나믹 프로그래밍과 분할 정복 알고리즘 차이*

- 다이나믹 프로그래밍은 문제들이 서로 영향을 미치고 있다는 점이 가장 큰 차이점이다.
  - 퀵 정렬은 한 번 기준 원소(Pivot)가 자리를 변경해서 자리를 잡게 되면 피벗의 위치는 더 이상 바뀌지 않고 그 피벗값을 다시 처리하는 부분 문제는 존재하지 않는다.
  - 반면에 다이나믹 프로그래밍은 한 번 해결했던 문제를 다시금 해결한다는 점이 특징이다. 그렇기 때문에 이미 해결된 부분 문제에 대한 답을 저장해 놓고, 이 문제는 이미 해결 했던 것이니까 다시 해결할 필요가 없다고 반환하는 것이다.

<br>

### *Top-Down & Bottom-Up*

- 위 피보나치 수열 구현 소스코드 처럼 재귀 함수를 이용하여 다이나믹 프로그래밍 소스코드를 작성하는 방법을, 큰 문제를 해결하기 위해 작은 문제를 호출한다고 하여 **Top-Down 방식**이라고한다.
- 반면에 단순히 반복문을 이용하여 소스코드를 작성하는 경우 작은 문제부터 차근차근 답을 도출한다고 하여 **Bottom-Up 방식**이라고 한다.
  - Bottom-Up 방식에서 사용되는 결과 저장용 리스트는 DP 테이블이라고 부른다. ( 메모이제이션은 Top-Down 방식에 국한)

```python
// Bottom-Up 방식의 피보나치 수열 소스코드

n = int(input())	// n번째 피보나치 수열을 구하기 위해 입력받음
d = [0] * 100	// DP 테이블 초기화

d[1] = 1
d[2] = 1

for i in range(3, n + 1) :
    d[i] = d[i - 1] + d[i - 2]	// 피보나치 함수를 반복문으로 구현

print(d[n])
```

<br>

<br>

---


참고 : 이것이 코딩테스트다 with 파이썬 (나동빈)
