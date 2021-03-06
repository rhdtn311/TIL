# 그래프 이론 

그래프란 노드와 노드 사이에 연결된 간선의 정보를 가지고 있는 자료구조이다.

### *트리* 

- 다양한 알고리즘에서 사용되기 때문에 꼭 기억해야 할 자료구조
- 우선순위 큐에서 최소 힙이 트리 자료구조에 속한다.
  - 최소 힙(Min heap) : 항상 부모 노드가 자식 노드보다 크기가 작은 자료구조
- 부모에서 자식으로 내려오는 계층적인 모델
- 전통적인 수학에서는 무방향 그래프에 속하지만, 컴퓨터공학 분야에서는 방향 그래프라고 간주된다.



|                     | 그래프                         | 트리             |
| ------------------- | ------------------------------ | ---------------- |
| 방향성              | 방향 그래프 혹은 무방향 그래프 | 방향 그래프      |
| 순환성              | 순환 및 비순환                 | 비순환           |
| 루트 노드 존재 여부 | 루트 노드가 없음               | 루트 노드가 존재 |
| 노드간 관계성       | 부모와 자식 관계 없음          | 부모와 자식 관계 |
| 모델의 종류         | 네트워크 모델                  | 계층 모델        |

<br>

### *그래프의 구현 방법*

- **인접 행렬 (Adjacency Matrix)** : 2차원 배열을 사용하는 방식
- **인접 리스트(Adjacency :List)** : 리스트를 사용하는 방식
  - \>>> [인접 행렬, 인접 리스트](https://github.com/rhdtn311/TIL/blob/main/Algorithm/BFS,DFS.md#dfs%EC%99%80-bfs%EC%9D%98-%EC%8B%9C%EA%B0%84%EB%B3%B5%EC%9E%A1%EB%8F%84) <<<

- 다익스트라 최단 경로 알고리즘 : 인접 리스트를 이용

  - 노드의 개수가 V개일 때는 V개의 리스트를 만들어서 각 노드와 연결된 모든 간선에 대한 정보를 리스트에 저장함.

- 플로이드 워셜 알고리즘 : 인접 행렬을 이용

  - 모든 노드에 대하여 다른 노드로 가는 최소 비용을![image](https://user-images.githubusercontent.com/68289543/103851623-8859f480-50ed-11eb-8178-2a03ab6c335f.png)크기의 2차원 리스트에 저장한 뒤에 해당 비용을 갱신해서 최단 거리를 계산

<br>

###  *서로소 집합*

- 공통 원소가 없는 두 집합을 의미
  - ex ) {1, 2}와 {3, 4}는 서로소 집합

#### 서로소 집합 자료구조

- 서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조
- 서로소 집합 자료구조는 **union**과 **find** 이 2개의 연산으로 조작할 수 있다.
  - **union** : 2개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산
  - **find** : 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산
- 서로소 집합 자료구조를 구현할 때는 **트리 자료구조**를 이용하여 집합을 표현한다.

<br>

#### 트리를 이용하여 서로소 집합을 계산하는 알고리즘

서로소 집합 정보 ( 합집합 연산 )가 주어졌을 때 트리 자료구조를 이용해서 집합을 표현하는 서로소 집합 계산 알고리즘은 다음과 같다.

1. union 연산을 확인하여, 서로 연결된 두 노드 A, B를 확인한다.
   1. A와 B의 루트 노드 A', B' 를 각각 찾는다.
   2. A' 와 B' 중 더 작은 원소를 부모 노드로 설정한다. (더 작은 원소를 가리키도록 한다.)
2. 모든 union 연산을 처리할 때까지 위 과정을 반복한다.



ex) 전체 집합 `{1, 2, 3, 4, 5, 6}` 총 6개의 원소로 구성되어 있는 상황을 생각해보자. 여기엔 다음과 같은 union 연산이 주어졌다.

