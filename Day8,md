# Day8 String Part 01

---

### 1. 344 Reverse String
Two pointers: left and right points move to the center and swap.  

```
Pseudocode:
left, right = 0, (len(s) - 1)
while left < right:
    temp = s[left]
    s[left] = s[right]
    s[right] = temp
    left += 1
    right -= 1
```

---

### 2. 541 Rverse String II
Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.  
Increment the pointer each time by 2k step.  

```
Paeudocode
if k == 0 or k == 1:
    return s

if len(s) <= k:
    return s[::-1]

s = list(s)
left, right = 0, k
while right < len(s):
    s[left : right] = s[left : right][::-1]
    left += 2 * k
    right += 2 * k
if left < len(s):
    s[left :] = s[left :][::-1]
out = ''
for i in s:
    out += i
return out
```
**Note**  
For a list l, l.reverse() change l but ruturn None.  l[a : b].reverse() reverses a new list and return None, which does not change l itself and cannot be assigned. l[a : b][::-1] can be assigned.  
str(['a', 'b']) returns '['a', 'b']'. Need a foor loop to recreate the string.  

---

### 3. Replace Number
Replace all occurrences of numbers in a string by 'number'.  
Easy to do in python, just iterate and replace.  
In C++, you need to control the size of a string. First count the occurrences of numbers, get the space, fill in from the back, replace when pointer encounters a number.  