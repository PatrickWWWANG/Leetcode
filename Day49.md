# Day49 Dynamic Programming Part 11

---

### 1. 1143 Longest Common Subsequence
Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0. A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.  
The meaning of dp array for this problem is different from previous problem. Previous problem defines dp array as length of repeated subarray ends exactly at position i - 1 and j - 1. For this problem, dp array means the length of longest common subsequence up until position i - 1 and j - 1. The subsequence doesn't necessarily end at these positions.  
This is because previous problem requires continuous repeated subarray, so if we meet one unequal element, we reset length to 0. For this problem, common subsequence can be discontinuous. Therefore, we can inherit longest common sequence even though we have unequal elements at a position.  
If text1[i - 1] == text2[i - 1], then dp[i][j] is both texts move back one position longest common subsequence add 1, that is dp[i - 1][j - 1] + 1.  
If text1[i - 1] != text2[i - 1], then dp[i][j] is equal to the bigger between text1 move back one position and text2 move back one position. That is max(dp[i][j - 1], dp[i - 1][j]).  

```
Pseudocode:
dp = [[0 for _ in range(len(text2) + 1)] for _ in range(len(text1) + 1)]

for i in range(1, len(text1) + 1):
    for j in range(1, len(text2) + 1):
        if text1[i - 1] == text2[j - 1]:
            dp[i][j] = dp[i - 1][j - 1] + 1
        else:
            dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])

return dp[-1][-1]
```
**Note**  
This problem can't be compressed to 1-D dp array because we reply on dp[i][j - 1] term.  

---

### 2. 1035 Uncrossed Lines
You are given two integer arrays nums1 and nums2. We write the integers of nums1 and nums2 (in the order they are given) on two separate horizontal lines. We may draw connecting lines: a straight line connecting two numbers nums1[i] and nums2[j] such that: nums1[i] == nums2[j], and the line we draw does not intersect any other connecting (non-horizontal) line. Return the maximum number of connecting lines we can draw in this way.  
This problem is essentially the same as longest common subsequence.  
Maximum number of uncrossed lines connect in one direction. We are trying to find the same subsequence, which is longest common subsequence.  

```
Pseudocode:
dp = [[0 for _ in range(len(nums2) + 1)] for _ in range(len(nums1) + 1)]

for i in range(1, len(nums1) + 1):
    for j in range(1, len(nums2) + 1):
        if nums1[i - 1] == nums2[j - 1]:
            dp[i][j] = dp[i - 1][j - 1] + 1
        else:
            dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])

return dp[-1][-1]
```

---

### 3. 53 Maximum Subarray
Given an integer array nums, find the subarray with the largest sum, and return its sum.  
In greedy solution, we keep track of a sum and add each item to sum. If adding one item causing the sum smaller than the item itself, we use the item as the sum. We return the max sum recorded in iteartion.  
In divide and conquer solution, we recursively find the max of left subarray, right subarray, and cross-mid subarray.  
In dynamic programming solution, the dp array means the sum of maximum subarray that ends exactly at this position. This is because we are finding continuous subarray in this problem.  
The transition of dp array has two possibilities: continue previous subarray and add current num, or use current num itself as the new subarray.  
Initialize dp[0] as the first num.  
Return max(dp) bacause it's a continuous subarray problem.  

```
Pseudocode:
dp = [0 for _ in range(len(nums))]
dp[0] = nums[0]

for i in range(1, len(nums)):
    dp[i] = max(dp[i - 1] + nums[i], nums[i])

return max(dp)

Pseudocode Using Compressed DP Array:
dp = [nums[0], 0]

maxsum = nums[0]
for i in range(1, len(nums)):
    dp[1] = max(dp[0] + nums[i], nums[i])
    if dp[1] > maxsum:
        maxsum = dp[1]
    dp[0] = dp[1]

return maxsum
```
**Note**  
In compressed dp array method, result recorder maxsum should be initialized to nums[0]. If initialized to 0, it can't deal with all negative nums case.  

---

### 4. 392 Is Subsequence
Given two strings s and t, return true if s is a subsequence of t, or false otherwise.  
Can use a pointer.  
Dynamic programming solution is find the maximum common subsequence and check if it is s.  
Pointer method is more efficient and DP method is more general.  

```
Pseudocode Using Pointer:
if not s:
    return True

i = 0
for j in t:
    if j == s[i]:
        i += 1
        if i == len(s):
            return True
return False

Pseudocode Using DP:
dp = [[0 for _ in range(len(t) + 1)] for _ in range(len(s) + 1)]

for i in range(1, len(s) + 1):
    for j in range(1, len(t) + 1):
        if s[i - 1] == t[j - 1]:
            dp[i][j] = dp[i - 1][j - 1] + 1
        else:
            dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])

return dp[-1][-1] == len(s)
```
