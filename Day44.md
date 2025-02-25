# Day44 Dynamic Programming Part 07

---

### 1. 198 House Robber
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night. Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.  
DP transition formula is the max of robbing this house and not robbing this house, which is i - 2 house + this house, and i - 1 house.  

```
Pseudocode:
if len(nums) == 1:
    return nums[0]

dp = [0 for _ in range(len(nums))]
dp[0] = nums[0]
dp[1] = max(nums[0], nums[1])

for i in range(2, len(nums)):
    dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

return dp[-1]
```
**Note**  
Remember to return directly when len(nums) is 1, otherwise nums[1] causes runtime error.  

---

### 2. 213 House Robber II
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses were broken into on the same night. Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.  
Same the previous problem, despite you can't rob both first and last house.  
Produce two subarray, one from first to second to last, another from second to last.  
Use dp method from previous problem to compute max for both subarray, and return the bigger one.  

```
Pseudocode:
if len(nums) == 1:
    return nums[0]
elif len(nums) == 2:
    return max(nums[0], nums[1])

dp = [0 for _ in range(len(nums) - 1)]
dp[0] = nums[0]
dp[1] = max(nums[0], nums[1])

for i in range(2, len(nums) - 1):
    dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

dp2 = [0 for _ in range(len(nums) - 1)]
dp2[0] = nums[1]
dp2[1] = max(nums[1], nums[2])

for j in range(2, len(nums) - 1):
    dp2[j] = max(dp2[j - 1], dp2[j - 2] + nums[j + 1])

return max(dp[-1], dp2[-1])
```

---

### 3. 337 House Robber III
After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night. Given the root of the binary tree, return the maximum amount of money the thief can rob without alerting the police.  
This is a dynamic program problem in binary tree.  
We need to use recursion with dynamic program for this problem.  
**In each layer of recursion, we define a dp array of length 2, which means [rob this node, no rob this node].**  
For the recursion, we use post-order traversal to pass data from leaf to root.  
If we rob this node, the value is node.val + left[1] + right[1] because we can't rob any child.  
If we do not rob this node, the value is **max(left) + max(right)** because we can choose whether to rob child. We want to max value.  
Finally we return the max value of the dp array at root.  

```
Pseudocode:
def traversal(node):
    if not node:
        return [0, 0]
    left = traversal(node.left)
    right = traversal(node.right)
    rob = node.val + left[1] + right[1]
    norob = max(left) + max(right)
    return [rob, norob]

return max(traversal(rob, norob))
```
