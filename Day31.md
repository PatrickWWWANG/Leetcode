# Day30 Backtracking Part 04

---

### 1. 491 Non-decreasing Subsequences
Given an integer array nums, return all the different possible non-decreasing subsequences of the given array with at least two elements.  
Use backtraing. Check for membership when add to result is possible but very time consuming.  
Can use a set to reject duplicating path or doing tree-level duplicate check.  
In this problem, we need to keep the order of original nums array, so we can't use sort. The tree-level duplicate check can't be simply check nums[i] and nums[i - 1] in a sorted array. Therefore, we maintain a level set for this task.  

```
Pseudocode using Set as Result:
result, path = set(), []

def backtracking(nums, start):
    nonlocal result, path
    if len(path) > 1:
        result.add(tuple(path[:]))

    if start == len(nums):
        return
    
    for i in range(start, len(nums)):
        if len(path) > 0 and nums[i] < path[-1]:
            continue
        else:
            path.append(nums[i])
            backtracking(nums, i + 1)
            path.pop()
    return

backtracking(nums, 0)
return [list(item) for item in result]

Pseudocode using Set for Tree-level Check:
result, path = [], []

def backtracking(nums, start):
    nonlocal result, path
    if len(path) > 1:
        result.append(path[:])
    
    if start == len(nums):
        return
    
    level = set()
    for i in range(start, len(nums)):
        if (len(path) > 0 and nums[i] < path[-1]) or (nums[i] in level):
            continue
        else:
            path.append(nums[i])
            level.add(nums[i])
            backtracking(nums, i + 1)
            path.pop()
    return

backtracking(nums, 0)
return result
```
**Note**  
Set only accepts tuple, not list.  
Note the level set doesn't need to be backtracked because it is maintained throughout the tree-level.  

---

### 2. 46 Permutations
Given an array nums of distinct integers, return all the possible permutations.  
In permutation problems, sequence matters. We can choose back to the first element in the second element tree. Therefore, start index is not needed in permutation problem. 
Need to do a branch duplication check to prevent use the same element for multiple times.  
Use a 'used' array to check if the item has been used in the branch before. Or, since in this problem all elements are distinct and we only have len(nums) <= 30, we can directly check if the element is in path.  

```
Pseudocode:
result, path = [], []

def backtracking(nums):
    nonlocal result, path
    if len(path) == len(nums):
        result.append(path[:])
        return
    
    for i in range(len(nums)):
        if nums[i] in path:
            continue
        else:
            path.append(nums[i])
            backtracking(nums)
            path.pop()
    return

backtracking(nums)
return result
```

---

### 3. 47 Permutations II
Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.  
Need to remove duplicates for both tree-branch (not reuse same element in a path) and tree-level (not output same permutation twice).  
Keep a 'used' array for removing duplicates.  

```
Pseudocode:
nums.sort()
result, path = [], []

def backtracking(nums, used):
    nonlocal result, path
    if len(path) == len(nums):
        result.append(path[:])
    
    for i in range(len(nums)):
        if i > 0 and nums[i] == nums[i - 1] and used[i - 1] == 1:
            continue
        elif used[i] == 0:
            path.append(nums[i])
            used[i] = 1
            backtracking(nums, used)
            used[i] = 0
            path.pop()
    return

used = [0 for _ in range(len(nums))]
backtracking(nums, used)
return result
```
**Note**  
Note that the if statement removes duplicate in tree-level and the elif statement removes duplicate in tree-branch.  
