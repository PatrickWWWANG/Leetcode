# Day33 Greedy Part 02

---

### 1. 122 Best Time to Buy and Sell Stock II
Find and return the maximum profit you can achieve.  
Simply add up all positive differences to get maximum profit.  

```
Pseudocode:
profit = 0

for i in range(1, len(prices)):
    if (prices[i] - prices[i - 1]) > 0:
        profit += (prices[i] - prices[i - 1])

return profit
```

---

### 2. 55 Jump Game
You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position. Return true if you can reach the last index, or false otherwise.  
The only that we can't reach the last index is when we have a 0 that we can't jump pass.  
If we encounter a zero, check all previous elements to see if there is one that can allow us to jump pass the zero.  
Be careful of special cases: len(nums) == 1 is automatic true because we start at the last index.  

```
Pseudocode Checking 0:
if len(nums) == 1:
    return True

for i in range(len(nums) - 1):
    if nums[i] == 0:
        for j in range(i - 1, -2, -1):
            if j == -1:
                return False
            if nums[j] > i - j:
                break

return True

Pseudocode Checking Cover:
if len(nums) == 1:
    return True

cover = 0
i = 0

while i < cover:
    cover = max(cover, nums[i] + i)
    if cover >= len(nums) - 1:
        return True
    i += 1

return False
```
**Caution**  
Be careful of the sequence of the 2 if statements in checking zero method. They can't be flipped, otherwise there will be an extra check on nums[-1], which we don't want.  

---

### 3. 45 Jump Game II
Return the minimum number of jumps to reach the last index. The test cases are generated such that you can reach the last index.  
Keep one number to track the max cover of current step.  
Keep another number to track the max cover of next step.  
If we iterate to the max cover of current step, we take one more jump and the max cover of next step is now max cover of current step. Return number of step if we find the last index is within max cover.  

```
Pseudocode:
if len(nums) == 1:
    return 0

cur, next, step = 0, 0, 0
for i in range(len(nums) - 1):
    next = max(i + nums[i], next)
    if i == cur:
        step += 1
        cur = next
        if cur >= len(nums) - 1:
            return step
```

---

### 4. 1005 Maximize Sum of Array After K Negations
Negate largest negative items first.  
Then check if k % 2 is 1. If so, negate the smallest item.  

```
Pseudocode:
nums.sort()
i = 0
while k > 0 and i < len(nums) and nums[i] <= 0:
    nums[i] *= -1
    k -= 1
    i += 1

if k % 2 == 1:
    nums.sort()
    nums[0] *= -1

return sum(nums)

Pseudocode Using Abs Sort:
nums.sort(key=abs, reverse=True)
for i in range(len(nums)):
    while k > 0 and nums[i] < 0:
        nums[i] *= -1
        k -= 1

if k % 2 == 1:
    nums[-1] *= -1

return sum(nums)
```
**Note**  
Remember to add the i < len(nums) check in conditions for while loop to prevent index error.  
