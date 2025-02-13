# Day38 Dynamic Programming Part 02

---

### 1. 62 Unique Paths
There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time. Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.  
Use dynamic programming.  
Dp array means unique paths to each grid.  
Initialize to 1 bacause with only right or down move, only 1 path to each grid in first row and first column.  
Path to each grid is sum of path to left grid and path to upper grid.  

```
Pseudocode:
dp = [[1 for _ in range(n)] for _ in range(m)]
for i in range(1, m):
    for j in range(2, n):
        dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
return dp[m - 1][n - 1]
```

---

### 2. 63 Unique Paths II
You are given an m x n integer array grid. There is a robot initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time. An obstacle and space are marked as 1 or 0 respectively in grid. A path that the robot takes cannot include any square that is an obstacle. Return the number of possible unique paths that the robot can take to reach the bottom-right corner.  
If start is obstacle or target is obstacle, automatically return 0.  
Iterate all grids by cases.  
Set num path to 0 for obstacle grids because not reachable.  

```
Pseudocode:
if obstacleGrid[0][0] == 1 or obstacleGrid[-1][-1] == 1:
    return 0

dp = [[0 for _ in row] for row in obstacleGrid]
for i in range(len(obstacleGrid)):
    for j in range(len(obstacleGrid[0])):
        if i == 0 and j == 0:
            dp[i][j] == 1
        elif obstacleGrid[i][j] == 1:
            dp[i][j] == 0
        elif i == 0:
            dp[i][j] = dp[i][j - 1]
        elif j == 0:
            dp[i][j] = dp[i - 1][j]
        else:
            dp[i][j] = dp[i][j - 1] + dp[i - 1][j]

return dp[-1][-1]
```

---

### 3. 343 Integer Break
Given an integer n, break it into the sum of k positive integers, where k >= 2, and maximize the product of those integers. Return the maximum product you can get.  
Dp array dp[n] represents max product of n.  
Two condition for a number i:  
    (1) Two number j and i - j, then product is i * (i - j)  
    (2) Three or more numbers, then product is j * dp[i - j] because dp[i - j] is the max product of break (i - j) to two or more nums  

```
Pseudocode:
dp = [0 for _ in range(n + 1)]
dp[0] = 0
dp[1] = 0
dp[2] = 1
for i in range(3, n + 1):
    for j in range((i // 2) + 1):
        dp[i] = max(dp[i], (j * (i - j)), (j * dp[i - j]))
return dp[n]
```
**Note**  
Only need to consider j up to i // 2, bacause the bigger half is the same as the smaller half.  
Add dp[i] in the max method to preserve the previous max result.  

---

### 4. 96 Unique Binary Trees
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.  
Dp array dp[n] represents unique BSTs of n nodes.  
Suppose the root is 1 ... n, in each case, num of unique BSTs is num of unique left subtree * num of unique right subtree.  
In BST of nodes, 1 to n, num of nodes of left and right subtrees is determined when node value is determined.  

```
Pseudocode:
dp = [0 for _ in range(n + 1)]
dp[0] = 1
dp[1] = 1
for i in range(2, n + 1):
    for j in range(i):
        dp[i] += dp[j] * dp[i - 1 - j]
return dp[n]
```
