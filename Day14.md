# Day14 Binary Tree Part 02

---

### 1. 226 Invert Binary Tree
1. Recursion: use pre-order or post-order.  
2. Iteration: use a queue.  

```
Pseudocode Recursion:
if not root:
    return root
root.left, root.right = root.right, root.left
self.invertTree(root.left)
self.invertTree(root.right)
return root

Pseudocode Iteration:
from collections import deque
queue = deque()
if root:
    queue.append(root)
while queue:
    node = queue.popleft()
    node.left, node.right = node.right, node.left
    if node.left:
        queue.append(node.left)
    if node.right:
        queue.append(node.right)
return root
```

---

### 2. 101 Symmetric Tree
1. Iteration: use level-order traversal and check if each level is palindrome with 'null' fill in.  
2. Recursion: use idea of post-order traversal to check if left.left == right.right and vice versa.  

```
Pseudocode Iteration:
if not root:
    return True

from collections import deque
queue = deque()
layers = []
level = -1
queue.append(root)

while queue:
    size = len(queue)
    level += 1
    layers.append([])
    while size > 0:
        node = queue.popleft()
        if node:
            queue.append(node.left)
            queue.append(node.right)
            layers[level].append(node.val)
        else:
            layer[level].append('null')
        size -= 1

for layer in layers:
    if layer != layer[::-1]:
        return False
return True

Pseudocode Recursion:
if not root:
    return True

def compare(left, right):
    if left and not right:
        return False
    elif not left and right:
        return False
    elif not left and not right:
        return True
    elif left.val != right.val:
        return False
    else:
        return compare(left.left, right.right) and compare(left.right, right.left)

left = root.left
right = root.right
return compare(left, right)
```

---

### 3. Maximum Depth of Binary Tree
1. Recursion: use idea of post-order traversal, maxDepth = height of root, start from null node has height of 0.  
2. Iteration: use level-order traversal and find length of layer list. Space consuming.  

```
Pseudocode:
if not root:
    return 0

def getHeight(node):
    if not node:
        return 0
    return max(getHeight(node.left) + 1, getHeight(node.right) + 1)

return getHeight(root)
```

---

### 4. 111 Minimum Depth of Binary Tree
Given a binary tree, find its minimum depth. The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.  
Use the idea of post-order traversal and recursion. Make sure to adapt to the problem description for the termination conditions.  

```
Pseudocode:
if not root:
    return 0

def getMinHeight(node):
    if not node.left and not node.right:
        return 1
    elif not node.left and node.right:
        return 1 + getMinHeight(node.right)
    elif node.left and not node.right:
        return 1 + getMinHeight(node.left)
    else:
        return 1 + min(getMinHeight(node.left), getMinHeight(node.right))

return getMinHeight(root)
```

---

### 5. 222 Count Complete Tree Nodes
O(n) method to count nodes for every binary tree.  
Use property of complete tree to get a better solution.  

```
Pseudocode O(n):
if not root:
    return 0

def getNum(node):
    if not node:
        return 0
    return getNum(node.left) + getNum(node.right) + 1

return getNum(root)

Pseudocode Complete Tree:
if not root:
    return 0

def getNumComplete(node):
    if not node:
        return 0
    
    leftDep, rightDep = 1, 1
    cur = node
    while cur.left:
        leftDep += 1
        cur = cur.left
    cur = node
    while cur.right:
        rightDep += 1
        cur = cur.right
    
    if leftDep == rightDep:
        return 2 ** leftDep - 1
    else:
        return 1 + getNumComplete(node.left) + getNumComplete(node.right)

return getNumComplete(root)
```
