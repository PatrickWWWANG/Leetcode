# Day11 Stack and Queue Part 02

---

### 1. 150 Evaluate Reverse Polish Notation
You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation. Evaluate the expression.  
Use a stack to solve this. Iterate the tokens and push numbers into the stack. When iterating to an operator, pop two numbers, do the calculation, push the result back in.  
```
Pseudocode:
stack = []
for i in tokens:
    if i == '+' or i == '-' or i == '*' or i == '/':
        a = int(stack.pop())
        b = int(stack.pop())
        if i == '+':
            stack.append(b + a)
        elif i == '-':
            stack.append(b - a)
        elif i == '*':
            stack.append(b * a)
        elif i == '/':
            stack.append(int(b / a))
    else:
        stack.append(i)
return int(stack.pop())
```
**Caution**  
1. Be careful of the sequence of the calculations, especially for '/', should be 'b / a'.  
2. int() method truncates a decimal towards zero, whereas // and floor() takes the floor.  

---

### 2. 239 Sliding Window Maximum
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. Each time the sliding window moves right by one position. Return a list of the max of each sliding window.  
Use brute force is easy but will cause timeout.  
Design and maintain a monotonic decreasing queue to solve the problem.  

```
Pseudocode:
from collections import deque
out, monoD = [], deque()
for i in range(k):
    self.monoDpush(monoD, nums[i])
for j in range(len(nums) - k):
    out.append(monoD[0])
    if nums[j] == monoD[0]:
        monoD.popleft()
    self.monoDpush(monoD, num[j + k])
out.append(monoD[0])
return out

def MonoDpush(self, monoD, num):
    while monoD and num > monoD[-1]:
        monoD.pop()
    monoD.append(num)
```
**Note**  
Using collections.deque is much faster than using list in this case.  
list.pop(0) is O(n), while deque.popleft() is O(1).  

---

### 3. Top K Frequent Elements
Given an integer array nums and an integer k, return the k most frequent elements.  
Brute force need two dictionaries: num : freq and freq : num.  
Use a min-heap to improve solution.  

```
Pseudocode:
import heapq
cnt = {}
for i in nums:
    if i in cnt.keys():
        cnt[i] += 1
    else:
        cnt[i] = 1

heap = []
for key, value in cnt.items():
    heapq.heappush(heap, (value, key))
    if len(heap) > k:
        heapq.heappop(heap)

out = []
while heap:
    out.append(heapq.heappop(heap)[1])
return out
```
**Note**
1. Import heapq module in python to make a list a heap.  
2. Can push tuple, list into heap, order based on first element.  
3. If need max-heap, simply negate the ordering key.  