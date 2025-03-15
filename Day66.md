# Day66 Graph Part11

---

### Floyd's Algorithm
Floyd's algorithm is an algorithm for finding shortest paths in a directed weighted graph with positive or negative edge weights (but with no negative cycles). It finds the lengths of shortest paths between all pairs of vertices.  
Floyd's algorithm is a dynamic programming solution.  
It uses a n * n matrix to store min distances, and another n * n matrix to store path if reconstruction is required.  
1. For all node in graph  
2. For all node pair  
3. Compare current length and path length using the node as mid point, update if new route is shorter  
Initialize min distance matrix to edge weights, initialize path matrix to -1.  
In path reconstruction, the path matrix records mid point in path, but not necessarily the point prior to destination.  

---

### A* Algorithm
A* is a graph traversal and pathfinding algorithm that is used in many fields of computer science due to its completeness, optimality, and optimal efficiency. Given a weighted graph, a source node and a goal node, the algorithm finds the shortest (with respect to cost) path.  
A* is based on the cost of the path and an estimate of the cost required to extend the path all the way to the goal.  

---

### 1. 743 Network Delay Time
You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target. We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal.  
Use Floyd's algorithm.  

```
Pseudocode Floyd's Algorithm:
minDist = [[float('inf')] * (n + 1) for _ in range(n + 1)]

for i in range(1, n + 1):
    minDist[i][i] = 0

for [a, b, w] in times:
    minDist[a][b] = w

for x in range(1, n + 1):
    for y in range(1, n + 1):
        for z in range(1, n + 1):
            if minDist[y][z] > minDist[y][x] + minDist[x][z]:
                minDist[y][z] = minDist[y][x] + minDist[x][z]

if max(minDist[k][1:]) < float('inf'):
    return max(minDist[k][1:])
else:
    return -1
```
**Note**  
Floyd's algorithm is O(n^3) time efficiency. It works better for graphs with small number of nodes and dense edges. For graphs with big number of nodes and sparse edges, we can call Dijkstra's algorithm multiple times to find multiple source shortest paths.  

---

### A* Code

```Python
from queue import PriorityQueue
def distance(a, b):
    (x1, y1) = a
    (x2, y2) = b
    return abs(x1 - x2) + abs(y1 - y2)

def a_star_search(graph, start, goal):
    frontier = PriorityQueue()
    frontier.put(start, 0)
    came_from = {}
    cost_so_far = {}
    came_from[start] = None
    cost_so_far[start] = 0

    while not frontier.empty():
        current = frontier.get()

        if current == goal:
            break
        
        for next in graph.neighbors(current):
            new_cost = cost_so_far[current] + graph.cost(current, next)
            if next not in cost_so_far or new_cost < cost_so_far[next]:
                cost_so_far[next] = new_cost
                priority = new_cost + distance(goal, next)
                frontier.put(next, priority)
                came_from[next] = current
        
    return came_from, cost_so_far
```
**Note**  
Use priority queue or min heap to realize A* algorithm.  
