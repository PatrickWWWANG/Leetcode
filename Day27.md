# Day27 Binary Tree Part 08

---

### 1. 669 Trim a Binary Search Tree
If the value of a node is larger than high, trim left subtree and return because there may be eligible nodes in left subtree.  
If the value of a node is smaller than high, trim right subtree and return because there may be eligible nodes in right subtree.  

```
Pseudocode:
if not root:
    return None

if root.val < low:
    right = self.trimBST(root.right, low, high)
    return right
elif root.val > high:
    left = self.trimBST(root.left, low, high)
    return left

root.left = self.trimBST(root.left, low, high)
root.right = self.trimBST(root.right, low, high)
return root
```
**Caution**  
Remember to use a variable to receive the return of a function.  

---

### 2. 108 Convert Sorted Array to Binary Search Tree
Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.  

```
Pseudocode:
n = len(nums)
if n == 0:
    return None
elif n == 1:
    return TreeNode(nums[0])

mid = n // 2
root = TreeNode(nums[mid])
root.left = self.sortedArrayToBST(nums[: mid])
root.right = self.sortedArrayToBST(nums[mid + 1 :])

return root
```

---

### 3. 538 Convert BST to Greater Tree
Given the root of a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus the sum of all keys greater than the original key in BST.  
For [a, b, c, ...] to become sum array, keep the rightmost item, inverse iterate and add the right item to left.  
Inverse in-order traversal of BST (right-root-left) and use a variable (two pointers) to track value to add.  

```
Pseudocode:
val_prev = 0

def traversal(node):
    nonlocal val_prev
    if not node:
        return
    traversal(node.right)
    root.val += val_prev
    val_prev = root.val
    traversal(node.left)

traversal(root)
return root
```
