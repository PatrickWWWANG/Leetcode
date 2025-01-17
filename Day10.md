# Day10 Stack and Queue Part 01

---

### 1. 232 Implement Queue using Stacks
Implement a first in first out (FIFO) queue using only two stacks.  
Use two stacks to implement a queue.  

```
Pseudocode:
def __init__(self):
    self.s1 = []
    self.s2 = []

def push(self, x):
    if self.s2:
        while self.s2:
            self.s1.append(self.s2.pop())
    self.s1.append(x)

def pop(self):
    if self.s1:
        while self.s1:
            self.s2.append(self.s1.pop())
    out = self.s2.pop()
    return out

def peek(self):
    if self.s1:
        while self.s1:
            self.s2.append(self.s1.pop())
    return self.s2[-1]

def empty(self):
    return not (self.s1 or self.s2)
```

---

### 2. 225 Implement Stack using Queues
Implement a last-in-first-out (LIFO) stack using queues.  
Can be done using only one queue.  

```
Pseudocode:
def __init__(self):
    self.q = []

def push(self, x):
    self.q.append(x)

def pop(self):
    for _ in range(len(self.q) - 1):
        self.q.append(self.q.pop(0))
    return self.q.pop(0)

def top(self):
    for _ in range(len(self.q) - 1):
        self.q.append(self.q.pop(0))
    item = self.q.pop(0)
    self.q.append(item)
    return item

def empty(self):
    return not self.q
```

---

### 3. 20 Valid Parentheses
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.  
Use a stack to solve this problem, because LIFO ([{}]).  

```
Pseudocode:
if len(s) % 2 != 0:
    return False

from collections import deque
stack = deque()
for i in s:
    if i == '(':
        stack.append(')')
    elif i == '[':
        stack.append(']')
    elif i == '{':
        stack.append('}')
    else:
        if not stack or stack.pop() != i:
            return False

return not stack
```
**Note**  
There are three conditions for returning False.  

---

### 4. 1047 Remove All Adjacent Duplicates in String
You are given a string s consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them.  
We repeatedly make duplicate removals on s until we no longer can.  
Use a stack to solve this problem.  
Stack is appropriate for these problems because it records the previous element in iteration.  

```
Pseudocode:
stack = []
for i in s:
    if stack and i == stack[-1]:
        stack.pop()
    else:
        stack.append(i)

out = ''
while stack:
    out = stack.pop() + out
return out
```
**Note**  
Can use deque or list to immitate a stack.  