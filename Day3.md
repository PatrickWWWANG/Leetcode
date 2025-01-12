# Day3 Linked List Part 01

---

### Define a Linked List Class  
```
class ListNode:
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
```

---

### 1. 203 Remove Linked List Elements
Method 1 Two cases:  
    1. Deleting head node: move the head node pointer to the next node  
    2. Deleting other nodes: set the next pointer to the next node  
Mothod 2 Dummy head:  
    Delete all node using case 2 above  

```
Pseudocode Method 1:
while head and head.val == target:
    head = head.next

if not head:
    return None

cur = head
while cur and cur.next:
    if cur.next.val == target:
        cur.next = cur.next.next
    else:
        cur = cur.next

return head
```
**Caution** In method1, it is important to check if the head or pointer is None in each while loop, otherwise error.  
Also, in case2, we stand at the current node and check if the next node equals to target value because we deal with singly linked list.  

```
Pseudocode Method 2:
dummy = ListNode()
dummy.next = head
cur = dummy

while cur and cur.next:
    if cur.next.val == target:
        cur.next = cur.next.next
    else:
        cur = cur.next

return dummy.next
```

---

### 2. 707 Design Linked List
```
Psuedocode
init:
    self.dummy = ListNode()
    self.size = 0

get(index):
    if index < 0 or index >= size:
        return -1
    
    for _ in range(index + 1):
        cur = cur.next
    return cur.val

addAtHead(val):
    head = ListNode()
    head.val = val
    head.next = dummy.next
    dummy.next = head
    size += 1

addAtTail(val):
    cur = dummy
    while cur.next:
        cur = cur.next
    cur.next = ListNode()
    cur.next.val = val
    size += 1

addAtIndex(index, val):
    if index == size:
        addAtTail(val)
    elif index >= 0 and index < size:
        cur = dummy
        for _ in range(index):
            cur = cur.next
        right = cur.next
        cur.next = ListNode()
        cur.next.val = val
        cur.next.next = right
        size += 1

deleteAtIndex(index):
    if index >= 0 and index < size:
        cur = dummy
        for _ in range(index):
            cur = cur.next
        cur.next = cur.next.next
        size -= 1
```
**Caution**  
1. Set up a dummy head in initialization to make methods easier  
2. Index of linked list starts at 0, be careful in for loops when setting pointers  
3. Make sure to update size in each method  
4. When deleting, set pointer to the node before the index node to delete it  

---

### 3. 206 Reverse Linked List
Method 1 Two pointers:  
    Use two pointers pre and cur. In each step, reverse the edge by set cur.next to pre.  
Method 2 Recirsion:  
    Use a recursive reverse function.  

```
Psuedocode Method 1:
pre = None
cur = head
while cur:
    temp = cur.next
    cur.next = pre
    pre = cur
    cur = temp
return pre

Psuedocode Method 2:
return reverse(None, head)

def reverse(pre, cur):
    if not cur:
        return pre
    temp = cur.next
    cur.next = pre
    return reverse(cur, temp)
```
**Note** the correspondence between method 1 and method 2.