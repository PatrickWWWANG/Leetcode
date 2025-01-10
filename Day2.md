# Day2 Array Part 02

---

### 1. 209 Minimum Size Subarray Sum  
Return minimum size of subarray of nums that sums >= target. Return 0 if no such array.  
Two pointers (Sliding window):  
    One pointer representing end of subarray slide to the right. If the sum of subarry >= target, record minimum window size and slide another pointer representing the start of subarray to the right.  

```
Psuedocode:
i = 0
sum = 0
result = len(nums) + 1
for j in range(len(nums)):
    sum += nums[j]
    while sum >= target:
        sublen = j - i + 1
        result = min(result, sublen)
        sum -= nums[1]
        i += 1

if result > len(nums):
    return 0
else:
    return result
```

---

### 2. 59 Spiral Matrix II  
Generate n x n matrix filled with elements from 1 to n x n in spiral order.  
**Boundary conditions** are the most significant for this problem.  
Loop invariant: Keep the same rule when processing each edge. (Leave the last node to the next edge each time)  

```
Psuedocode
Create n * n matrix
process length = n - 1
level = 0
num = 0

while process length >= 0:
    if process length != 0:
        process four edges using four loops
        a. output[level][i + level]
        b. output[i + level][n - 1 - level]
        c. output[n - 1 - level][n - 1 - level - i]
        d. output[n - 1 - level - i][level]
        each time fill in num, then num += 1
    
    else:
        output[level][level] = num

    process length -= 2
    level += 1

return output
```

Be careful with the loop invariant and the indexs when processing each edge.  

---

### 3. 303 Range Sum Query - Immutable
Calculate sum of elements of nums between indices left and right inclusive.  
Brute force may cause timeout if multiple queries are requested.  
**Partial sum (Prefix)**: Calculate and store prefix sum. Range sum is the different between two prefix sums.  

```
Pseudocode
Creat a prefix sum list with the same size as nums
Store sum from element 0 to element index in each position of the prefix sum list
if left == 0:
    return prefix_sum[right]
else:
    return prefix_sum[right] - prefix_sum[left - 1]
```

### 4. 开发商购买土地
Given a matrix, find a split of two parts that minimizes the sum difference between two parts.  
Setup a prefix sum matrix, store sum of upper left elements as prefix sum.  
Loop over all possible splits, use prefix sum matrix to calculate split sum difference and store the minimum. 