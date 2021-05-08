# 다익스트라(Dijkstra) 알고리즘

<br>

## 개요

- 최단 경로 탐색 알고리즘
- 하나의 정점에서 다른 정점들로 가는 각각의 최소 비용(최단 경로)를 찾는다.
- 간선은 음의 간선을 포함하지 않는다.

<br>

## 구현

- 시작 정점 s와 연결 관계를 기록한 인접 행렬이 주어졌다고 가정한다.
- 시작 정점으로부터의 거리(비용) 리스트를 가능한 최댓값(최장거리 혹은 무한대)으로 설정한다. 시작 정점 자신으로 가는 비용은 0으로 설정한다.
- 시작 정점에 연결된 정점으로 가는 비용을 갱신한다. 그 중 비용이 가장 작은 정점을 다음 정점을 로 설정한다.
- 다음 정점에서 연결된 정점으로 (다음 정점을 거쳐서) 가는 비용을 기존의 비용과 비교하여 갱신한다. 방문하지 않은 정점 중 비용이 가장 작은 정점을 다음 정점으로 설정한다. 모든 정점을 확인할 때까지 세 번째, 네 번째 작업을 반복한다.

```python
# 노드의 수 N+1, 간선의 수 E
N, E = map(int, input().split())
# 인접행렬 생성 및 입력받기
adj_matrix = [[0]*(N+1) for x in range(N+1)]
for _ in range(E):
    start, end, weight = map(int, input().split())
    adj_matrix[start][end] = weight
# 0에서 부터의 비용 기록할 리스트 초기화
cost_from_zero = [10*(N+1)]*(N+1)
cost_from_zero[0] = 0
# 방문여부 기록할 리스트 초기화
visited = [0]*(N+1)
visited[0] = 1
# 현재 노드 설정
current = 0
# 방문한 노드 수 초기화
cnt = 1
# 다익스트라
while cnt <= N+1:
    # cost_from_zero 갱신
    for i in range(N+1):
        # 현재 노드에서 다른 노드로 갈 수 있고, 현재 노드를 거쳐가는 것이 비용이 더 적을 때 갱신
        if adj_matrix[current][i] and cost_from_zero[current] + adj_matrix[current][i] < cost_from_zero[i]:
            cost_from_zero[i] = cost_from_zero[current] + adj_matrix[current][i]
    # 갈 수 있는 비용이 가장 낮은 노드로 current 갱신
    for i in range(N+1):
        if not visited[i]:
            current = i
            break
    for i in range(current, N+1):
        if cost_from_zero[i] < cost_from_zero[current] and not visited[i]:
            current = i
    # 방문 기록 및 방문한 노드 수 합산
    visited[current] = 1
    cnt += 1
print("#{} {}".format(tc, cost_from_zero[N]))
```



