# Day59 Graph Part05

---

### Union Find Data Structure
1. Add 2 elements to a same set.  
2. Check if 2 elements are in the same set.  
We use a 'father' array such that father[A] = father of A.  
Path compression: we can set the father of A to the root when searching to avoid duplicate search.  
When we join 2 elements, we join the root of both nodes.  

---

### 1. 1971 Find if Path Exists in Graph
Given edges and the integers n, source, and destination, return true if there is a valid path from source to destination, or false otherwise.  
The is a basic problem about union find data structure. Simply use union find to check if source and destination belong to the same set.  

```
Pseudocode:
fa = list(range(n))

def find(u):
    if fa[u] == u:
        return u
    else:
        fa[u] = find(fa[u])
        return fa[u]

def join(u, v):
    u = find(u)
    v = find(v)
    if u != v:
        fa[v] = u

for [u, v] in edges:
    join(u, v)

s = find(source)
d = find(destination)

return s == d
```
**Note**  
Note that in the join function, we join the root of u and v.  
Note the path compression step in find function.  
