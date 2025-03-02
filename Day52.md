# Day52 Monotone Stack Part 01

---

### Monotone Stack
Monotone stack is a stack with elements monotone increase or decrease.  
Monotone stack is good for problems finding the first bigger or smaller item on thr left or right side of the current item in an array.  
Monotone increase stack finds first bigger element, monotone decrease stack finds first smaller element.  
Monotone increase stack is a stack with biggest member at the bottom of the stack.  

---

### 1. 739 Daily Temperatures
Use monotone increase stack, which stores the index of items.  
While the itrating item is bigger than the top of the stack, we pop the stack and calculate difference in index to put into the ans array.  

```
Pseudocode:
st = [0]
ans = [0 for _ in range(len(temperatures))]

for i in range(1, len(temperatures)):
    while temperatures[i] > temperatures[st[-1]]:
        idx = st.pop()
        ans[idx] = i - idx
    st.append(i)

return ans
```
**Note**  
We are finding the strictly bigger next item in this problem, so we use '>' in the while loop.  

---

### 2. 496 Next Greater Element I
You are given two distinct 0-indexed integer arrays nums1 and nums2, where nums1 is a subset of nums2. For each 0 <= i < nums1.length, find the index j such that nums1[i] == nums2[j] and determine the next greater element of nums2[j] in nums2. If there is no next greater element, then the answer for this query is -1.
Use a monotone increase stack to find the next bigger element for each element in nums2. If the element is in nums1, record the next bigger element in ans array.  
Use a map to reflct elements in nums1 to index in nums1.  

```
Pseudocode:
if not nums1:
    return []

st = []
ans = [-1 for _ in range(len(nums1))]
nums1map = {}

for i in range(len(nums1)):
    nums1map[nums[i]] = i

for j in range(len(nums2)):
    while st and nums2[j] > nums2[st[-1]]:
        idx = st.pop()
        if nums2[idx] in nums1:
            ans[nums1map[nums2[idx]]] = nums2[j]
    st.append(j)

return ans
```

---

### 3. 503 Next Greater Element II
Given a circular integer array nums (i.e., the next element of nums[nums.length - 1] is nums[0]), return the next greater number for every element in nums. The next greater number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return -1 for this number.
Can also use module to immitate circular array iteration.  
Since we are finding the next greater element in this circular integer array, we simply iterate the array twice.  
Use a monotone increase stack.  

```
Pseudocode Using Idxlist:
st = []
ans = [-1 for _ in range(len(nums))]
idxlist = list(range(len(nums))) * 2

for i in idxlist:
    while st and nums[i] > nums[st[-1]]:
        idx = st.pop()
        ans[idx] = nums[i]
    st.append(i)

return ans

Pseudocode Using Module:
n = len(nums)
st = []
ans = [-1 for _ in range(n)]

for i in range(2 * n):
    while nums[i % n] > nums[st[-1]]:
        idx = st.pop()
        ans[idx] = nums[i % n]
    st.append(i % n)

return ans
```
**Note**  
In module method, we iterate in range 2 * n because we need to cover the array twice.  
