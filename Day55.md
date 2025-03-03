# Day55 Graph Part01

---

### Graph
1. Directed graph, undirected graph  
2. Weigth of edge  
3. Degree of node, in-degree, out-degree  
4. Connected graph (undirected graph), strongly connected graph (directed graph)  
5. Connected component, strongly connected component  
6. Naive storage (store all edges), adjacency matrix, adjacency table  
7. DFS, BFS  

---

### DFS
DFS is good for finding path (number of paths) between two nodes.  

```
Pseudocode:
Initialize result, path
def dfs(graph, visited nodes):
    if terminal condition:
        store result
        return
    for all nodes connected to current node:
        process node
        dfs(graph, visited node (+ current node))
        (backtrack: reverse operation)
```

---

### BFS
BFS is good for finding the shortest path between two nodes.  

```
Pseudocode:
from collections import deque
def bfs(graph):
    que = deque()
    visited = [0 for _ in range(len(graph))]
    que.append(0)
    visited[0] = 1
    while que:
        node = que.popleft()
        for i in graph[node]:
            if visited[i] == 0:
                'DO SOMETHING'
                que.append(i)
                visited[i] = 1
```

---

### 1. 797 All Paths From Source to Target
Given a directed acyclic graph (DAG) of n nodes labeled from 0 to n - 1, find all possible paths from node 0 to node n - 1 and return them in any order.  
Use a DFS to iterate the graph and keep track of the path.  
Method similar to backtracking.  
Process each adjacent node to the current node in iteration step.  

```
Pseudocode:
result, path = [], [0]

def dfs(graph, node):
    if path and path[-1] == len(graph) - 1:
        result.append(path[:])
        return
    for i in graph[node]:
        path.append(i)
        dfs(graph, i)
        path.pop()

dfs(graph, 0)
return result
```
**Caution**  
Include the start node '0' when initialize the path array. Otherwise the output path will miss the start node.  
