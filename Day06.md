# Day6 Hash Table Part 01

---

### Hash Table Problems  
**Use hash table to quickly find if an element is in a set or not.**  
index = hashFunction(name)  
hashFunction = hashCode(name) % tableSize  
Common data structures for hash table problems: Array, Set, Map  

---

### 1. 242 Valid Anagram
Given two strings s and t, return true if t is an anagram of s, and false otherwise.  
Hash table method: set a list of length 26, add 1 for each char in s and minus 1 for each char in t. Check if all elements are 0.

```
Pseudocode:
wordcnt = [0 for _ in range(26)]
for i in s:
    wordcnt[ord(i) - ord('a')] += 1
for j in t:
    wordcnt[ord(j) - ord('a')] -= 1
for k in wordcnt:
    if k != 0:
        return False
return True
```
**Note** Possible testcase: s longer, t longer, different characters

---

### 2. 349 Intersection of Two Arrays
Given two integer arrays nums1 and nums2, return an array of their intersection.  
Use set: if a number in nums1 appears in nums2, record it in set.  
Use array: max number 1000, make two lists and have list[num] += 1 each for nums1 and nums2. At a position, if list1[position] * list2[position] is not zero, it means this number appears in both num1 and nums2.

```
Pseudocode Set:
output = set([])
for i in nums1:
    if i in nums2:
        output.add(i)
return list(output)

Pseudocode Set operation:
return list(set(num1) & set(nums2))

Pseudocode Array:
list1 = [0 for _ in range(1000)]
list2 = [0 for _ in range(1000)]
for i in nums1:
    list1[i] += 1
for j in nums2:
    list2[j] += 1

output = []
for k in range(1001):
    if list1[k] * list2[k] != 0:
        output.append(k)
return output
```
**Note**  
For array method, can also make each entry binary, i.e. set list[number] = 1, and check "if list1[k] and list2[k]" for intersection.  

---

### 3. 202 Happy Number
A happy number is a number defined by the following process:  
Starting with any positive integer, replace the number by the sum of the squares of its digits.  
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.  
Those numbers for which this process ends in 1 are happy.  
Return true if n is a happy number, and false if not.  
**Thought**  
If a sum appears for the second time in the process, it will loop forever and the number is not a happy number.  
Use a set to record sums in process.  
Convert number to string, iterate the string and convert back to int to get all digits of a number.  

```
Pseudocode:
results = set([])
while True:
    add = 0
    for i in str(n):
        add += int(i) * int(i)
    
    if add == 1:
        return True
    elif add in results:
        return False
    else:
        n = add
        results.add(add)
```
**Note**  
Remember to set "n = add" in the else branch.

---

### 4. 1 Two Sums
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.  
Iterate over the array, find if (target - num) appeared before. Store num and index in a dictionary if not till find answer.  

```
Pseudocode
nummap = {}
for i in range(len(nums)):
    if (target - nums[i]) in nummap.keys():
        return [nummap[(target - nums[i])], i]
    else:
        nummap[nums[i]] = i
```
