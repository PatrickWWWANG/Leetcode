# Day46 Dynamic Programming Part 09

---

### 1. 188 Best Time to Buy and Sell Stock IV
Find the maximum profit you can achieve. You may complete at most k transactions: i.e. you may buy at most k times and sell at most k times.  
Dynamic programming method, very similar to last problem.  
Note that in last problem, the state transition formula has a pattern. We can code this pattern.  
The length of dp state array varies according to the value of k.  
Initialize all buys in the first day.  
Can compress dp array to 2 entries because state transition only depends on the previous day.  

```
Pseudocode:
dp = [[0 for _ in range(2 * k + 1)] for _ in range(2)]
for i in range(1, 2 * k + 1, 2):
    dp[0][i] = -prices[0]

for m in range(1, len(prices)):
    for n in range(1, 2 * k + 1):
        dp[1][n] = max(dp[0][n], dp[0][n - 1] + (prices[m] * (-1) ** n))
    dp[0] = dp[1]

return dp[1][-1]
```
**Note**  
1. Note the (-1) ** n that controls if we add or subtract prices[m] for a given state.  
2. We need dp[0] = dp[1] after the nested for loop before if we place it before, we mess up the initialization.  
3. We can return dp[1][-1] because trade more times always include trade less times, that is, buy-sell-buy-sell includes buy-sell by doing another same day buy-sell that has no influence on profit.  

---

### 2. 309 Best Time to Buy and Sell Stock with Cooldown
Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions: After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).  
Similar to Best Time to Buy and Sell Stock II. With one day cool down after sell, the have stock state depends on not having stock state of 2 days ago.  
Can use 2 states, and [i - 2] to refer to 2 days ago. Or use 3 states, with the third one record the cool down state, equals to not having stock state of the day before.  

```
Pseudocode:
dp = [[0 for _ in range(3)] for _ in range(prices)]
dp[0][0] = -prices[0]

for i in range(len(prices)):
    dp[i][0] = max(dp[i - 1][0], dp[i - 1][2] - prices[i])
    dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i])
    dp[i][2] = dp[i - 1][1]

return dp[-1][1]
```
**Note**  
If use dp[i - 2] for cool down, need to ensure length of peices >= 2.

---

### 3. 714 Best Time to Buy and Sell Stock with Transaction Fee
You are given an array prices where prices[i] is the price of a given stock on the ith day, and an integer fee representing a transaction fee. Find the maximum profit you can achieve.  
Similar to Best Time to Buy and Sell Stock II. Simply subtract the fee when selling stock.  

```
Pseudocode:
dp = [[0 for _ in range(2)] for _ in range(len(prices))]
dp[0][0] = -prices[0]

for i in range(1, len(prices)):
    dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i])
    dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i] - fee)

return dp[-1][1]
```
