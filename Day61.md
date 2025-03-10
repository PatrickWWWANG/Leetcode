# Day61 Graph Part06

---

### 1. 684 Redundant Connection
You are given a graph that started as a tree with n nodes labeled from 1 to n, with one additional edge added. Return an edge that can be removed so that the resulting graph is a tree of n nodes. If there are multiple answers, return the answer that occurs last in the input.  
Use union find data structure to solve this problem. We don't need to explicitly write the join function because we need to find the roots for node in iteration of edges, so we can write the join logic there.  
We check if the two nodes of an edge are already in the same set, if so, we can return this edge, otherwise we join the two nodes.  

```
fa = list(range(len(edges) + 1))

def find(u):
    if fa[u] == u:
        return u
    else:
        fa[u] = find(fa[u])
        return fa[u]

for [u, v] in edges:
    u_r = find(u)
    v_r = find(v)
    if u_r == v_r:
        return [u, v]
    else:
        fa[v_r] = u_r
```
**Caution**  
Note that in this problem, nodes are 1 to n, so be careful of the initialization of father list.  

---

### 2. 685 Redundant Connection II
The given input is a directed graph that started as a rooted tree with n nodes (with distinct values from 1 to n), with one additional directed edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed. Return an edge that can be removed so that the resulting graph is a rooted tree of n nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array.  
When we have graph that is a rooted directed tree plus one additional edge, there will be two possibilities:  
1. There will be one node with in-degree 2 when the additional edge goes to the node that is not root.  
2. All nodes have in-degree 1 and there is a cycle when the additional edge goes to the root.  
In case 1, we need to find the node that has in-degree 2. We try to delete the edge that comes later in edges array and check if the rest graph is a valid rooted tree by checking if there is cycle in it. If yes, we return this edge, and if not, we return the other edge.  
In case two, we simply return the first edge that makes cycle in the graph.  

```
Pseudocode:
fa = list(range(len(edges) + 1))

def find(u):
    if fa[u] == u:
        return u
    else:
        fa[u] = find(fa[u])
        return fa[u]

# Find in-degrees of each node
in_degree = {}
for [u, v] in edges:
    if v in in_degree.keys():
        in_degree[v] += 1
    else:
        in_degree[v] = 1

# Check if there is a node with in-degree 2, pick the edges causing it if so
candidate = []
for i in range(len(edges) - 1, -1, -1):
    if in_degree[edges[i][1]] == 2:
        candidate.append(i)

# Try delete one edge and check the rest graph if there is a node with in-degree 2
if candidate:
    to_delete = candidate[0]
    for i in range(len(edges)):
        if i != to_delete:
            u_r = find(edges[i][0])
            v_r = find(edges[i][1])
            if u_r == v_r:
                return edges[candidate[1]]
            else:
                fa[v_r] = u_r
    return edges[to_delete]
# Find edge causing cycle if there is no node with in-degree 2
else:
    for [u, v] in edges:
        u_r = find(u)
        v_r = find(v)
        if u_r == v_r:
            return [u, v]
        else:
            fa[v_r] = u_r
```