![image](https://user-images.githubusercontent.com/68289543/103853719-19cb6580-50f2-11eb-904e-eda4f0528908.png)

​										( 참고로 ![image](https://user-images.githubusercontent.com/68289543/103853780-39fb2480-50f2-11eb-8914-ac7eb93775e0.png)는 '1과 4는 같은 집합' 이라는 뜻이다. )

편의상 그림으로 나타내면 다음과 같다. (실제로 각 원소의 집합 정보를 표현하려면 **트리 자료구조**를 이용한다.)

![image](https://user-images.githubusercontent.com/68289543/103854432-c4905380-50f3-11eb-96d0-c8848241b6ae.png)

즉, 이 그림을 통해 관계를 빠르게 알 수 있는데, 전체 원소가 `{1, 2, 3, 4}`와 `{5, 6}` 두 집합으로 나뉘어진다. 예시를 통해 구체적인 과정을 알아보자.

<br>

1.  초기 단계에서는 가장 먼저 노드의 개수(V) 크기의 **부모 테이블**을 초기화한다. 이때 모든 원소가 자기 자신을 부모로 가지도록 설정한다. 부모 테이블은 말 그대로 부모에 대한 정보만을 담고 있다. 그렇기 때문에 우리가 실제로 루트를 확인하고자 할 때는 재귀적으로 부모를 거슬러 올라가서 최종적인 루트를 찾아야한다. 

![image](https://user-images.githubusercontent.com/68289543/103855010-12f22200-50f5-11eb-9080-04b45fdf4ccd.png)

| 노드 번호 | 1    | 2    | 3    | 4    | 5    | 6    |
| --------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 부모      | 1    | 2    | 3    | 4    | 5    | 6    |

<br>

2. **union 1, 4**

   첫 번째 `union` 연산을 확인하면, 1과 4를 합친다. 이때는 노드 1과 노드 4의 루트 노드를 각각 찾으면 된다. 현재 루트 노드는 각각 1과 4이기 때문에 더 큰 번호에 해당하는 루트 노드 4의 부모를 1로 설정한다.

   ![image](https://user-images.githubusercontent.com/68289543/103859669-ca8b3200-50fd-11eb-8459-e92de347731d.png)

| 노드 번호 | 1    | 2    | 3    | 4    | 5    | 6    |
| --------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 부모      | 1    | 2    | 3    | 1    | 5    | 6    |

<br>

3. **union 2, 3** 

   현재 `union` 연산을 확인하면, 2와 3을 합친다. 따라서 노드 2와 노드 3의 루트 노드를 각각 찾으면 된다. 현재 루트 노드는 각각 2와 3이기 때문에 더 큰 번호에 해당하는 루트 노드 3의 부모를 2로 설정한다.

   ![image](https://user-images.githubusercontent.com/68289543/103859878-2786e800-50fe-11eb-8083-325e589faa51.png)

| 노드 번호 | 1    | 2    | 3    | 4    | 5    | 6    |
| --------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 부모      | 1    | 2    | 2    | 1    | 5    | 6    |

<br>

4. **union 2, 4**

   현재 `union` 연산을 확인하면, 2와 4를 합친다. 각각의 부모 노드를 확인하는데 노드 2의 부모 노드는 2, 4의 부모 노드는 1이다. 이 때 더 큰 번호에 해당하는 루트 노드 2의 부모를 1로 설정한다.

![image](https://user-images.githubusercontent.com/68289543/103860138-95331400-50fe-11eb-8da5-bb027da9b5cf.png)

| 노드 번호 | 1    | 2    | 3    | 4    | 5    | 6    |
| --------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 부모      | 1    | 1    | 2    | 1    | 5    | 6    |

<br>

5. **union 5, 6**

   마지막으로 `union` 연산을 확인하면 5와 6을 합친다. 이 때 노드 5와 노드 6의 부모 노드는 각각 5와 6이므로 더 큰 번호에 해당하는 루트 노드 6의 부모를 5로 설정한다.

   ![image](https://user-images.githubusercontent.com/68289543/103854432-c4905380-50f3-11eb-96d0-c8848241b6ae.png)

| 노드 번호 | 1    | 2    | 3    | 4    | 5    | 6    |
| --------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 부모      | 1    | 1    | 2    | 1    | 5    | 5    |

<br>

이렇게 모든 `union` 연산을 처리했다. 이 알고리즘에서 유의해야 할 점은 효과적인 `union` 연산을 처리하기 위해 '부모 테이블'을 항상 가지고 있어야 한다는 점이다.  또한 루트 노드를 즉시 계산할 수 없고 부모 테이블을 계속해서 확인하며 거슬러 올라가야 한다는 것이다. 위 연산에서도 노드 3의 부모 노드는 2라고 설정되어 있지만 노드 2의 부모 노드는 1이므로 최종적으로 노드 3의 루트 노드는 1이라고 볼 수 있다.

<br>

`기본적인 서로소 집합 알고리즘 소스코드`

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x) :
    if parent[x] != x :
        return find_parent(parent, parent[x])
    return x

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b) :
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b :
        parent[b] = a
    else :
        parent[a] = b

# 노드의 개수와 간선(union 연산)의 개수 입력받기
v, e = map(int,input().split())
parent = [0] * (v + 1)

# 부모 테이블 상에서, 부모를 자기 자신으로 초기화
for i in range(v + 1) :
    parent[i] = i

# union 연산을 각각 수행
for i in range(e) :
    a, b = map(int, input().split())
    union_parent(parent, a, b)
    
# 각 원소가 속한 집합 출력
print('각 원소가 속한 집합: ', end = '')
for i in range(1, v + 1) :
    print(find_parent(parent, i), end = ' ')

print()

# 부모 테이블 내용 출력
print('부모 테이블: ', end = '')
for i in range(1, v + 1) :
    print(parent[i], end = ' ')
```

위 소스코드의 실행 결과는 앞서 다룬 예시와 동일하다. 하지만 위와같이 코딩을 하게 되면 `find` 함수가 비효율적으로 동작한다. 최악의 경우에는 `find` 함수가 모든 노드를 다 확인해야 하기 때문에 시간복잡도가 O(V)이다. 이러한 `find` 함수는 **경로 압축(Path Compression)기법**을 적용하면 시간 복잡도를 개선시킬 수 있다.

경로 압축은 `find` 함수를 재귀적으로 호출한 뒤에 부모 테이블 값을 갱신하는 기법이다. 기존의 `find` 함수를 다음과 같이 변경하면 경로 압축 기법의 구현이 완료된다.

```python
def find_parent(parent, x) :
    if parent[x] != x :
        parent[x] = find_parent(parent, parent[x])
    return parent[x]
```

<br>

<br>

___

참고 : 이것이 코딩테스트다. with 파이썬 (나동빈)


