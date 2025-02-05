# Day29 Backtracking Part 02

---

### 1. 39 Combination Sum
Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target.  
Elements can be used multiple times.  

```
Pseudocode:
result, path = [], []

def backtracking(candidates, sum, start):
    nonlocal result, path
    if sum >= target:
        if sum == target:
            result.append(path[:])
        return
    
    n = len(candidates)
    for i in range(start, n):
        path.append(candidates[i])
        backtracking(candidates, sum + candidates[i], i)
        path.pop()
    return

backtracking(candidates, 0, 0)
return result
```
**Note**  
Note the parameter in the recursion step, start is passed in as i, not i + 1.  
Pruning: sort the candidates list, cut the remaining branches when the sum is already >= target.  

---

### 2. 40 Combination Sum II
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.  
The key for this problem is pruning of repeated path search.  
Suppose candidates are [1, 1, 1, 2, 2, 5], every possible path containing 1 has been searched and added when starting from the first 1. Therefore, search starting from 2nd and 3rd 1 can be skipped.  
Can add a check for item currently working on equals to previous item and start index != i.  
Can also use an extra used array.  

```
Pseudocode:
candidates.sort()
result, path = [], []

def backtracking(candidates, sum, start):
    if not candidates:
        return
    
    if sum > target:
        if sum == target:
            result.append(path[:])
        return
    
    for i in range(start, len(candidates)):
        if i > 0 and candidates[i] == candidates[i - 1] and i != start:
            continue
        path.append(candidates[i])
        backtracking(candidates, sum + candidates[i], i + 1)
        path.pop()
    return

backtracking(candidates, 0, 0)
return result

Pseudocode with Used Array:
candidates.sort()
result, path = [], []

def backtracking(candidates, sum, start, used):
    if not candidates:
        return
    
    if sum > target:
        if sum == target:
            result.append(path[:])
        return
    
    for i in range(start, len(candidates)):
        if i > 0 and candidates[i] == candidates[i - 1] and used[i - 1] == 0:
            continue
        path.append(candidates[i])
        used[i] = 1
        backtracking(candidates, sum + candidates[i], i + 1)
        used[i] = 0
        path.pop()
    return

used = [0 for _ in range(len(candidates))]
backtracking(candidates, 0, 0, used)
return result
```

---

### 3. 131 Palindrome Partitioning
Given a string s, partition s such that every substring of the partition is a palindrome.  
This problem iterates the position of cut, similar to iterating candidates in previous problems.  
Take a slice using s[start : position of cut].  

```
Pseudocode:
def isPalindrome(lst):
    return lst == lst[::-1]

result, path = [], []

def backtracking(s, start):
    nonlocal result, path
    if len(path) > 0 and not isPalindrome(path[-1]):
        return
    if start == len(s):
        result.append(path[:])
        return
    
    for i in range(start, len(s)):
        path.append(s[start : i + 1])
        backtracking(s, i + 1)
        path.pop()
    return

backtracking(s, 0)
return result
```
**Note**  
Note the 's[start : i + 1]'. In slicing problem we append a slice.  
Can also check for palindrome in the for loop and continue if the slice is not.  
