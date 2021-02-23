# 스택(stack)

> 후입선출(Last-In-First-Out)의 자료구조



## 스택의 구현

### 자료구조

- 파이썬에서는 `List`를 사용할 수 있다.
- 스택에 마지막으로 삽입된 원소의 위치를 `top` 혹은 `stack pointer`이라고 한다.

### 연산

- 삽입: `push`, 스택에 자료를 추가한다.
- 삭제: `pop`, 스택에서 자료를 꺼낸다. 마지막으로 `push`한 자료가 나온다.
- 공백검사: `isEmpty`
- `peek`: `top`에 있는 원소를 반환한다. `pop`하지는 않는다.

### 속도

- `list.append`보다 빠르게 처리하기 위해서는 스택의 크기를 정해두고 `top` 인덱스를 이용해 자료를 추가하는 것이 좋다.



## Function Call

> 함수의 호출은 스택의 구조로 이루어진다.

- 함수가 사용되고 복귀되어야 하는 위치가 기록된다.
- 재귀 함수를 이용하거나, 함수 내에서 함수를 사용하는 경우 실행 관련 정보가 스택으로 쌓인다. top에는 현재 실행 중인 함수가 존재.

## 재귀(recursion)

> 기본형태 - `f(n,k)`: 호출단계 n, 목표치 k

### 재귀 호출

- f(0,3) -> f(1,3) -> f(2,3) -> f(3,3) 재귀 종료, return 시작 -> f(2,3) -> f(1,3) -> f(0,3)
- factorial을 재귀로 나타낼 때는 n이 기본적으로 0이지만, 모든 재귀함수에서 n이 0인 것은 아니다.

### cf) 재귀를 이용한 리스트 복사

```python
A = [1, 2, 3, 4, 5]
B = [0, 0, 0, 0, 0]


def list_copy(n, k):
    if n == k:
        return
    else:
        B[n] = A[n]
        list_copy(n+1, k)


list_copy(0, 5)
print(B)
```





## Memoization

> 특정 연산의 계산 결과를 저장해 두고, 중복하여 등장하는 경우 바로 사용해 계산 자원을 아낄 수 있음

### cf) Dynamic Programming



## DFS(깊이우선탐색)

> 스택을 이용한 DFS, 다양하게 구현될 수 있다.

```python
# 재귀를 사용하지 않는 dfs
# 지나간 점을 돌아오지 않도록 개선한 로직
# 인접행렬
adj_matrix = [[0,0,0,0,0],
             [0,0,0,0,0],
             [0,0,0,0,0],
             [0,0,0,0,0],
             [0,0,0,0,0],]
stack = [] # 방문 예정 노드를 stack에 담는다
visited = [0] * 5 # 방문 여부 리스트 visited
stack.append(start) # 시작점 start
visited[start] = 1
while stack:
    node = stack.pop()
    for i in range(5):
        adj_matrix[node][i]:
            if adj_matrix[node][i] == 1 and visited[i] == 0:
                stack.append(i)
                visited[i] = 1
```

