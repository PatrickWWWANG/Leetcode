# Day45 Dynamic Programming Part 08

---

### 1. 121 Best Time to Buy and Sell Stock
You are given an array prices where prices[i] is the price of a given stock on the ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.  
This problem can be easily solved using two variables.  
Use dynamic programming to prepare for further problems.  
We need a 2-D dp array, where the first entry of each day is the cost of having the stock, and the second entry is gain of not having the stock.  
Initialize first day, cost is -prices[0], and gain is 0.  
Transition formula for cost is dp[i][0] = max(dp[i - 1][0], -prices[i]), that is, compare cost of buying in previous days and cost of buying now to find the better one. -prices[i] is essentialy 0 - prices[i], because we only buy stock once, so for any buy we start at 0.  
Transition formula for gain is dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i]), that is, compare gain of selling in previous days and gain of selling now to find the better one. Note that if selling now, the cost is the cost one day before, and the difference between cost and today's price is gain.  

```
Pseudocode Using Two Variables:
minp = prices[0]
maxg = 0
for i in prices:
    if i < minp:
        minp = i
    if i - minp > maxg:
        maxg = i - minp
return maxg

Pseudocode Using Dynamic Programming:
dp = [[0 for _ in range(2)] for _ in range(len(prices))]
dp[0][0] = -prices[0]
dp[0][1] = 0

for i in range(1, len(prices)):
    dp[i][0] = max(dp[i - 1][0], -prices[i])
    dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i])

return max(dp[-1])
```
**Caution**  
The iteration of prices starting from position 1. 

---

### 2. 122 Best Time to Buy and Sell Stock II
On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. Find and return the maximum profit you can achieve.  
Brute force: iterate prices and add up all price increases.  
Dynamic programming: similar to last problem, the change is we can buy and sell multiple times. Therefore, for any buy the start point is the money of not having stock the previous day, that is dp[i - 1][1].  

```
Pseudocode Brute Force:
sum = 0
for i in range(len(peices) - 1):
    if prices[i + 1] - prices[i] > 0:
        sum += (prices[i + 1] - prices[i])
return sum

Pseudocode Using Dynamic Programming:
dp = [[0 for _ in range(2)] for _ in range(len(prices))]
dp[0][0] = -prices[0]

for i in range(1, len(prices)):
    dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i])
    dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i])

return dp[-1][1]
```
**Note**  
Can directly return dp[-1][1] max cash must happen with not holding stock on the last day.  

---

### 3. 123 Best Time to Buy and Sell Stock III
Find the maximum profit you can achieve. You may complete at most two transactions.  
Use dynamic programming state representation of length 5: no action, first time have stock, first time not have stock, second time have stock, second time not have stock.  
**Be careful at initialization, we need to initialize both first time have stock and second time have stock to -price[i].** We can consider it as buy-sell-buy on the first day.  
State transition similar to previous problems.  

```
Pseudocode:
dp = [[0 for _ in range(5)] for _ in range(len(prices))]
dp[0][1] = -prices[0]
dp[0][3] = -prices[0]

for i in range(1, len(prices)):
    dp[i][1] = max(dp[i - 1][1], -prices[i])
    dp[i][2] = max(dp[i - 1][2], dp[i - 1][1] + prices[i])
    dp[i][3] = max(dp[i - 1][3], dp[i - 1][2] - prices[i])
    dp[i][4] = max(dp[i - 1][4], dp[i - 1][3] + prices[i])

return max(dp[-1][0], dp[-1][2], dp[-1][4])
```
