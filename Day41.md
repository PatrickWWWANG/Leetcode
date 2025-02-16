# Day41 Dynamic Programming Part 04

---

### 1. 1049 Last Stone Weight II
We are playing a game with the stones. On each turn, we choose any two stones and smash them together. Return the smallest possible weight of the left stone. If there are no stones left, return 0. 
Use dynamic programming.  
We try to select stones that make up a value as close to half of the total value as possible.  

```
Pseudocode:
if len(stones) == 1:
    return stones[0]

target = sum(stones) // 2
dp = [0 for _ in range(target + 1)]
for i in range(len(stones)):
    for j in range(target, stones[i] - 1, -1):
        dp[j] = max(dp[j], dp[j - stones[i]] + stones[i])

return sum(stones) - dp[target] * 2
```
**Note**  
We eliminate 2 times dp[target] from stones to get final answer, because we eliminated 2 times that value from stones by collision.  

---

### 2. 494 Target Sum
You are given an integer array nums and an integer target. You want to build an expression out of nums by adding one of the symbols '+' and '-' before each integer in nums and then concatenate all the integers. Return the number of different expressions that you can build, which evaluates to target.  
Use dynamic programming.  
DP[i][j] means numbers of different method to select nums 0...i to **fill** knapsack with volumn j.  
DP[i][j] = DP[i-1][j] + DP[i-1][j-nums[i]], which is not choose nums[i] + choose nums[i].  
Then compres to 1-D dp array.  
In this problem, we need to divide sum(nums) - target to 2 euqal parts, one is minus sign and another is plus sign. Therefore, if sum(nums) - target can't divides 2, we automatically return 0 bacause there is no such way exist.  
Initialize the first row using first item. dp[0] = 1 because there is 1 method to fill knapsack with volumn 0, that is not taking the item.  

```
Pseudocode:
if (sum(nums) - target) % 2 == 1:
    return 0

comb_sum = (sum(nums) - target) // 2
if comb_sum < 0:
    return 0
else:
    dp = [0 for _ in range(comb_sum + 1)]
    dp[0] = 1
    if nums[0] <= comb_sum:
        dp[nums[0]] += 1
    for i in range(1, len(nums)):
        for j in range(comb_sum, nums[i] - 1, -1):
            dp[j] = dp[j] + dp[j - nums[i]]
    return dp[comb_sum]
```
**Caution**  
Return 0 when comb_sum < 0 bacause target is too big to reach in this case.  
Use dp[nums[0]] += 1 bacause there is case nums[0] == 0, then we can have dp[0] == 2.  

---

### 3. 474 Ones and Zeros
You are given an array of binary strings strs and two integers m and n. Return the size of the largest subset of strs such that there are at most m 0's and n 1's in the subset.  
Use dynamic programming. This is a **Muptiple Kanpsack** problem.  
We have item with **multiple** elements, and **multiple** knapsacks to constrain these element. Therefore we need a **multi-dimensional** dp array to handle this problem.  
We use a 3-D dp array, with dimensions item, m, and n. Then, we compress it to 2-D dp array.  
DP update is max between taking current str and not taking current string.  

```
Pseudocode:
dp = [[0 for _ in range(m + 1)] for _ in range(n + 1)]

for i in range(len(strs)):
    ones = strs.count('1')
    zeros = strs.count('0')
    for j in range(n, ones - 1, -1):
        for k in range(m, zeros - 1, -1):
            dp[j][k] = max(dp[j - ones][k - zeros] + 1, dp[j][k])

return dp[n][m]
```
