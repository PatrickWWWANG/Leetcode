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

### 2. 