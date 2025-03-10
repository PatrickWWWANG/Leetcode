# Day62 Graph Part07

---

### Minimum Spanning Tree
MST is a subset of the edges of a connected, edge-weighted undirected graph that connects all the vertices together, without any cycles and with the minimum possible total edge weight.  

---

### Prim Algorithm (Add Node)
1. Strating from any node, add it to connected part and initialize minDist array  
2. Choose the cloest node to the connected part, add it to the connected part  
3. Update minDist array, which is the shortest distance between not-connected nodes and the connected part  
Prim works better for dense graphs (dense edges).  

---

### Kruskal Algorithm (Add Edge)
1. Find the smallest edge in the graph, add it to MST    
2. Find the smallest remaining edge in the graph, add it to MST if the two nodes of the edge are not in the same connected component  
3. Iterate over all edges  
Kruskal works better for sparse graphs.  

---

### 1. 1584 Min Cost to Connect All Points
You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi]. The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val. Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.  
Regard it as a MST problem, assuming the points form a strongly connect graph and we try to find the MST.  
Since we view the problem as a strongly connect graph, which is dense, Prim should work more efficiently. We can still use both Prim and Kruskal to approach this problem.  

```
Pseudocode Prim:
visited = [False] * len(points)
minDist = [float('inf')] * len(points)

def distance(a, b):
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

for _ in range(len(points)):
    min_d = float('inf')
    min_node = -1
    
    for i in range(len(points)):
        if visited[i] == False and minDist[i] < min_d:
            min_d = minDist[i]
            min_node = i
    
    visited[min_node] = True

    for j in range(len(points)):
        if visited[j] == False:
            minDist[j] = min(minDist[j], distance(points[min_node], points[j]))

return sum(minDist[:-1])

Pseudocode Kruskal:
def distance(a, b):
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

edges = []

for i in range(len(points) - 1):
    for j in range(i + 1, len(points)):
        edges.append([i, j, distance(points[i], points[j])])

edges.sort(key=lambda x: x[2])

fa = list(range(len(points)))

def find(u):
    if fa[u] == u:
        return u
    else:
        fa[u] = find(fa[u])
        return fa[u]

path = 0
for edge in edges:
    u_r = find(edge[0])
    v_r = find(edge[1])
    if u_r != v_r:
        path += edge[2]
        fa[v_r] = u_r

return path
```
**Note**  
In Prim, we return sum(minDist[:-1]) because these first n - 1 items in minDist represents the n - 1 edges we added to the MST. The last item of minDist is float('inf') because we firstly add the last point into MST.  
In Kruskal, we need to add all edges to an array and sort edges on weights. When we iterate over the edges, we check if the two nodes of the edge are in the same connected component using **union find data structure**.  
