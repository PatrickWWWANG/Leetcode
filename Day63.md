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
