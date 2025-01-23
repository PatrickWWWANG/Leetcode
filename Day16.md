# Day16 Binary Tree Part 04

---

### 1. 513 Find Bottom Left Tree Value
Iteration: Level-order traversal and find the first node in last level.  
Recursion: The last row of the tree has the biggest depth. Use backtracking in traversal.  

```
Pseudocode Iteration:
from collections import deque
queue = deque()
layers = []
level = -1
if root:
    queue.append(root)

while queue:
    size = len(queue)
    level += 1
    layers.append([])
    while size > 0:
        node = queue.popleft()
        layers[level].append(node.val)
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
        size -= 1

return layers[-1][0]

Pseudocode Recursion:
maxDepth = -1
result = 0

def traversal(node, depth):
    nonlocal maxDepth, result
    if not node.left and not node.right:
        if depth > maxDepth:
            maxDepth = depth
            result = node.val
    if node.left:
        traversal(node.left, depth + 1)
    if node.right:
        traversal(node.right, depth + 1)

traversal(root, 1)
return result
```
**Caution**  
Remember to declear 'nonlocal' when reassigning nonlocal variables from a nested function.  

---

### 2. 112 Path Sum
Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.  
Recursion: Use backtarck.  

```
Pseudocode with a nonlocal variable:
if not root:
    return False
res = False
def traversal(node, sum):
    nonlocal res
    if node.val + sum == targetSum and not node.left and not node.right:
        res = True
    if node.left:
        traversal(node.left, sum + node.val)
    if node.right:
        traversal(node.right, sum + node.val)

traversal(root, 0)
return res

Pseudocode with no nonlocal variable:
if not root:
    return False
def traversal(node, sum):
    if not node.left and not node.right:
        if node.val + sum == targetSum:
            return True
        else:
            return False
    if node.left:
        if traversal(node.left, sum + node.val):
            return True
    if node.right:
        if traversal(node.right, sum + node.val):
            return True
    return False
return traversal(root, 0)
```

---

### 3. 113 Path Sum II
112 + Print Path  
Recursion: Use backtarck.  

```
Pseudocode:
if not root:
    return []
out = []
def traversal(node, sum, path):
    if node.val + sum == targetSum and not node.left and not node.right:
        path.append(node.val)
        out.append(list(path))
        path.pop()
    if node.left:
        path.append(node.val)
        traversal(node.left, sum + node.val, path)
        path.pop()
    if node.right:
        path.append(node.val)
        traversal(node.right, sum + node.val, path)
        path.pop()
traversal(root, 0, [])
return out
```

---

### 4. 106 Construct Binary Tree from Inorder and Postorder Traversal
The last element of he post-order array is the root.  
Use the root to cut left and right subtree in the in-order array.  
Use the post-order array to find the root for both subtrees.  
Recursion till end.  

```
Pseudocode:
if not postorder:
    return None
rootval = postorder[-1]
root = TreeNode(rootval)
if len(postorder) == 1:
    return root
idx_root_in = inorder.index(rootval)
left_inorder = inorder[: idx_root_in]
right_inorder = inorder[idx_root_in + 1 :]
left_postorder = postorder[: idx_root_in]
right_postorder = postorder[idx_root_in : -1]
root.left = self.buildTree(left_inorder, left_postorder)
root.right = self.buildTree(right_inorder, right_postorder)
return root
```

---

### 5. 105 Construct Binary Tree from Preorder and Inorder Traversal
Similar to 106, despite the root value is now the first element of the preorder array.  

```
Pseudocode:
if not preorder:
    return None
rootval = preorder[0]
root = TreeNode(rootval)
if len(preorder) == 1:
    return root
idx_root_in = inorder.index(rootval)
left_preorder = [1 : idx_root_in + 1]
right_preorder = [idx_root_in + 1 :]
left_inorder = [: idx_root_in]
right_inorder = [idx_root_in + 1 :]
root.left = self.buildTree(left_preorder, left_inorder)
root.right = self.buildTree(right_preorder, right_inorder)
return root
```
