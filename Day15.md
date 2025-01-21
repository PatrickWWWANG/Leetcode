# Day15 Binary Tree Part 03

---

### 1. 110 Balanced Binary Tree
Given a binary tree, determine if it is height-balanced. A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.  
When calculating height, record -1 if an unbalanced subtree is discovered and propagate the result upwards, otherwise calculate the height.  

```
Pseudocode:
if not root:
    return True

def getHeight(node):
    if not node:
        return 0
    left = getHeight(node.left)
    right = getHeight(node.right)
    if left == -1 or right == -1:
        return -1
    if abs(left - right) > 1:
        return -1
    else:
        return 1 + max(left, right)

return getHeight(root) != -1
```

---

### 2. 257 Binary Tree Paths
Given the root of a binary tree, return all root-to-leaf paths in any order.  
Use backtracking idea.  
Use recursion to find path. Record the path if it is found, pop the nodes in the path and try other way.  

```
Pseudocode:
def printPath(path):
    out = ''
    for val in path:
        out += str(val)
        out += '->'
    return out[:-2]

def findPath(node, path, result):
    path.append(node.val)
    if not node.left and not node.right:
        result.append(printPath(path))
        return
    if node.left:
        findPath(node.left, path, result)
        path.pop()
    if node.right:
        findPath(node.right, path, result)
        path.pop()

result = []
findPath(root, [], result)
return result
```
**Note**  
In different versions of solutions, note the using of list and string as path. List is mutable, so each time we pass path to the next recursion, we are working on the same list. Therefore pop() is necessary. String is immutable, so each time we do str += sth we created a new copy and pass this new object to the next recursion. The old copy is stored and will be retrived when we backtrack from the recursion. Therefore, in solutions using string for path pop() is not needed.  

---

### 3. 404 Sum of Left Leaves
Given the root of a binary tree, return the sum of all left leaves. A left leaf is a leaf that is the left child of another node.  
Use recursion to solve.  

```
Pseudocode:
if not root:
    return 0

if not root.left and not root.right:
    return 0

leftvalue = 0
if root.left:
    if not root.left.left and not root.left.right:
        leftvalue = root.left.val

return leftvalue + self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
```
**Note**  
The spirit of recursion: whatever itself contributes + whatever from left + whatever from right.  
In this problem, the self contribution comes from condition and value of left node.  

---

### 4. 222 Count Complete Tree Nodes
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
