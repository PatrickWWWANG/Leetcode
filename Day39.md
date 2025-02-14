# Day39 Dynamic Programming Part 03

---

### 0-1 Knapsack 2-D DP Array
0-1 Knapsack: knapsack volumn m, n items, weight w, value v, each item can be selected only once.  
Brute force uses backtracking, time complexity O(2^n).  
DP[i][j] means max value with only items 0-i available and knapsack volumn j.  
DP[i][j] = max(DP[i - 1][j], DP[i - 1][j - w[i]] + v[i]).  
It is the max value between not taking item i and taking item i.  
Initialize first column (j = 0) to 0, first row (i = 0) j < w[0] to 0, j >= w[0] to v[0].  
The iteration sequence is not strict (item -> knapsack or knapsack -> item).  
Iterate left to right or right to left, both works(knapsack).  

---

### 0-1 Knapsack 1-D DP Array
Can reduce the dp array to 1-D to save space.  
Iterate item first, then iterate kanpsack volumn from left to right.  
DP[j] = max(DP[j], DP[j - w[i]] + v[i])  
Initilize first array all 0, first iteration of item for loop takes care of item 0.  
The iteration sequence is strict (item -> knapsack).  
**Iterate knapsack from right to left.** This is becasue we need some thing same as DP[i - 1][j - w[i]] in 2-D case, if we iterate left to right, the left value has been overwritten when need it from right item. So, strict iteration order.  

---

### 1. 416 Partition Equal Subset Sum
Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.  
See it as an abstract 0-1 knapsack problem.  
Volumn is sum target, which is 1/2 of sum of nums array.  
nums[i] is both v[i] and w[i].  
Check if we can select some element add to target is to check is dp[target] == target.  

```
Pseudocode:
tot_sum = sum(nums)
if tot_sum % 2 == 1:
    return False
target = tot_sum // 2

dp = [0 for _ in range(target + 1)]
for i in range(len(nums)):
    for j in range(target, nums[i] - 1, -1):
        dp[j] = max(dp[j], dp[j - nums[i]] + nums[i])
    if dp[-1] == target:
        return True

return False
```
