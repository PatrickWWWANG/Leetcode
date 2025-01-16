# Day9 String Part 02

---

### 1. 151 Reverse Words in a String
Given an input string s, reverse the order of the words. Deal with the spaces.  
Eay to do with strip method. Try to do it without.  
Use two pointers to prevent a new string and save space.  

```
Pseudocode
s = list(s)
slow, fast = 0, 0
while fast < len(s):
    if s[fast] = ' ':
        if slow != 0:
            s[slow] = ' '
            slow += 1
        while fast < len(s) and s[fast] = ' ':
            fast += 1
    else:
        s[slow] = s[fast]
        slow += 1
        fast += 1

if s[slow - 1] == ' ':
    s = s[:slow - 1]
else:
    s = s[:slow]

s.reverse()
left, right = 0, 0
while right < len(s):
    if s[right] != ' ' and right < len(s) - 1:
        right += 1
    elif right == len(s) - 1:
        s[left : right + 1] = s[left : right + 1][::-1]
        right += 1
    else:
        s[left : right] = s[left : right][::-1]
        right += 1
        left = right

out = ''
for i in s:
    out += s
return out
```
**Note**  
1. Python string is immutable, so need to convert to list to work with.  
2. Remember to use "s[left : right] = s[left : right][::-1]" expression.  

---

### 2. Rotate String
s = 'abcdefg', k = 3 -> output = 'efgabcde'  
Use reverse to smartly solve it with no extra space.  
**Reverse the whole string, and reverse first k items and the rest items individually.**  

---

### 3. 28 Find the Index of the First Occurence in a String
Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.  
Use brute force is simple.  
Can improve using KMP algorithm.  

```
Pseudocode brute force:
for i in range(len(haystack) - len(needle) + 1):
    if haystack[i : i + len(needle)] == needle:
        return i
return -1
```

---

### 4. 456 Repeated Substring Pattern
Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.  
Method 1: Brute force by loop.  
Method 2: Brute force by construct from subtring with length factor of string length.  
Method 3: String concatenation.  
Method 4: KMP finding max equal prefix and suffix.  

```
Pseudocode Method 1:
if not s:
    return False
for i in range(len(s) // 2):
    pattern = [:i + 1]
    j = i + 1
    while s[j : j + len(pattern)] == pattern and j < len(s):
        j += len(pattern)
    if j == len(s):
        return True
return False

Pseudocode Method 2:
if not s:
    return False
for i in range(1, len(s)):
    if len(s) % i == 0:
        pattern = s[:i]
        count = len(s) // i
        ss = pattern * count
        if ss == s:
            return True
return False

Pseudocode Method 3:
if not s:
    return False
ss = s + s
ss = ss[1 : -1]
return ss.find(s) != -1
```