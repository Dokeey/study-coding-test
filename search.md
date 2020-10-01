# 코딩테스트 알고리즘

## 1. 너비 우선 탐색 (BFS)

### 개념

너비를 우선으로 하여 탐색을 수행하는 탐색 알고리즘

큐 자료구조를 사용

1. 큐에서 하나의 노드를 꺼낸다.
2. 해당 노드에 연결된 노드 중 방문하지 않은 노드를 방문하고, 차례대로 큐에 삽입한다.

루트 노드부터 가까운 노드들 탐색이 이루어짐

BFS는 그 자체로는 큰 의미가 없고 다른 알고리즘에 적용한다는 것이 핵심

## 2. 깊이 우선 탐색 (DFS)

### 개념

깊이를 우선으로 하여 탐색을 수행하는 탐색 알고리즘

스택 자료구조를 사용

1. 스택의 최상단 노드를 확인
2. 최상단 노드에게 방문하지 않은 인접 노드가 있다면 그 노드를 스택에 넣고 방문처리.
3. 방문하지 않은 노드가 없다면 스택에서 최상단 노드를 뺀다.

재귀 함수 자체가 스택의 원리이기 때문에 짧은 코드로 구현할 수 있음

DFS 또한 그 자체로의 큰 의미가 없다.



## 문제

### DFS와 BFS

> 출처: 백준알고리즘 1260번 문제

#### 문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

#### 입력

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

#### 예제 입력

```
4 5 1
1 2
1 3
1 4
2 4
3 4
```

#### 출력

```
1 2 4 3
1 2 3 4
```

#### code

```python
from collections import deque

# 입력받기
nums = ["4 5 1",
        "1 2",
        "1 3",
        "1 4",
        "2 4",
        "3 4"]

# 노드수, 간선수, 시작 정점 받기
nodes, lines, start = map(int, nums.pop(0).split())

# 그래프 그리기
graph = {}
for idx, num in enumerate(nums):
    a, b = map(int, num.split())
    if not a in graph:
        graph[a] = [b]
    elif not b in graph[a]:
        graph[a].append(b)
    if not b in graph:
        graph[b] = [a]
    elif not a in graph[b]:
        graph[b].append(a)

def DFS(graph):
    stack = [start]
    visited = []

    while stack:
        node = stack.pop()
        if not node in visited:
            visited.append(node)
        # stack 이기 때문에 reverse True로 작은 수가 제일 끝에 있어야 한다.
        stack += sorted(list(set(graph[node]) - set(visited)), reverse=True)
    return visited

def BFS(graph):
    queue = deque([start])
    visited = []

    while queue:
        node = queue.popleft()
        if not node in visited:
            visited.append(node)
        queue += sorted(list(set(graph[node]) - set(visited)))
    return visited

print(graph)
print(DFS(graph))
print(BFS(graph))
```

