# 탐색 (Search)

저장된 정보들 중에서 원하는 값을 찾는 것

<br>



## *순차 탐색 (Sequential Search)*

- 가장 기본적인 탐색 방법

- 리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 차례로 확인하는 방법

- 일반적으로 정렬되어 있지 않은 리스트에서 데이터를 찾아야 할 때 사용한다.

- 리스트 내에 데이터가 아무리 많아도 시간만 충분하다면 항상 원하는 데이터를 찾을 수 있다.

  

```python
# 순차탐색
# n: 원소의 개수, target: 찾고자 하는 데이터, array: target이 있는 리스트
def sequential_search(n,target,array) :
    for i in range(n) :
        if array[i] == target :
            retrun i+1
```

- 데이터의 개수가 N개일 때 시간복잡도 : O(N) (최악의 경우)

<br>

## *이진 탐색(Binary Search)*

- 배열 내부의 데이터가 **정렬되어 있어야만** 사용할 수 있는 알고리즘
- 탐색 범위를 절반씩 좁혀가며 데이터를 탐색한다.
- 이진 탐색은 위치를 나타내는 변수 3개를 사용하는데 탐색하고자 하는 범위의 **시작점, 끝점, 중간점**이다.
- 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는다.

### ex)

### 0  2  <span style="color:red">4</span>  6  <span style="color:blue">8</span>  10  12  14  16  18 중 원소 4를 찾는다고 가정해보자.

1. 배열에서 시작점, 끝점을 확인한 다음 **중간점을 정한다.** 

   위 예에서 시작점은(0) 끝점은 (18)이다. 중간점은 한 가운데 인덱스로 (0+9)/2 = 4.5 번째 인덱스를 가지는 값이 중간점인데, 

   이렇게 실수일 때는 소수점을 버린다. 위 예에서는 [4]번 인덱스인 8이 중간점이다.

2.  그 다음 중간점과 찾으려는 데이터를 비교한다.

   &nbsp;8과 4를 비교하여 중간점 8이 더 크므로 중간점 이후의 값은 확인할 필요가 없다.

 &nbsp;  따라서 끝점을 [4]번째 인덱스에서 [3]번 째 인덱스로 바꾼다.

### 0  <span style="color:blue">2</span>  <span style="color:red">4</span>  6&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;~~8  10  12  14  16  18~~

3. 이제 시작점은 [0]번 인덱스, 끝점은 [3]번 인덱스가 되었다.

   따라서 중간점은 (0+3)/2 = 1.5 -> [1]번 인덱스인 2가 된다.

   여기서 중간점 2는 찾으려는 값인 4보다 작으므로 이번에는 값이 2 이하인 데이터를 더 이상 확인할 필요가 없다.(데이터는 오름차순으로 정렬 되어있기 때문)

   따라서 시작점을 [2]번 인덱스로 변경한다.

### ### ~~0  2~~&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="red">4</font>  6 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;~~8  10  12  14  16  18~~

4. 시작점은 [2]번 인덱스인 4, 끝점은 [3]번 인덱스인 6이다. 이 때 중간점은 [2]번 인덱스인 4이다. 중간점에 위치한 데이터 4는 찾으려는 데이터 4와 동일하므로 이 시점에서 탐색을 종료한다.

</br>

- 전체 데이터의 개수는 10개지만 이진 탐색을 이용하여 총 3번의 탐색으로 원소를 찾을 수 잇었다.
- **시간 복잡도 : O(logN)**
  - 한 번 확인할 때 마다 확인해야 할 원소의 개수가 절반씩 줄어들기 때문
- 이진 탐색의 코드는 재귀함수를 이용한 방법과 반복문을 이용하는 방법이 있다.

