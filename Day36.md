# Day36 Greedy Part 05

---

### 1. 56 Merge Intervals
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.  
Use greedy. Sort the array and use end index to check overlap.  

```
Pseudocode:
intervals.sort(key=lambda x: x[0])
start = intervals[0][0]
end = intervals[0][1]
out = []
for interval in intervals:
    if interval[0] > end:
        out.append([start, end])
        start = interval[0]
        end = interval[1]
    else:
        end = max(end, interval[1])
out.append([start, end])
return out
```
**Caution**  
Don't forget to append the last interval after the for loop.  

---

### 2. 738 Monotone Increasing Digits
An integer has monotone increasing digits if and only if each pair of adjacent digits x and y satisfy x <= y. Given an integer n, return the largest number that is less than or equal to n with monotone increasing digits.  
Brute force will exceed runtime limit.  
Use greedy. Iterate through all digits. If encounter a digit that is bigger than the next digit, move backward if there are digits with same number before. Decrement the digit by 1, and set all following digits to 9.  

```
Pseudocode:
s = str(n)
change = False

for i in range(len(s) - 1):
    if int(s[i]) > int(s[i + 1]):
        change = True
        break

if change:
    while i > 0 and s[i] == s[i - 1]:
        i -= 1
    s = s[: i] + str(int(s[i]) - 1) + '9' * (len(s) - i - 1)

return int(s)
```
**Note**  
Make sure to move backward if there are digits with same number before the break point. Otherwise, 1339 will become 1329, which is wrong.  
Make sure to check the i > 0 when moving backward, otherwise i will go negative and the check last digits, which will be wrong.  
String can't be assigned a value at a index, but can use string manipulation.  

---

### 3. 968 Binary Tree Cameras
You are given the root of a binary tree. We install cameras on the tree nodes where each camera at a node can monitor its parent, itself, and its immediate children. Return the minimum number of cameras needed to monitor all nodes of the tree.  
Define a state array: [0: No cover, 1: Camera, 2: Covered]  
Conditions:  
    1. Left 2, Right 2 -> Parent 0  
    2. Left or Right at least one 0 -> Parent 1  
    3. Left or Right at lease one 1 -> Parent 2  
    4. Root 0 after finish -> Root 1  
    5. Null node start state is 2  
Follow these conditions to write a post-order traversal of the tree.  

```
Pseudocode:
count = 0

def traversal(node):
    nonlocal count
    if not node:
        return '2'
    left = traversal(node.left)
    right = traversal(node.right)
    if left == '2' and right == '2':
        return '0'
    elif left == '0' or right == '0':
        count += 1
        return '1'
    elif left == '1' or right == '1':
        return '2'

root_v = traversal(root)
if root_v == '0':
    count += 1
return count
```
**Note**  
Condition 4 is checked after traversal finishes, so it's written after the nested function is called.  
