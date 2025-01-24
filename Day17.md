# Day17 Binary Tree Part 05

---

### 1. 654 Maximum Binary Tree
Find the max element and index, get two subarrays, construct using method similar to 105 and 106.  

```
Pseudocode:
if not nums:
    return None
rootval = -1
root_idx = -1
for i in range(len(nums)):
    if nums[i] > rootval:
        rootval = nums[i]
        root_idx = i
root = TreeNode(rootval)
if len(nums) == 1:
    return root
left_sub = nums[: root_idx]
right_sub = nums[root_idx + 1 :]
root.left = self.constructMaximumBinaryTree(left_sub)
root.right = self.constructMaximumBinaryTree(right_sub)
return root
```

---

### 2. 617 Merge Two Binary Trees
Recursion: use pre-order traversal.  

```
Pseudocode:
if not root1 and not root2:
    retrun None
if not root1:
    return root2
if not root2:
    return root1

root1.val += root2.val
root1.left = self.mergeTrees(root1.left, root2.left)
root1.right = self.mergeTrees(root1.right, root2.right)
return root1
```
**Note**  
Reuse tree1 rather than create a new tree to save space.  

---

### 3. 700 Search in a Binary Search Tree
Recuesion and iteration.
You are given the root of a binary search tree (BST) and an integer val. Find the node in the BST that the node's value equals val and return the subtree rooted with that node. If such a node does not exist, return null.  

```
Pseudocode Recursion:
if not root.left and not root.right and root.val != val:
    return None

if root.val == val:
    return root

if root.val > val and root.left:
    return self.searchBST(root.left, val)
elif root.val < val and root.right:
    return self.searchBST(root.right, val)
else:
    return None

Pseudocode Iteration:
while root and root.val != val:
    if val < root.val and root.left:
        root = root.left
    elif val > root.val and root.right:
        root = root.right
    else:
        root = None

return root
```

---

### 4. 98 Validate Binary Search Tree
Given the root of a binary tree, determine if it is a valid binary search tree (BST).  
**PROPERTY OF BST:** in-order traversal returns a sorted array.  
Do in-order traversal and output a list and check.  
Assign a max value and check during traversal to be more efficient.  

```
Pseudocode with Array:
if not root:
    return True

out = []
def dfs(node):
    if not node:
        return
    dfs(node.left)
    out.append(node.val)
    dfs(node.right)

dfs(root)
return out == sorted(list(set(out)))

Pseudocode with Comparing in Traversal:
maxNum = float(-'inf')

def valid(node):
    nonlocal maxNum
    if not node:
        return True
    left = valid(node.left)
    if node.val > maxNum:
        maxNum = node.val
    else:
        return False
    right = valid(node.right)
    return left and right

return valid(root)
```
**Caution**
list.sort() modifies original list and returns None.  
sorted(list) doesn't modify original list and returns a new list.  
Set() removes duplicate but has random order.  
Use float('-inf') to represent negative infinity in Python.  