```python
def binary_search(array,target,start,end) :
    if start>end : 
        return None
    mid = (start+end)//2
    
    if array[mid] == target : # 값을 찾은 경우 중간점 인덱스를 반환
        return mid+1
    if array[mid] > target : # 중간점의 값이 찾고자 하는 값보다 크다면 배열을 축소
        return binary_search(array,target,start,mid-1)
    elif array[mid] < target : # 중간점의 값이 찾고자 하는 값보다 작다면 배열을 축소
        return binary_search(array,target,mid+1,end)
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;재귀 함수를 이용한 방법

```python
def binary_search(array,target,start,end) : 
    while start <= end : 
        mid = (start+end) // 2
        if target == array[mid] :
            print(mid+1)
            return
        elif target > array[mid] :
            start = mid+1
           else : 
            end = mid - 1
    return None
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;반복문을 이용한 방법
<br>

- 코딩테스트에서의 이진탐색 문제는 **탐색 범위가 큰 상황**에서의 탐색을 가정하는 문제가 많다.
  - 따라서 탐색 범위가 2000만을 넘어가면 이진 탐색으로 접근



## *트리 자료구조* 

- **노드와 노드의 연결**로 표현하며 여기에서 노드는 정보의 단위로서 어떠한 정보를 가지고 있는 개체이다.
- 트리 자료구조는 그래프 자료구조의 일종으로 데이터베이스 시스템이나 파일 시스템과 같은 곳에서 많은 양의 데이터를 관리하기 위한 목적으로 사용한다.
- 트리 자료구조의 특징
  - 트리는 부모 노드와 자식 노드의 관계로 표현
  - 트리의 최상단 노드를 **루트 노드**라고 한다.
  - 트리의 최하단 노드를 **단말 노드**라고 한다.
  - 트리에서 일부를 떼어내도 트리 구조이며 이를 서브트리라고 한다.
  - 트리는 파일 시스템과 같이 **계층적**이고 **정렬된 데이터**를 다루기에 적합하다.

<br>

## *이진 탐색 트리*

- 트리 자료구조 중에서 가장 간단한 형태
- 이진 탐색 트리의 특징
  - 모든 노드의 키 (데이터 값)은 유일하다. (중복이 없다.)
  - 왼쪽 서브트리의 키들은 루트의 키보다 작다.
  - 오른족 서브트리의 키들은 루트의 키보다 크다.
  - 왼쪽과 오른쪽의 서브트리도 이진 탐색 트리이다. (부모 노드의 자식노드 중 왼쪽은 부모 노드보다 작고 오른쪽은 부모 노드보다 크다.)

<br>

### 이진 탐색 트리에서 데이터를 조회하는 과정 



![img](https://lh6.googleusercontent.com/zN0WA2afG5ZXFEHt6QMv2d_T6ZBtgsRJDWRtEyxiwihI6WpxhhpoP3SWwCGRR3aLqLaRozqCwLctNDhjiqaFnsG23q016a_iHGdD2KwJwG66WyWry54ON5YFDgMUj0vURgm-X92X)

찾고자 하는 데이터는 37이다.

![K-006](https://user-images.githubusercontent.com/68289543/98771575-1f753980-2428-11eb-9975-c6f870338c52.png)

1. 이진 탐색 트리는 루트 노드부터 방문한다.
2. 찾는 노드의 값은 37인데 루트 노드의 값이 30이므로 왼쪽은 배제하고 오른쪽 서브루틴으로 이동한다.

![K-009](https://user-images.githubusercontent.com/68289543/98771582-2439ed80-2428-11eb-864a-bd0d876eba5e.png)

3.  그로 인해 48이 부모노드가 되었다.

4. 48이 찾는 노드의 값 37보다 크기 때문에 오른쪽 서브루틴은 배제하고 왼쪽 서브루틴만 확인한다.

![K-008](https://user-images.githubusercontent.com/68289543/98771586-2603b100-2428-11eb-806a-6bf32164ad5d.png)

5. 찾는 값인 37보과 방문 노드의 값이 동일하다. 탐색을 종료한다.

