# MST(최소 신장 트리)

> Minimum Spanning Tree

### 개요

- 최소 신장 트리: 그래프의 모든 정점이 연결된 트리(사이클이 없음) 중 가중치의 합이 가장 작은 트리
- 최소비용 문제 (섬과 섬을 연결하는 다리를 지을 때 가장 적은 비용이 드는 경우)에 사용할 수 있다.
- 최소 신장 트리의 구현은 그리디 방식으로 접근한다. 즉, 현재 연결이 가능한 경우의 수 중 1) 가장 비용이 적게 드는 것을 연결하고, 2) 연결로 인해 갱신된 비용을 확인하고, 3) 다시 가장 비용이 적게 드는 것을 연결, 이를 반복해 최소 신장 트리를 완성하게 된다.
- 주로 Prim(노드 시작) / Kruskal(간선 시작) 알고리즘으로 구현한다.

<br>

## Prim 알고리즘

> 시작 노드에서부터 최소 신장 트리를 그려나가는 방법

- O(n^2)의 시간복잡도를 가진다. 
- 간선이 많이 존재하는 그래프의 최소신장트리를 구하는데 적합하다.

```python
# 마지막 노드 V(0~V), 간선의 수 E
V, E = map(int, input().split())
# 인정행렬 adj_matrix
adj_matrix = [[0]*(V+1) for x in range(V+1)]
# 간선의 가중치 정보를 인접행렬에 입력 - 무방향
for _ in range(E):
    n1, n2, w = map(int, input().split())
    adj_matrix[n1][n2] = w
    adj_matrix[n2][n1] = w
# 현재 상태에서 각 노드의 연결비용을 기록한 costs
costs = [11]*(V+1)
# mst에 추가된 노드 기록할 mst
mst = [0]*(V+1)
# 추가한 노드의 수 기록할 cnt
cnt = 0

# 0번 노드 추가
costs[0] = 0
mst[0] = 1
current = 0
cnt += 1
sum_costs = 0

# 모든 노드를 추가할 때까지
while cnt <= V:
    # costs 갱신
    for i in range(V+1):
        if adj_matrix[current][i] and adj_matrix[current][i] < costs[i]:
            costs[i] = adj_matrix[current][i]
    # 다음 연결할 노드 결정하기
    for i in range(V+1):
        if not mst[i]:
            next = i
            break
    for i in range(next, V+1):
        if costs[i] < costs[next] and not mst[i]:
            next = i
    # 노드 연결, 기록 및 비용 합산
    mst[next] = 1
    cnt += 1
    sum_costs += costs[next]
    current = next

# 최종 비용
print(sum_costs)
```



<br>

## Kruskal 알고리즘

> 최소 비용을 간선에서 시작하여 최소 신장 트리를 그려나가는 방법

- 노드가 많이 존재하는 그래프의 최소신장트리를 구하는데 적합하다.
- 1) 그래프의 간선들을 가중치 순으로 정렬하고, 2) 가장 가중치가 낮은 간선부터 하나씩 확인하며, 사이클을 형성하지 않는 간선만 채택하여 MST에 추가한다.

```python
# 그래프에 연결되었다면 대표노드를, 아니라면 자기 자신을 리턴하는 함수: 즉, 어떤 경우에나 대표노드를 리턴
def find_set(x):
    while x != p[x]:
        x = p[x]
    return x

# 마지막 노드 V(0~V), 간선의 수 E
V, E = map(int, input().split())
# 모든 간선 입력받는 edge 리스트: (w, n1, n2)
edges = []
for _ in range(E):
    n1, n2, w = map(int, input().split())
    edges.append((w, n1, n2))
# 간선을 가중치 오름차순으로 정렬
edges.sort()
# 대표노드 리스트 p
p = [i for i in range(V+1)]
# 연결한 노드의 수 cnt: 첫 간선이 2개의 노드를 연결하므로 1에서 시작
cnt = 1
# 연결된 간선들의 가중치 합 total
total = 0
# 가장 비용이 낮은 간선부터 순서대로 확인
for w, n1, n2 in edges:
    # 두 노드의 대표노드가 같지 않다면(같은 그래프에 속하지 않는다면)
    # 두 노드의 대표노드가 같다면, 사이클을 형성하므로 걸러야한다.
    if find_set(n1) != find_set(n2):
        # 현재 확인중인 간선을 채택: 노드 수 합산, 간선 가중치 합산
        cnt += 1
        total += w
        # n1을 항상 더 큰 숫자의 노드로 설정
        if n1 < n2:
            n1, n2 = n2, n1
        # 대표노드 설정: n1이 속한 그래프의 대표노드를 n2의 대표노드로
        p[find_set(n1)] = find_set(n2)
        # 모든 노드가 연결되었다면 break
        if cnt == V+1:
            break
            
# 최종 비용
print(total)
```



<br>

