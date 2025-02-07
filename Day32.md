# Day32 Greedy Part 01

---

### 1. 455 Assign Cookies
Use greedy, give biggest cookie to biggest child.  

```
Pseudocode:
g.sort()
s.sort()
p, q = len(g), len(s)
res = 0

while p and q:
    if s[q - 1] >= g[q - 1]:
        res += 1
        q -= 1
        p -= 1
    else:
        p -= 1

return res
```

---

### 2. 376 Wiggle Subsequence
Given an integer array nums, return the length of the longest wiggle subsequence of nums.  
Use greedy. Be careful that in [1, 2, 4, 3], when iterate to '4', although we can't add an extra element to wiggle subsequence because 2 > 1 and 4 > 2, we have to **substitute** the '2' in wiggele subsequence by '4'. Otherwise, we will have problem adding the '3' to wiggle subsequence. Note what we do when nums[i] > (or <) ptr and flag == 'pos' (or 'neg').  

```
Pseudocode:
res = 1
flag = 'init'
ptr = nums[0]

for i in range(1, len(nums)):
    if nums[i] == ptr:
        continue
    elif nums[i] > ptr and flag != 'pos':
        flag = 'pos'
        ptr = nums[i]
        res += 1
    elif nums[i] < ptr and flag != 'neg':
        flag = 'neg'
        ptr = nums[i]
        res += 1
    elif nums[i] > ptr and flag == 'pos':
        ptr = nums[i]
    elif nums[i] < ptr and flag == 'neg':
        ptr = nums[i]
    else:
        continue

return res
```

---

### 3. 53 Maximum Subarray
Given an integer array nums, find the subarray with the largest sum, and return its sum.  
Use greedy: reset sum to 0 when the sum of previous subarray is < 0.  
Use divide-n-conquer:

```
Pseudocode Greedy:
max, sum = nums[0], 0

for i in range(len(nums)):
    sum += nums[i]
    if sum > max:
        max = sum
    if sum < 0:
        sum = 0

return max

Pseudocode Divide-n-conquer:
def maxSubArray(self, nums):
    if len(nums) == 1:
        return nums[0]
    mid = len(nums) // 2
    maxL = self.maxSubArray(nums[: mid])
    maxR = self.maxSubArray(nums[mid :])
    max_Cross = self.maxC(nums, mid)
    return max(maxL, maxR, max_Cross)

def maxC(self, nums, mid):
    sumL, sumR = nums[mid - 1], nums[mid]
    maxL, maxR = nums[mid - 1], nums[mid]
    for i in range(mid - 2, -1, -1):
        sumL += nums[i]
        if sumL > maxL:
            maxL = sumL
    for j in range(mid + 1, len(nums)):
        sumR += nums[j]
        if sumR > maxR:
            maxR = sumR
    return maxL + maxR
```
**Caution**  
The two if statements in greedy method have to be in this order. Otherwise, max will be set to zero in a array of all negative elements, which is incorrect. If one wants to switch the order, can use (if sum < nums[i]: sum = nums[i]).  
Divide-n-conquer is more "advanced" according ro leetcode, but this problem, greedy is much more efficient.  
Greedy is O(n), and divide-n-conquer is O(nlogn).  
