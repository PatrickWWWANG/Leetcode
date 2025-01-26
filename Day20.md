# Day20 Binary Tree Part 07

---

### 1. 235 Lowest Common Ancestor of a Binary Search Tree
Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.  
Can use the traditional method for ant binary tree.  
Improve using property of BST: **root < both p and q, go right; root > both p and q, go left; root in between, this is common ancestor**. Can do recursion or iteration.  

```
Pseudocode Traditional:
if not root:
    return None

if root == p or root == q:
    return root

left = self.lowestCommonAncestor(root.left, p, q)
right = self.lowestCommonAncestor(root.right, p, q)

if left and right:
    return root
elif left and not right:
    return left
elif right and not left:
    return right
else:
    return None

Pseudocode Improved Recursion:
if (root.val >= p.val and root.val <= q.val) or (root.val <= p.val and root.val >= q.val):
    return root

elif root.val < p.val and root.val < q.val:
    return self.lowestCommonAncestor(root.right, p, q)

elif root.val > p.val and root.val > q.val:
    return self.lowestCommonAncestor(root.left, p, q)

Pseudocode Improved Iteration:
while root:
    if root.val < p.val and root.val < q.val:
        root = root.right
    elif root.val > p.val and root.val > q.val:
        root = root.left
    else:
        return root
```

---

### 2. 701 Insert into a Binary Search Tree
All insertion into a BST can be done at a leaf position.  
Simply compare values and find a direction.  

```
Pseudocode:
if not root:
    return TreeNode(val)

if val < root.val and not root.left:
    root.left = TreeNode(val)
elif val > root.val and not root.right:
    root.right = TreeNode(val)
elif val < root.val:
    self.insertIntoBST(root.left, val)
else:
    self.insertIntoBST(root.right, val)

return root
```

---

### 3. 450 Delete Node in a BST
Cases:  
    1. Key not found  
    2. Key is a leaf: simply remove  
    3. Key.left has node and key.right is None: parent points to key.left  
    4. Key.right has node and key.left is None: parent points to key.right  
    5. Key has two childs: attach key.left to leftmost child in key.right  
Can use recursion or iteration, recursion is simpler.  

```
Pseudocode:
if not root:
    return None

if key == root.val:
    if not root.left and not root.right:
        return None
    elif root.left and not root.right:
        return root.left
    elif root.right and not root.left:
        return root.right
    else:
        cur = root.right
        while cur.left:
            cur = cur.left
        cur.left = root.left
        return root.right
elif key < root.val:
    root.left = self.deleteNode(root.left, key)
else:
    root.right = self.deleteNode(root.right, key)

return root
```
