# Day30 Backtracking Part 03

---

### 1. 93 Restore IP Address
Given a string s containing only digits, return all possible valid IP addresses that can be formed by inserting dots into s.  
Use backtracking, similar to previous problem.  

```
Pseudocode:
def isValid(ip):
    if int(ip) > 255:
        return False
    if len(ip) > 1 and ip[0] == '0':
        return False
    return True

def recreateIP(ips):
    out = ''
    for ip in ips:
        out += ip
        out += '.'
    return out[: -1]

result, path = [], []

def backtracking(s, start):
    nonlocal result, path
    if start == len(s) and len(path) == 4:
        result.append(recreateIP(path[:]))
    
    for i in range(start, len(s)):
        if isValid(s[start : i + 1]) and len(path) < 4:
            path.append(s[start : i + 1])
            backtracking(s, i + 1)
            path.pop()
        else:
            break
    return

backtracking(s, 0)
return result
```
**Note**  
Remember the limitation of the length of output IP address, which has to be 4.  
Remember to include the case that IP can contain 0.  
**In this problem, use 'break' instead of 'continue' because once we have an invalid substring, it is impossible for us to move the slicing further right to get a valid substring. Therefore we can simply break. In previous palindrome problem, we can have invlid 'ab' and move slice further right to get valid 'aba', so we have to use 'continue'.**   

---

### 2. 78 Subsets
Given an integer array nums of unique elements, return all possible subsets (the power set).  
Use backtracking. In this problem, we collect result in each node, not just leaf node.  

```
Pseudocode:
result, path = [], []

def backtracking(nums, start):
    nonlocal result, path
    result.append(path[:])
    if start == len(nums):
        return
    
    for i in range(start, len(nums)):
        path.append(nums[i])
        backtracking(nums, i + 1)
        path.pop()
    return

backtracking(nums, 0)
return result
```
**Note**  
Note that in this problem we collect result in each node.  

---

### 3. 90 Subsets II
Given an integer array nums that may contain duplicates, return all possible subsets (the power set).  
Use backtracking, recall the mathod dealing with repeat items in 40 Combination Sum II.  

```
Pseudocode:
nums.sort()
result, path = [], []

def backtracking(nums, start):
    nonlocal result, path
    result.append(path[:])
    if start == len(nums):
        return

    for i in range(start, len(nums)):
        if i > start and nums[i] == nums[i - 1]:
            continue
        else:
            path.append(nums[i])
            backtracking(nums, i + 1)
            path.pop()
    return

backtracking(nums, 0)
return result
```
