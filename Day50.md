# Day50 Dynamic Programming Part 12

---

### 1. 115 Distinct Subsequences
Given two strings s and t, return the number of distinct subsequences of s which equals t.  
DP array means how many distinct subsequences of s[: i] equals t[: j].  
When s[i - 1] == t[j - 1], dp[i][j] includes 2 parts. If we use s[i - 1], then the number of distinct subsequences equals to dp[i - 1][j - 1], this is the number of t[: j - 1] in s[: i - 1]. The second part is we do not use s[i - 1], which is the number of distinct subsequences equals to t[: j] in s[: i - 1], which is dp[i - 1][j].  
If s[i - 1] != t[j - 1], we kind of ignore or delete s[i - 1], then dp[i][j] = dp[i - 1][j].  
We initialize dp[i][0] = 1 bacause there is always one distinct empty string in s.  

```
Pseudocode:
dp = [[0 for _ in range(len(t) + 1)] for _ in range(len(s) + 1)]

for m in range(len(s) + 1):
    dp[m][0] = 1

for i in range(1, len(s) + 1):
    for j in range(1, len(t) + 1):
        if s[i - 1] == t[j - 1]:
            dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j]
        else:
            dp[i][j] = dp[i - 1][j]

return dp[-1][-1]
```

---

### 2. 583 Delete Operation for Two Strings
Given two strings word1 and word2, return the minimum number of steps required to make word1 and word2 the same.  
DP array is the number of operations needed for two strings to be equal.  
If word1[i - 1] == word2[j - 1], dp[i][j] is equal to dp[i - 1][j - 1] because we don't need to operate on this position since they are equal.  
If word1[i - 1] != word2[j - 1], we need to delete one of the characters. We choose to keep the part that requires less operations to achieve.  
Initialize first row and column as we need to delete everything to get empty string.  

```
Pseudocode:
dp = [[0 for _ in range(len(word2) + 1)] for _ in range(len(word1) + 1)]

for m in range(1, len(word1) + 1):
    dp[m][0] = m
for n in range(1, len(word2) + 1):
    dp[0][n] = n

for i in range(1, len(word1) + 1):
    for j in range(1, len(word2) + 1):
        if word1[i - 1] == word2[j - 1]:
            dp[i][j] = dp[i - 1][j - 1]
        else:
            dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + 1

return dp[-1][-1]
```

---

### 3. 72 Edit Distance
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.  
Very similar to previous problem.  
Delete is operation from dp[i - 1][j], insert is operation from dp[i][j - 1], replace is operation from dp[i - 1][j - 1]. Cost of all three operations is 1.  

```
Pseudocode:
dp = [[0 for _ in range(len(word2) + 1)] for _ in range(len(word1) + 1)]

for m in range(1, len(word1) + 1):
    dp[m][0] = m
for n in range(1, len(word2) + 1):
    dp[0][n] = n

for i in range(len(word1) + 1):
    for j in range(len(word2) + 1):
        if word1[i - 1] == word2[j - 1]:
            dp[i][j] = dp[i - 1][j - 1]
        else:
            dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1

return dp[-1][-1]
```
