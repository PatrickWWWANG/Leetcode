# Day4 Linked List Part 02

---

### 1. 24 Swap Nodes in Pairs
Given a linked list, swap every two adjacent nodes and return its head.

```
Pseudocode
if not head:
    return None
dummy = ListNode()
dummy.next = head
cur = dummy

while cur.next and cur.next.next:
    temp = cur.next
    temp2 = cur.next.next.next
    cur.next = cur.next.next
    cur.next.next = temp
    cur.next.next.next = temp2
    cur = cur.next.next

return dummy.next
```
**Caution**  
1. There are three edges to set in each loop  
2. Each time, process the next two nodes after the pointer  
3. Write "while cur.next and cur.next.next" to prevent AttributeError "NoneType"  

---

### 2. 19 Remove Nth Node From End of List
Use two pointers  

```
Pseudocode
if not head:
    return None
dummy = ListNode()
dummy.next = head
left, right = dummy, dummy

for _ in range(n + 1):
    right = right.next

while right:
    left = left.next
    right = right.next

left.next = left.next.next
return dummy.next
```
**Caution**  
Make sure the left pointer is finally placed before the node we want to remove.  

---

### 3. 160 Intersection of Two Linked Lists
Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.  
Find the lengths of both linked lists. Set two pointers to heads of both linked lists. Move the pointer of the longer linked list such that the remaining part has same length as another list. Move two pointers together to check for intersection.  

```
Pseudocode:
lenA, lenB = 0, 0
tempA, tempB = headA, headB
while tempA:
    lenA += 1
    tempA = tempA.next
while tempB:
    lenB += 1
    tempB = tempB.next

curA, curB = headA, headB
if lenA > lenB:
    diff = lenA - lenB
    for _ in range(diff):
        curA = curA.next
elif lenA < lenB:
    diff = lenB - lenA
    for _ in range(diff):
        curB = curB.next

while curA and curA != curB:
    curA = curA.next
    curB = curB.next

return curA
```

---

### 4. 142 Linked List Cycle II
Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.  
    1. Check if there is a cycle. Use two pointers, fast and slow. If two pointers meet at some point, there is cycle.
    2. Find begining of cycle. When fast and slow pointers meet, set another pointer starting from head and move one step each time with slow. They meet at the begining of cycle.  

```
Pseudocode1:
if not head or not head.next:
    return None

fast, slow = head.next.next, head.next
while fast != slow:
    if not fast or not fast.next:
        return None
    fast = fast.next.next
    slow = slow.next

cur = head
while cur != slow:
    cur = cur.next
    slow = slow.next

return cur

Psuedocode2:
if not head or not head.next:
    return None

fast, slow = head, head
while fast and fast.next:
    fast = fast.next.next
    slow = slow.next
    if fast == slow:
        cur = head
        while cur != slow:
            cur = cur.next
            slow = slow.next
        return cur
return None
```
**Note** Psuedocode is more concise and preferable.
