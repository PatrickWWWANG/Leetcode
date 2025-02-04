# Day28 Backtracking Part 01

---

### Backtracking Algorithm
Backtracking algorithm is a type of brute force search.  
Template: if (termination condition) then collect result and return  
    for (elements in set), process node, recursion, backtrack. Then return  

---

### 1. 77 Combinations
Given two integers n and k, return all possible combinations of k numbers chosen from the range [1, n].  
Use backtracking:  
    1. Determine recursion function parameter and return  
    2. Determine termination condition  
    3. Single layer recursion logic  
Can improve time efficiency using pruning.  

```
Pseudocode:
result, path = [], []

def backtracking(n, k, start):
    nonlocal result, path
    if len(path) == k:
        result.append(path[:])
        return
    for i in range(start, n + 1):
        path.append(i)
        backtracking(n, k, i + 1)
        path.pop()
    return

backtracking(n, k, 1)
return result

Pseudocode with Pruning:
result, path = [], []

def backtracking(n, k, start):
    nonlocal result, path
    if len(path) == k:
        reault.append(path[:])
        return
    for i in range(start, n - k + len(path) + 2):
        path.append(i)
        backtracking(n, k, i + 1)
        path.pop()
    return

backtracking(n, k, 1)
return result
```
**Caution**  
Remember to append(path[:]), otherwise path is being appended as a reference and will only get [] in the end.  
Note the range expression in for loop in the pruning version.  

---

### 2. 216 Combination Sum III
Find all valid combinations of k numbers that sum up to n such that the following conditions are true: only numbers 1 through 9 are used; each number is used at most once.  
Use backtracking.  

```
Pseudocode:
result, comb = [], []

def backtracking(k, sum, start):
    nonlocal result, comb
    if sum > n:
        return

    if len(comb) == k:
        if sum == n:
            result.append(comb[:])
        return
    
    for i in range(start, 11 - k + len(comb)):
        comb.append(i)
        backtracking(k, sum + i, i + 1)
        comb.pop()
    return

backtracking(k, 0, 1)
return result
```
**Note**
Note the range expression in for loop which includes pruning.  
Also the "if sum > n" statement for pruning.  

---

### 3. 17 Letter Combinations of a Phone Number
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.  
Use backtracking. Remember that the for loop in backtracking loops through all possible candidates at a certain position.  
In previous problems, we were finding combinations from a same group. Therefore, we need a start index to keep track of elements we have used. In this problem, each position of the combination maps to a different candidate group, so we use the index to keep track of the position we are working on and to retrieve the candidate group.  
Tree diagram might be helpful in analyzing backtracking problems.  

```
Pseudocode:
num_letter_dict = {
    '2' : ['a', 'b', 'c'],
    '3' : ['d', 'e', 'f'],
    '4' : ['g', 'h', 'i'],
    '5' : ['j', 'k', 'l'],
    '6' : ['m', 'n', 'o'],
    '7' : ['p', 'q', 'r', 's'],
    '8' : ['t', 'u', 'v'],
    '9' : ['w', 'x', 'y', 'z'],
}

result = []

def backtracking(digits, cur, comb):
    nonlocal result
    if not digits:
        return
    
    if cur == len(digits):
        result.append(comb)
        return

    l_list = num_letter_dict[digits[cur]]
    for i in l_list:
        backtracking(digits, cur + 1, comb + i)
    return

backtracking(digits, 0, '')
return result
```
