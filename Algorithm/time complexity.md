#  시간복잡도

알고리즘을 잘 설계하기 위해서 

1. 해결할 문제의 특성을 이해해야 한다.
2. **시간**과 공간 사이의 상충 관계를 이해해야한다. 
3. 위를 바탕으로 적절한 **자료 구조**를 선택해야 한다. 

<br>

결국 좋은 알고리즘을 구현하기 위해서는 알고리즘을 수행하는데 최소한의 시간을 걸리도록 구현하는 것이 중요하다. 시간복잡도는 특정한 크기의 입력에 대하여 알고리즘이 얼마나 오래 걸리는지를 의미한다. 알고리즘에서 시간복잡도는 알고리즘의 실행시간에 크게 좌우하는 연산을 중점적으로 계산한다. 시간복잡도를 표기하는 표기법은 다음과 같다.

- 최악의 경우 : 빅오 표기법 (Big-O Notation)
- 보통의 경우 : 세타 표기법 (Big-θ Notation)
- 최상의 경우 : 오메가 표기법 (Big-Ω Notation)

이 중에서 코딩테스트에서 최악인 경우인 빅오 표기법을 사용하여 알고리즘의 시간복잡도를 판단한다.

<br>

##  Big-O 표기법

빅오 표기법은 알고리즘의 복잡도를 표기하는 방법으로 코드의 실제 러닝 타임을 표시하는 것은 아니며 input data의 증가율에 따른 알고리즘의 성능을 논리적으로 예측하기 위해 사용한다. 빅오 표기법에는 다음과 같은 규칙이 있다.

1. 가장 높은 차수만 남긴다.  

2. 계수 및 상수는 과감하게 버린다. 

![1](https://user-images.githubusercontent.com/68289543/101932743-987dd180-3c1e-11eb-9b3e-c4133bce2a30.gif)

다음은 빅오표기법으로 나타낸 시간복잡도의 표이다. 가파를 수록 시간복잡도가 크다.

![K-053](https://user-images.githubusercontent.com/68289543/101931156-64091600-3c1c-11eb-997b-27f5404e64aa.png)

- ![O(1)](https://user-images.githubusercontent.com/68289543/101933513-a97b1280-3c1f-11eb-82c7-4c8ddf8aae86.gif) (상수 시간)

  입력 데이터의 크기에 상관없이 일정한 시간이 걸리는 알고리즘

  ```python
  a = 1 
  print("Hi")
  ```

- ![O(logN)](https://user-images.githubusercontent.com/68289543/101933493-a08a4100-3c1f-11eb-8a52-910af54dacd4.gif) (로그 시간)

  입력 데이터의 크기가 커질 수록 처리 시간이 로그만큼 짧아지는 알고리즘 (데이터가 10배가 되면 처리 시간은 2배가 됌)

- ![O(N)](https://user-images.githubusercontent.com/68289543/101933496-a122d780-3c1f-11eb-91ed-0505b704e4e5.gif) (선형 시간)

  입력 데이터의 크기에 비례하여 처리 시간이 증가하는 알고리즘 (데이터가 10배가 되면 처리 시간도 10배가 됌)

  ```python
  for i in range(n) : 
      print(i)
  ```

- ![O(nlogn)](https://user-images.githubusercontent.com/68289543/101933501-a1bb6e00-3c1f-11eb-8f33-20a0dd2103a6.gif) (선형 로그 시간)

  입력 데이터의 크기가 커질 수록 처리시간이 로그 배 만큼 커지는 알고리즘 ( 데이터가 10배가 되면 처리 시간은 약 20배가 됌)

- ![O(n^2)](https://user-images.githubusercontent.com/68289543/101933497-a1bb6e00-3c1f-11eb-8235-8b24d0e56648.gif) (이차 시간)

  입력 데이터의 크기가 커질 수록 처리 시간이 급수적으로 늘어나는 알고리즘 ( 데이터가 10배가 되면 처리 시간은 100배가 됌)

  ```python
  for i in range(n) : 
      for j in range(n) : 
          print(i,j)
  ```

- ![O(2^n)](https://user-images.githubusercontent.com/68289543/101933502-a2540480-3c1f-11eb-8253-07b441e2eeb8.gif) (지수 시간)

  입력 데이터의 크기가 커질 수록 처시 시간이 기하급수적으로 늘어나는 알고리즘 

<br>

#### 암기할 것

1.  sort() : ![O(nlogn)](https://user-images.githubusercontent.com/68289543/101933501-a1bb6e00-3c1f-11eb-8f33-20a0dd2103a6.gif)

2. Hashmap에 접근 : ![O(1)](https://user-images.githubusercontent.com/68289543/101933513-a97b1280-3c1f-11eb-82c7-4c8ddf8aae86.gif) 

   Hashmap 구축 : ![O(N)](https://user-images.githubusercontent.com/68289543/101933496-a122d780-3c1f-11eb-91ed-0505b704e4e5.gif) 

3.  이진 탐색 : ![O(logN)](https://user-images.githubusercontent.com/68289543/101933493-a08a4100-3c1f-11eb-8a52-910af54dacd4.gif) 

4. heap 

   - heap에 삽입 : ![O(logN)](https://user-images.githubusercontent.com/68289543/101933493-a08a4100-3c1f-11eb-8a52-910af54dacd4.gif)
   - 길이가 n인 배열을  heap으로 생성 : ![O(nlogn)](https://user-images.githubusercontent.com/68289543/101933501-a1bb6e00-3c1f-11eb-8f33-20a0dd2103a6.gif)
   - 우선순위 최대인 값을 pop : ![O(logN)](https://user-images.githubusercontent.com/68289543/101933493-a08a4100-3c1f-11eb-8a52-910af54dacd4.gif)

<br>

<br>

참고 )

-  https://www.notion.so/a3ba1c7dd40b489ab7ea89dc3a18503a

  https://velog.io/@raram2/big-o-notation-and-time-complexity
