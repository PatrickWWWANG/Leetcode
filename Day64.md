# Day64 Graph Part09

---

### Dijkstra's Algorithm Optimization with Min-Heap
1. Use a dictionary to record edges and weights.  
2. Each time we check and update minDist, we add a [weight, node] pair to min-heap.  
3. In each iteration, the valid item pop out from min-heap is the closest node we want to find.  

---

### Bellman–Ford Algorithm
The Bellman–Ford algorithm is an algorithm that computes shortest paths from a single source vertex to all of the other vertices in a weighted digraph. It is slower than Dijkstra's algorithm, but is capable of handling graphs with negative weights.  
1. Set minDist of each node to infinity, set minDist of source to 0.  
2. Relax each edge n - 1 times.  
3. Use a parent array to record prior node if path reconstruction is required.  

---

### 1. 743 Network Delay Time
You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target. We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal.  
Use Dijkstra's Algorithm optimized with min-heap.  

```
Pseudocode Dijkstra's Algorithm Optimization with Min-Heap:
from collections import defaultdict
import heapq
minDist = [float('inf')] * (n + 1)
visited = [False] * (n + 1)
neighbors = defaultdict(list)
min_heap = []

for [a, b, w] in times:
    neighbors[a].append([b, w])

minDist[k] = 0
heapq.heappush(min_heap, [0, k])

while min_heap:
    [d, cur] = heapq.heappop(min_heap)
    if visited[cur]:
        continue
    visited[cur] = True
    for [b, w] in neighbors[cur]:
        if visited[b] == False:
            minDist[b] = min(minDist[b], d + w)
            heapq.heappush(min_heap, [minDist[b], b])

if max(minDist[1 :]) < float('inf'):
    return max(minDist[1 :])
else:
    return -1
```
**Note**  
Use heapq in python to realize the heap.  
When push [a, b] to a heap, heapq sort the heap with the first item as the key.  
Don't forget to 'continue' when the node pop out from heap is already visited. This is important because we may add a node multiple times into the min-heap and only take the first occurance, which is closet to sourse.  

Use Bellman–Ford Algorithm.  
There is no need to use a visited array in Bellman–Ford algorithm because all nodes are guaranteed to reach minimum distance after n - 1 relaxations of all edges.  
For this problem, Dijkstra's algorithm is preferred because it is more efficient. For problems with negative weights in graph, we have to use Bellman-Ford.  

```
Pseudocode Bellman–Ford Algorithm:
minDist = [float('inf')] * (n + 1)
minDist[k] = 0

for _ in range(n - 1):
    for [a, b, w] in times:
        minDist[b] = min(minDist[b], minDist[a] + w)

if max(minDist[1 :]) < float('inf'):
    return max(minDist[1 :])
else:
    return -1
```
