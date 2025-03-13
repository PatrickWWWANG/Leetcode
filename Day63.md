# Day63 Graph Part08

---

### Topological sorting
Topological sorting of a directed graph is a linear ordering of its vertices such that for every directed edge (u,v) from vertex u to vertex v, u comes before v in the ordering.  
Transform graph to a 1-D array.  
Check for cycle in graph. If topological sorting can't be done for a graph, then it has cycle.  

---

### Topological Sorting BFS
1. Find the node with in-degree == 0.  
2. Add the node to array, delete the node and all relating edges from graph.  
3. Iterate.  

---

### Dijkstra's Algorithm
Dijkstra's algorithm is an algorithm for finding the shortest paths between nodes in a weighted graph. It  finds the shortest path from a given source node to every other node.  
Weights in graph can't be negative to use Dijkstra's algorithm.  
1. Choose the closest node that is not visited.  
2. Mark the node as visited.  
3. Update the minDist array, using min(current value, distance travelling via the current node).  
If path reconstruction is required, we need another parent array.  

---

### 1. 210 Course Schedule II
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai. Return the ordering of courses you should take to finish all courses.  
Construct the problem as a graph, with edges from prerequisites to later courses. Do a topological sorting.  
1. Iterate the edges, maintain an array to record in-degrees and a dictionary to record edges.  
2. Find the nodes with 0 in-degree, add them to a queue.  
3. While queue is not empty, pop and handle the first item from the queue. Each time decrement the in-degree, add the node to the queue if the in-degree becomes 0.  
4. If the result length == numCourses, the ordering is possible and return. Otherwise return empty list.  

```
Psdeudocode:
from collections import deque, defaultdict
in_degree = [0] * numCourses
pre_req = defaultdict(list)

for [a, b] in prerequisites:
    in_degree[a] += 1
    pre_req[b].append(a)

que = deque()
for i in range(numCourses):
    if in_degree[i] == 0:
        que.append(i)

order = []
while que:
    cur = que.popleft()
    order.append(cur)
    for i in pre_req[cur]:
        in_degree[i] -= 1
        if in_degree[i] == 0:
            que.append(i)

if len(order) == numCourses:
    return order
else:
    return []
```
**Caution**  
Check in_degree == 0 and add i to queue only when we decrement the in-degree because this ensures we only add each course to queue at most one time to prevent duplicate.  

---

### 2. 743 Network Delay Time
You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target. We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal.  
Use Dijkstra's Algorithm to compute the distance between source and each node, and return the maximum.  

```
Pseudocode:
from collections import defaultdict
weights = [[float('inf')] * (n + 1) for _ in range(n + 1)]
minDist = [float('inf')] * (n + 1)
visited = [False] * (n + 1)
neighbors = defaultdict(list)

minDist[k] = 0

for [a, b, w] in times:
    weights[a][b] = w
    neighbors[a].append(b)

for _ in range(n):
    min_D = float('inf')
    for i in range(1, n + 1):
        if visited[i] == False and minDist[i] < min_D:
            cur = i
            min_D = minDist[i]
    if cur:
        visited[cur] = True
        for j in neighbors[cur]:
            if visited[j] == False:
                minDist[j] = min(minDist[j], min_D + weights[cur][j])
    else:
        break

if max(minDist[1 :]) < float('inf'):
    return max(minDist[1 :])
else:
    return -1
```
**Note**  
For this problem, nodes are 1 to n, so be carefully when dealing with the indexes.  
Don't forget to check if this node is already visited when finding min_D and updating minDist array.  
The dictionary recording edges is not necessary. We can iterate over all nodes when updating minDist because we set non-existent edge to infinite weight.  
**Caution**  
Make sure to use one * and one for loop when creating matrix, otherwise the rows of the matrix are actually referring to the same array.  
