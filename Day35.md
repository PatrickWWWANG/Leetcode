# Day35 Greedy Part 04

---

### 1. 452 Minimum Number of Arrows to Burst Ballons
Given the array points, return the minimum number of arrows that must be shot to burst all balloons.  
Interval scheduling problem. Use greedy.  
Sort the points array base on Xend value. This is because when we add one more arrow and update new right boundry, we want to make sure that this new right boundry is the smallest Xend among remaining points. Otherwise we can't make sure one arrow can burst all points with Xstart <= right boundry.  

```
Pseudocode:
points.sort(key=lambda x: x[1])
arrow = 0
cur_r = float('-inf')
for point in points:
    if point[0] > cur_r:
        arrow += 1
        cur_r = point[1]
return arrow
```

---

### 2. 435 Non-overlapping Intervals
Given an array of intervals intervals where intervals[i] = [starti, endi], return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.  
Interval scheduling problem. Use greedy.  
Sort the points array base on end value. Iterate the array to find intervals to keep, then return length - keep.  

```
Pseudocode:
if len(intervals) == 1:
    return 0

intervals.sort(key=lambda x: x[1])
keep = 0
cur_r = float('-inf')
for interval in intervals:
    if interval[0] >= cur_r:
        keep += 1
        cur_r = interval[1]

return len(intervals) - keep
```

---

### 3. 763 Partition Labels
You are given a string s. We want to partition the string into as many parts as possible so that each letter appears in at most one part. Return a list of integers representing the size of these parts.  
Store the rightmost positions of letters in a dictionary, so that don't need to invoke rfind() when we encounter duplicate letters.  
We find a eligible string slice when the iterating point equals to the right most point of any letter from previous string slice.  
Can do a "find last index of a letter" by hand, but time consuming. Python rfind() is efficient.  

```
Pseudocode:
def findpart(s):
    letter = {}
    right = 0
    for i in range(len(s)):
        if s[i] not in letter.keys():
            letter[s[i]] = s.rfind(s[i])
            if letter[s[i]] == len(s) - 1:
                return len(s)
            right = max(right, letter[s[i]])
        if i == right:
            return i + 1

res = []
while sum(res) < len(s):
    res.append(findpart(s[sum(res) :]))
return res
```
