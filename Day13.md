# Day13 Binary Tree Part 01

---

### Type
1. Full Binary Tree. #nodes 2^k - 1  
2. Complete Binary Tree. Full except deepest level and deepest level full from left.  
3. Binary Search Tree. child_l <= parent <= child_r, searching for a node in O(n).  
4. Balanced Binary Search Tree. abs(left subtree depth - right subtree depth) <= 1.  

### Method of Storage
1. Linked: linked list with two pointers.  
2. Linear: store in anarray. Root index i: left 2*i+1, right 2*i+2.  

### Traverse
##### DFS (Recursion or Iteration)
1. Pre-Order Traversal: root -> left child -> right child  
2. In-Order Traversal: left child -> root -> right child  
3. Post-Order Traversal: left child -> right child -> root  
##### BFS
Level-Order Traversal: iteration using a queue.  

### Definition
```
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = None
        self.right = None
```

---

### 1. Recursive Traversal 144 Pre--Order 94 In-Order 145 Post-Order 
1. Find the parameters and return value of the recursive function.  
2. Determine the termination condition.  
3. Set the recursive step.  

```
Pseudocode Pre-Order:
out = []

def dfs(node):
    if not node:
        return
    out.append(node.val)
    dfs(node.left)
    dfs(node.right)

dfs(root)
return out

Pseudocode In-Order:
out = []

def dfs(node):
    if not node:
        return
    dfs(node.left)
    out.append(node.val)
    dfs(node.right)

dfs(root)
return out

Pseudocode Post-Order:
out = []

def dfs(node):
    if not node:
        return
    dfs(node.left)
    dfs(node.right)
    out.append(node.val)

dfs(root)
return out
```

---

### 2. Iterative Traversal 144 Pre--Order 94 In-Order 145 Post-Order 
In iterative traversal, use stack to simulate recursion.  
Pre-Order: stack pop root, and push right, left, get root -> left -> right.  
Post-Order: stack pop root, and push left, right, get root -> right -> left, then reverse.  
In-Order: use a pointer cur to help traverse the tree because the node being traversed is not the node being added to output.  

```
Pseudocode Pre-Order:
from collections import deque
out = []
stack = deque()
if root:
    stack.append(root)
while stack:
    node = stack.pop()
    out.append(node.val)
    if node.right:
        stack.append(node.right)
    if node.left
        stack.append(node.left)
return out

Pseudocode Post-Order:
from collections import deque
out = []
satck = deque()
if root:
    stack.append(root)
while stack:
    node = stack.pop()
    out.append(node.val)
    if node.left:
        stack.append(node.left)
    if node.right:
        stack.append(node.right)
out.reverse()
return out

Pseudocode In-Order:
from collections import deque
out = []
stack = deque()
cur = root
while cur or stack:
    if cur:
        stack.append(cur)
        cur = cur.left
    else:
        cur = stack.pop()
        out.append(cur.val)
        cur = cur.right
return cur
```

---

### 3. 102 Binary Tree Level Order Traversal
Level-Order traversal is similar to BFS.  
Use two nested while loops, one for controlling queue, one for controlling level.  

```
Pseudocode:
if not root:
    return []

from collections import deque
out = []
queue = deque()
queue.append(root)
level = -1

while queue:
    size = len(queue)
    level += 1
    out.append([])
    while size > 0:
        node = queue.popleft()
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
        out[level].append(node.val)
        size -= 1

return out
```