# Day43 Dynamic Programming Part 06

---

### 1. 322 Coin Change
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money. Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.  
Dynamic programming complete knapsack problem because we have infinite number of each kind of coin available.  
When use dp to find a minimum number, like the number of coins, we tend to initialize the dp array as float('inf').  
DP[j] = min(DP[j], DP[j - coins[i]] + 1), that is, take the minimum between what we have and number of coins to form (j - coins[i]) plus current coin.  
This problems asks for number of coins, which is unrelated to combination or permutation. Therefore, iteration order can be both item -> volumn and volumn -> item.  

```
Pseudocode:
if amount == 0:
    return 0

dp = [float('inf') for _ in range(amount + 1)]
dp[0] = 0

for i in range(len(coins)):
    for j in range(coins[i], amount + 1):
        dp[j] = min(dp[j], dp[j - coins[i]] + 1)

return dp[amount] if dp[amount] < float('inf') else -1
```

---

### 2. 279 Perfect Squares
Given an integer n, return the least number of perfect square numbers that sum to n.  
The idea is the same as the previous problem.  
For this problem, we need to generate the nums array in the code.  

```
Pseudocode:
nums = []
num = 1
while num * num <= n:
    nums.append(num * num)
    num += 1

dp = [float('inf') for _ in range(n + 1)]
dp[0] = 0

for i in range(len(nums)):
    for j in range(nums[i], n + 1):
        dp[j] = min(dp[j], dp[j - nums[i]] + 1)

return dp[n]

Pseudocode without Explicit Square Array:
dp = [float('inf') for _ in range(n + 1)]
dp[0] = 0

for i in range(1, floor(n ** 0.5) + 1):
    for j in range(i * i, n + 1):
        dp[j] = min(dp[j], dp[j - i * i] + 1)

return dp[n]
```

---

### 3. 139 Word Break
Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.  
Dynamic programming complete knapsack permutation kind of problem, because each word can be used multiple times and they can have different orders.  

```
Pseudocode:
dp = [False for _ in range(len(s) + 1)]
dp[0] = True

for j in range(len(s) + 1):
    for i in wordDict:
        if j >= len(i):
            dp[j] = dp[j] or (s[j - len(i) : j] == i and dp[j - len(i)])

return dp[-1]
```
**Note**  
In dynamic programming problem, update dp[j] must be some operation of current dp[j] and some other value. Be aware of that.  
