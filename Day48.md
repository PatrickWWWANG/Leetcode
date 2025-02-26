# Day48 Dynamic Programming Part 10

---

### 1. 300 Longest Inceasing Subsequence
Given an integer array nums, return the length of the longest strictly increasing subsequence.  
DP array means longest strictly increasing subsequence ending at position i.  
For each position, iterate from start of nums to i. For each nums[j] that is smaller than nums[i], dp[i] is the bigger between itself and dp[j] + 1. dp[j] + 1 means add nums[i] to existing longest strictly increasing subsequence ending at j.  
Initialize as 1 because each num is strictly increasing subsequence itself.  

```
dp = [1 for _ in range(len(nums))]

for i in range(len(nums)):
    for j in range(i):
        if nums[i] > nums[j]:
            dp[i] = max(dp[i], dp[j] + 1)

return max(dp)
```

---

### 2. 674 Longest Continuous Inceasing Subsequence
Given an unsorted array of integers nums, return the length of the longest continuous increasing subsequence (i.e. subarray). The subsequence must be strictly increasing.  
DP array means longest continuous strictly increasing subsequence ending at position i.  
If nums[i] bigger than nums[i - 1], dp[i] is dp[i - 1] + 1.  
Initialize as 1 because each num is strictly increasing subsequence itself.  

```
Pseudocode:
dp = [1 for _ in range(len(nums))]

for i in range(1, len(nums)):
    if nums[i] > nums[i - 1]:
        dp[i] = dp[i - 1] + 1

return max(dp)
```

---

### 3. 718 Maximum Length of Repeated Subarray
Given two integer arrays nums1 and nums2, return the maximum length of a subarray that appears in both arrays.  
We need a 2-D dp array of size len(nums1) + 1 * len(nums2) + 1.  
DP[i][j] means longest repeated subarray ending at nums1[i] and nums2[j].  
When nums1[i - 1] == nums2[j - 1], we update dp[i][j] = dp[i - 1][j - 1] + 1. This is because we add a dummy head before each list to deal the first num of each list. Otherwise dp[i - 1][j - 1] will go out of range.  
nums1[i - 1] == nums2[j - 1] means that the longest repeated subarray now is the longest repeated subarray ending at previous position of both lists plus 1.  
Initialize as 0 because if there is no same item, the longest repeated subarray is 0.  
Return the max value of the whole dp matrix.  

```
Pseudocode:
dp = [[0 for _ in range(len(nums2) + 1)] for _ in range(len(nums1) + 1)]

for i in range(1, len(nums1) + 1):
    for j in range(1, len(nums2) + 1):
        if nums1[i - 1] == nums2[j - 1]:
            dp[i][j] = dp[i - 1][j - 1] + 1

return max(max(row) for row in dp)

Pseudocode Using 1-D DP Array:
dp = [0 for _ in range(len(nums2) + 1)]

result = 0
for i in range(len(nums1)):
    for j in range(len(nums2), 0, -1):
        if nums1[i] == nums2[j - 1]:
            dp[j] = dp[j - 1] + 1
        else:
            dp[j] = 0
    result = max(result, max(dp))

return result
```
**Note**  
In 1-D DP Array solution, we need to set dp[j] to 0 when nums1[i] != nums2[j - 1] because this means there is no common subarries ending exactly at these two positions.  
We also need a result variable to keep track of max(dp) of each step because the solution may be covered in the next iteration.  
**Caution**  
In subarray problems, remember dp array means subarray meeting requirements that ends exactly at this position. Therefore, the final answer may not be in the last step of dynamic programming iteration.  