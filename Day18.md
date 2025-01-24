# Day18 Binary Tree Part 06

---

### 1. 530 Minimum Absolute Difference in BST
Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.  
In-order traversal of a BST returns a sorted array.  
Use two pointers to calculate difference and a variable to record minimum difference.  

```
Pseudocode:
if not root:
    return 0

minDiff = float('inf')
ptr = None
def traversal(node):
    nonlocal minDiff, ptr
    if not node:
        return
    traversal(node.left)
    if ptr and node.val - ptr.val < minDiff:
        minDiff = node.val - ptr.val
    ptr = node
    traversal(node.right)

traversal(root)
return minDiff
```

---

### 2. 501 Find Mode in Binary Search Tree
Given the root of a binary search tree (BST) with duplicates, return all the mode(s).  
Keep a count and a max count to get result with just one traversal.  

```
Pseudocode:
cnt, maxCnt = -1, -1
pre = None
out = []

def traversal(node):
    nonlocal cnt, maxCnt, pre, out
    if not node:
        return
    traversal(node.left)

    if not pre or (pre and node.val != pre.val):
        cnt = 1
    elif pre and node.val == pre.val:
        cnt += 1
    
    if cnt == maxCnt:
        out.append(node.val)
    elif cnt > maxCnt:
        maxCnt = cnt
        out = [node.val]
    
    pre = node

    traversal(node.right)

traversal(root)
return out
```
**Caution**  
Don't forget to update maxCnt when we have cnt > maxCnt.  

---

### 3. 236 Lowest Common Ancestor of a Binary Tree
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.  
Use post-order traversal and backtrack, return the common ancestor back.  
The root with both left and right not None is the lowest common ancestor.  

```
Pseudocode:
if not root:
    return None
if root = p or root = q:
    return root

self.lowestCommmonAncestor(root.left, p, q)
self.lowestCommmonAncestor(root.right, p, q)

if left and right:
    return root
elif left and not right:
    return left
elif right and not left:
    return right
else:
    return None
```
**Note**  
The condition of LCA is also p or q is considered.  
In this case, we return as soon as we reach LCA, no need to go to the subtree of LCA because another node is guaranteed to be in there.  
Be careful that p and q are TreeNode in this problem, not value.  
