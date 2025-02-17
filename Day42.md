# Day42 Dynamic Programming Part 05

---

### Complete Knapsack
Each item can be used infinite times. (1 time in 0-1 knapsack)  
Iterate knapsack volumn with regular order in dp array (1-D) iteration.  
Can put an item multiple times into the knapsack when iterating one item.  
For pure complete knapsack problem, can do iteration order item -> volumn or volumn -> item.  

---

### 1. 518 Coin Change II
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money. Return the number of combinations that make up that amount. If that amount of money cannot be made up by any combination of the coins, return 0.  
Complete knapsack dynamic programming problem.  
Iterate amount and coins from left to right such that we can consider that combinations with multiple same coins.  
DP transition is dp[j] + dp[j - coins[i]], this is the number of combinations without coins[i], plus with 1 extra coins[i] (number of combinations is the same as dp[j - coins[i]] in this situation).  

```
Pseudocode:
dp = [0 for _ in range(amount + 1)]
dp[0] = 1

for i in range(len(coins)):
    for j in range(coins[i], amount + 1):
        dp[j] = dp[j] + dp[j - coins[i]]

return dp[amount]
```
**Note**
Iteration order item -> volumn: combination.  
Iteration order volumn -> item: permutation (bacause [1, 2] and [2, 1] will be added individually).  

---

### 2. 377 Combination Sum IV
Given an array of distinct integers nums and a target integer target, return the number of possible combinations that add up to target.  
This problem is very similar to previous one, despite it is asking for permutation.  
Use the volumn -> item iteration order for permutation as mentioned above.  

```
Pseudocode:
dp = [0 for _ in range(target + 1)]
dp[0] = 1

for j in range(target + 1):
    for i in range(len(nums)):
        if j >= nums[i]:
            dp[j] += dp[j - nums[i]]

return dp[target]
```

---

### 3. 70 Climbing Stairs (Advanced)
You are climbing a staircase. It takes n steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?  
Advanced: each time you can climb 1, 2, ..., m steps, in how many distinct ways can you reach the top.  
This is actually the same as previous problem. We try to find the permutation of 1, 2, ..., m that add up to target.  

```
Pseudocode:
m = 2
nums = list(range(1, m + 1))

dp = [0 for _ in range(n + 1)]
dp[0] = 1

for j in range(n + 1):
    for i in range(m):
        if j >= nums[i]:
            dp[j] += dp[j - nums[i]]

return dp[n]
```
