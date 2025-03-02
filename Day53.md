# Day53 Monotone Stack Part 02

---

### 1. 42 Trapping Rain Water
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.  
The key idea is that **when we iterate from left to right with a monotone increase stack, the larger element to the right is the element waiting to be pushed, and the larger element to the left is the next item in the stack**.  
The edge index method recursively finds the smaller height between left and right until we reach the top of the rain, and add the amount of rain at the current column.  
The rain height and width method use the property of monotone increase stack, add up the amount of rain row by row. We find the height of both boundries, take the minimum, and times the distance between boundries.  

```
Pseudocode Using Edge Index (Calculate by Column):
st = []
edgeidx = [-1 for _ in range(len(height))]

for i in range(len(height)):
    while st and height[i] > height[st[-1]]:
        idx = st.pop()
        right_idx = i
        left_idx = st[-1] if st else -1

        if left_idx != -1 and right_idx != -1:
            if height[left_idx] <= height[right_idx]:
                edgeidx[idx] = left_idx
            else:
                edgeidx[idx] = right_idx

    st.append(i)

rain = 0
for m in range(len(height)):
    if edgeidx[m] != -1:
        cur_edge = edgeidx[m]
        while edgeidx[cur_edge] != -1:
            cur_edge = edgeidx[cur_edge]
        edge_height = height[cur_edge]
        rain += (edge_height - height[m])

return rain

Pseudocode Using Rain Height and Width (Calculate by Row):
st = []
rain = 0

for i in range(len(height)):
    if st and height[i] == height[st[-1]]:
        st.pop()
    else:
        while height[i] > height[st[-1]]:
            idx = st.pop()
            if st:
                rain_height = min(height[i], height[st[-1]]) - height[idx]
                rain_width = i - st[-] - 1
                rain += rain_height * rain_width
    st.append(i)

return rain
```
**Caution**  
Since we need to take st[-1] after pop to find the left larger item, we have to add a judgement of st not empty in the while loop to prevent indexerror when st is empty after pop.  

### 2. 84 Largest Rectangle in Histogram
Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.  
This problem is similar to the reverse of previous problem.  
We find the smaller item to the left and right of the current item, and the distance between the two smaller columns is the span available for the current column. We use a monotone decrease stack.  
We use a variable to record the max area.  
In previous problem, the boundry columns can't take rain water, so we just ignore them. In this problem, boundry columns can also be a part of a column. Therefore, we insert 0 to the start and end of the heights as dummy ends to calculate.  

```
Pseudocode:
st = []
max_area = 0
heights = [0] + heights + [0]

for i in range(len(heights)):
    while st and heights[i] < heights[st[-1]]:
        idx = st.pop()
        width = i - st[-1] - 1
        area = heights[idx] * width
        max_area = area if area > max_area else max_area
    st.append(i)

return max_area
```
