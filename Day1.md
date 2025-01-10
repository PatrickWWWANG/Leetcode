# Day1 Array Part 01

---

### 1. 704 Binary Search
Determine if the target is in the sorted array. Return index if Trure, return -1 if False.  
We usually define [left, right):  
    1. In while loop, it should be "**left < right**, not <="  
    2. In if loop, when updating left and right boundary, **left = mid + 1; right = mid**  

```
Pseudocode:  
left = 0  
right = len(Array)  
while left < right:  
    mid = (left + right) // 2  
    if Array[mid] > target:  
        right = mid  
    elif Array[mid] < target:  
        left = mid + 1  
    else:  
        return mid  
return -1  
```

### 2. 27 Remove Element
Remove all occurrences of val in nums. Return size of remaining array.  
Two pointers:  
    Fast pointer traverse nums. If it points to a number not equal to val, assign the number to slow pointer position.  

```
Pseudocode:  
slow, fast = 0, 0
for fast in range(len(nums)):
    if nums[fast] != val:
        nums[slow] = nums[fast]
        slow += 1
return slow
```

Caution: We had slow += 1 after the last update, so the index of slow = size of array we want to keep.  

---

### 3. 977 Squares of a Sorted Array
Square all elements in a sorted array and store in a sorted array.  
    1. Brute force: square and sort  
    2. Two pointers: after square, the array must be big to small to big. Two points move from both sides to center.  

```
Pseudocode:
k = len(nums) - 1
i, j = 0, k
while i <= j:
    if nums[i]*nums[i] > nums[j]*nums[j]:
        result[k] = nums[i]*nums[i]
        k -= 1
        i += 1
    else:
        result[k] = nums[j]*nums[j]
        k -= 1
        j -= 1
return result
```
