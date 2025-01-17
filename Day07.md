# Day7 Hash Table Part 02

---

### 1. 454 4Sum II  
Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that: 0 <= i, j, k, l < n, and nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0  
Iterate nums1 and nums2 first, maintain a map to store the count of each sum. Iterate num3 and nums4, check if (0-sum) is in the map and maintain a counter.  

```
Pseudocode
n = len(nums1)
nummap = {}

for i in range(n):
    for j in range(n):
        sum = nums1[i] + nums2[j]
        if sum in nummap.keys():
            nummap[sum] += 1
        else:
            nummap[sum] = 1

cnt = 0
for k in range(n):
    for l in range(n):
        diff = 0 - nums3[k] - nums4[l]
        if diff in nummap.keys():
            cnt += nummap[diff]

return cnt
```
**Note**  
If we need to return index, then store index in map.  
If we need to return count, then store count in map.

---

### 2. 383 Ransom Note  
Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.  
Maintain an array to count each character in magazine. Then subtract one for corresponding element for each character in ransomNote. If any element goes below zero, return false.  

```
Pseudocode:
charlist = [0 for _ in range(30)]

for char in magazine:
    charlist[ord(char) - ord('a')] += 1

for char in ransomNote:
    charlist[ord(char) - ord('a')] -= 1
    if charlist[ord(char) - ord('a')] < 0:
        return False

return True
```
**Note**  
Use array because consist of lowercase English letters only.  

---

### 3. 15 3Sum  
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.  
Using map is complicated when dealing with duplicated triplets.  
**Main Idea** Sort and have the sum approach target from above or below.  
Sort the list and use two pointers.  
Iterate the list, and process the right side of the iterating element. Pointer left to the smallest on the right side and pointer right to the largest on the right side. If the sum smaller than zero, then move left pointer to the right. If the sum bigger then zero, then move right pointer to the left.  
Each time iterate to next element, check if it is the same as the previous element to deal with duplicate.  

```
Pseudocode:
output = []
n = len(nums)
nums.sort()

for i in range(n):
    if nums[i] > 0 or i > (n - 3):
        return output
    
    if i > 0 and nums[i] == nums[i - 1]:
        continue

    left, right = i + 1, n - 1
    while left < right:
        sum = nums[i] + nums[left] + nums[right]
        if sum > 0:
            right -= 1
        elif sum < 0:
            left += 1
        else:
            output.append([nums[i], nums[left], nums[right]])
            left += 1
            right -= 1
            while nums[left] == nums[left - 1] and left < right:
                left += 1
            while nums[right] == nums[right + 1] and left < right:
                right -= 1
```
**Caution**  
Note that the sequence of two if statements cannot be reversed. Otherwise the for loop may exit without a single execution of return. To prevent this, one can also add another return statement at the end.  
Remember to move left and right pointers when a valid triplet is found. Duplicated elements needed to be considered.  
Make sure to add "left < right" check when processing duplicated element when moving left and right pointers, otherwise it may cause index out of range error.  
Remember that the output is triplet of elements, not indexs.  

---

### 4. 18 4Sum
Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that: 0 <= a, b, c, d < n, a, b, c, and d are distinct and nums[a] + nums[b] + nums[c] + nums[d] == target.  
Use two pointers similar to 3Sum with two nested for loops and left and right pointers.  

```
Pseudocode:
output = []
nums.sort()
n = len(nums)

for i in range(n):
    if i > (n - 4):
        return output
    
    if i > 0 and nums[i] == nums[i - 1]:
        continue

    for j in range(i + 1, n):
        if j > (n - 3):
            break
        
        if j > (i + 1) and nums[j] == nums[j - 1]:
            continue
        
        left, right = j + 1, n - 1:
        while left < right:
            sum = nums[i] + nums[j] + nums[left] + nums[right]
            if sum < target:
                left += 1
            elif sum > target:
                right -= 1
            else:
                output.append([nums[i], nums[j], nums[left], nums[right]])
                left += 1
                right -= 1
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1
```
**Note**  
1. In this problem, we are working with a target not necessarily zero, be sure to check that.  
2. When check duplicate of j, make sure check "j > i + 1" because j is in range(i + 1, n).  
3. If want to include pruning, make sure it is "nums[i] > target and target > 0" to rule out the negative target case.  