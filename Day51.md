# Day51 Dynamic Programming Part 13

---

### 1. 647 Palindromic Substrings
Given a string s, return the number of palindromic substrings in it.  
DP array stores 0 and 1 only. DP[i][j] means if s[i] to s[j] is palindromic.  
When s[i] == s[j], if i == j or i + 1 == j, we set dp to 1. Otherwise, we set dp to dp[i + 1][j - 1].  
Since we need [i + 1] for [i], we iterate i from right to left.  

```
Pseudocode:
dp = [[0 for _ in range(len(s))] for _ in range(len(s))]

for i in range(len(s) - 1, -1, -1):
    for j in range(i, len(s)):
        if s[i] == s[j]:
            if i == j or i + 1 == j:
                dp[i][j] = 1
            else:
                dp[i][j] = dp[i + 1][j - 1]

return sum(sum(row) for row in dp)
```

---

### 2. 516 Longest Palindromic Subsequence
Given a string s, find the longest palindromic subsequence's length in s.  
DP[i][j] is the longest palindromic subsequence's length for the substring between s[i] and s[j].  
When s[i] == s[j], i == j is length 1, i + 1 == j is length 2. Otherwise, dp[i][j] is the middle part plus 2 (i and j).  
When s[i] != s[j], we can't include both s[i] and s[j], so we choose the bigger between them.  

```
Pseudocode:
dp = [[0 for _ in range(len(s))] for _ in range(len(s))]

for i in range(len(s) - 1, -1, -1):
    for j in range(i, len(s)):
        if s[i] == s[j]:
            if i == j:
                dp[i][j] = 1
            elif i + 1 == j:
                dp[i][j] = 2
            else:
                dp[i][j] = dp[i + 1][j - 1] + 2
        else:
            dp[i][j] = max(dp[i + 1][j], dp[i][j - 1])

return max(max(row) for row in dp)
```
**Note**  
For subsequence problem (can delete element), we need to deal with the s[i] != s[j] case.  
