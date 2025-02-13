# Day37 Dynamic Programming Part 01

---

### Dynamic Programming
1. Define the dp array, understand the index of dp array  
2. Recursion formula  
3. Initialize dp array  
4. Sequence of iteration  
5. Print dp array (debug)  

---

### 1. 509 Fibonacci Number
The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. Given n, calculate F(n).  
Can use recursion, time consuming.  
Use dynamic programming.  

```
Pseudocode Recursion:
if n == 0:
    return 0
if n == 1:
    return 1
return self.fib(n - 1) + self.fib(n - 2)

Pseudocode Dynamic Programming:
if n == 0:
    return 0
elif n == 1:
    return 1
else:
    pre, prepre = 1, 0
    for _ in range(n - 1):
        temp = pre
        pre = pre + prepre
        prepre = temp
    return pre

Pseudocode Dynamic Programming Basic:
if n == 0:
    return 0
elif n == 1:
    return 1
else:
    dp = [0 for _ in range(n + 1)]
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

---

### 2. 70 Climbing Stairs
You are climbing a staircase. It takes n steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?  
Recusion formula is at n-2 stair climb 2 stairs and at n-1 stair climb 1 stair. So num[n] = num[n - 1] + num[n - 2].  

```
Pseudocode:
if n == 1:
    return 1
elif n == 2:
    return 2
else:
    dp = [1, 2]
    for _ in range(n - 2):
        sum = dp[0] + dp[1]
        dp[0] = dp[1]
        dp[1] = sum
    return dp[1]
```

---

### 3. 746 Min Cost Climbing Stairs
You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps. You can either start from the step with index 0, or the step with index 1. Return the minimum cost to reach the top of the floor.  
When len(cost) is 1, min cost is 0 because you can directly start above the first stair.  
When len(cost) is 2, min cost is min(cost[0], cost[1]) bacause you can start from either of these two and make one move to top.  
Beyond that, min cost is min((cost[s-1] + min cost to s-1), (cost[s] + min cost to s)).  

```
Pseudocode Using Full dp Array:
if len(cost) == 2:
    return min(cost)
else:
    dp = [0 for _ in range(len(cost))]
    dp[1] = min(cost[0], cost[1])
    for i in range(2, len(dp)):
        dp[i] = min((cost[i] + dp[i - 1]), (cost[i - 1] + dp[i - 2]))
    return dp[-1]

Pseudocode Using Two Elements:
if len(cost) == 2:
    return min(cost)
else:
    dp = [0, min(cost[0], cost[1])]
    for i in range(2, len(cost)):
        next = min((cost[i] + dp[1]), (cost[i - 1] + dp[0]))
        dp[0] = dp[1]
        dp[1] = next
    return dp[1]
```
