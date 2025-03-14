# Day65 Graph Part10

---

### Bellman–Ford Optimization with Queue (Shortest Path Faster Algorithm, SPFA)
When we relax edges, we only relax those from the nodes that we updated minDist.  
We use a queue to store the nodes that we updated minDist.  
We use an array to check if a node is in the queue to prevent adding a node to the queue again while it's already in the queue.  

---

### Check Negative-Weight Circle in Graph with Bellman-Ford
1. In regular Bellman-Ford, after n - 1 relaxations of edges, we record minDist array and do one more relaxation for all edges. If the minDist array updates, there must be negative-weight cycle.  
2. In Bellman-Ford optimization with queue, we use another array to record the number of times each node is added into the queue. If any node is added more than n - 1 times, there must be negative-weight cycle.  

---

### Bellman-Ford Single Source Finite Length Shortest Path
When we relax all edges one time, we are essentially finding shortest path with max length 1 from source.  
To find shortest path with length k, we control number of relaxations of all edges to k.  
We have to make a **minDist copy** before each relaxation of all edges, this is because we need to control the path length. If we use current minDist, the number we get may from the current iteration, which breaks the control of path length.  
Bellman–Ford optimization with queue also works. We use a variable to record the number of enqueues in each iteration, and use this variable to control the number of relaxations of all edges.  

---

### 1. 743 Network Delay Time
You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target. We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal.  
Use Bellman–Ford optimization with queue.  

```
Pseudocode Bellman–Ford Optimization with Queue:
from collections import deque, defaultdict
minDist = [float('inf')] * (n + 1)
que = deque()
neighbors = defaultdict(list)
in_que = [False] * (n + 1)

for [a, b, w] in times:
    neighbors[a].append([b, w])

minDist[k] = 0
que.append(k)
in_que[k] = True

while que:
    cur = que.popleft()
    in_que[cur] = False
    for [b, w] in neighbors[cur]:
        if minDist[b] > minDist[cur] + w:
            minDist[b] = minDist[cur] + w
            que.append(b)
            in_que[b] = True

if max(minDist[1 :]) < float('inf'):
    return max(minDist[1 :])
else:
    return -1
```
**Note**  
For this problem, Bellman-Ford improved with queue can perform similar time efficiency as Dijkstra's.  

---

### 2. 787 Cheapest Flights Within K Stops
There are n cities connected by some number of flights. You are given an array flights where flights[i] = [fromi, toi, pricei] indicates that there is a flight from city fromi to city toi with cost pricei. You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1.  
Use Bellman-Ford to find single source finite length path.  
We do k + 1 relaxations of all edges because k stops means k + 1 path segments.  

```
Pseudocode:
minDist = [float('inf')] * n
minDist[src] = 0

for _ in range(k + 1):
    minDist_copy = minDist[:]
    for [a, b, w] in flights:
        minDist[b] = min(minDist[b], minDist_copy[a] + w)

if minDist[dst] < float('inf'):
    return minDist[dst]
else:
    return -1
```
**Caution**  
Use minDist_copy. When relaxing an edge, use source distance from copy because it may have updated in this round; use destination distance from current minDist because we don't want to overwrite any updates we have done in this round.  
