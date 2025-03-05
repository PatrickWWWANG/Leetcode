# Day57 Graph Part03

---

### 1. 1254 Number of Closed Islands
Given a 2D grid consists of 0s (land) and 1s (water).  An island is a maximal 4-directionally connected group of 0s and a closed island is an island totally (all left, top, right, bottom) surrounded by 1s. Return the number of closed islands.  
Method 1 is add a variable 'closed' in bfs or dfs and return it after search finish. In main function we only increment counter when the search returns closed == True.  
Method 2 is search edge first and convert all lands on the edge or connect to the edge to water. Then we search the modified grid again. This method requires two search functions, one for edge search and one for regular search.  

```
Pseudocode Method 1:
from collections import deque
counter = 0
visited = [[0] * len(grid[0]) for _ in grid]

def bfs(grid, row, col):
    closed = True
    que = deque()
    que.append([row, col])
    while que:
        [r, c] = que.popleft()
        for point in [[r - 1, c], [r + 1, c], [r, c - 1], [r, c + 1]]:
            if point[0] == -1 or point[0] == len(grid) or point[1] == -1 or point[1] == len(grid[0]):
                closed = False
                continue
            if grid[point[0]][point[1]] == 0 and visited[point[0]][point[1]] == 0:
                visited[point[0]][point[1]] = 1
                que.append(point)
    return closed

for row in range(len(grid)):
    for col in range(len(grid[0])):
        if grid[row][col] == 0 and visited[row][col] == 0:
            visited[row][col] = 1
            closed = bfs(grid, row, col)
            if closed:
                counter += 1

return counter
```
**Note**  
Note that in this problem, grid is 0 means land and grid is 1 means water.  

---

### 2. kamacoder 102 Sink Closed Island
Similar to method 2 of previous problem. We iterate all edges first and record all lands on the edge or connect to the edge. Then, we simply set all unrecorded points to water.  

---

### 3. 417 Pacific Atlantic Water Flow
The island is partitioned into a grid of square cells. You are given an m x n integer matrix heights where heights[r][c] represents the height above sea level of the cell at coordinate (r, c). The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is less than or equal to the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean. Return a 2D list of grid coordinates result where result[i] = [ri, ci] denotes that rain water can flow from cell (ri, ci) to both the Pacific and Atlantic oceans.  
Brute force method is to search all points and record the ones that can reach both oceans. This will cause timeout.  
We search from the edges, keep 2 visited matrix, one for each ocean. The visited matrixes record points that can be reached from each ocean.  
We iterate the grid and record points that can be visited from both oceans.  

```
Psudocode:
from collections import deque
reach_pacific = [[0] * len(heights[0]) for _ in heights]
reach_atlantic = [[0] * len(heights[0]) for _ in heights]

def bfs(heights, visited, row, col):
    visited[row][col] = 1
    que = deque()
    que.append([row, col])
    while que:
        [r, c] = que.popleft()
        for point in [[r - 1, c], [r + 1, c], [r, c - 1], [r, c + 1]]:
            if point[0] == -1 or point[0] == len(heights) or point[1] == -1 or point[1] == len(heights[0]):
                continue
            if heights[point[0]][point[1]] >= heights[r][c] and visited[point[0]][point[1]] == 0:
                # The reverse search expands to points with same or higher height.
                visited[point[0]][point[1]] = 1
                que.append(point)

for row in range(len(heights)):
    bfs(heights, reach_pacific, row, 0)
    bfs(heights, reach_atlantic, row, len(heights[0]) - 1)

for col in range(len(heights[0])):
    bfs(heights, reach_pacific, 0, col)
    bfs(heights, reach_atlantic, len(heights) - 1, col)

ans = []
for row in range(len(heights)):
    for col in range(len(heights[0])):
        if reach_atlantic[row][col] == 1 and reach_pacific[row][col] == 1:
            # Both visited matrix are 1 means can be reached from both oceans.
            ans.append([row, col])
return ans
```

---

### 4. 827 Making A Large Island
You are given an n x n binary matrix grid. You are allowed to change at most one 0 to be 1. Return the size of the largest island in grid after applying this operation.  
The brute force is find each 0 point, change to 1, and do a search to record max area. This method will go timeout.  
We use a new visited matrix. In this matrix, each island is marked by an island. For a land, visited[row][col] gives the id of the island this land belongs to. Besides that, we use a dictionary to map island id to island area we calculated in search.  
We iterate the grid, for each 0 point, we iterate all four connected points and use the visited matrix to find the islands that are connected to this point. We use a set to record the connected island ids to remove duplicate. Then we iterate the set and use the dictionary to calculate the new bigger island.  
Note that if the original grid is all 1 with no 0, we can't convert any sea. In this case, we return the number of 1s in this grid.  

```
Pseudocode:
from collections import deque
islands = {}
island_id = 2
visited = [[0] * len(grid[0]) for _ in grid]

def bfs(grid, row, col):
    nonlocal islands, island_id, visited
    area = 1
    visited[row][col] = island_id
    que = deque()
    que.append([row, col])
    while que:
        [r, c] = que.popleft()
        for point in [[r - 1, c], [r + 1, c], [r, c - 1], [r, c + 1]]:
            if point[0] == -1 or point[0] == len(grid) or point[1] == -1 or point[1] == len(grid[0]):
                continue
            if grid[point[0]][point[1]] == 1 and visited[point[0]][point[1]] == 0:
                area += 1
                visited[point[0]][point[1]] = island_id
                # We record the island id in island positions here
                que.append(point)
    islands[island_id] = area
    # We update the dictionary of island area here
    island_id += 1

for row in range(len(grid)):
    for col in range(len(grid[0])):
        if grid[row][col] == 1 and visited[row][col] == 0:
            bfs(grid, row, col)

max_area = 0
have_zero = False
# We use this flag to check if this grid is full of 1s with no 0
for row in range(len(grid)):
    for col in range(len(grid[0])):
        if grid[row][col] == 0:
            have_zero = True
            adj_islands = set()
            # We use set to remove duplicate
            for point in [[row - 1, col], [row + 1, col], [row, col - 1], [row, col + 1]]:
                if point[0] == -1 or point[0] == len(grid) or point[1] == -1 or point[1] == len(grid[0]):
                    continue
                if visited[point[0]][point[1]] > 0:
                    adj_islands.add(visited[point[0]][point[1]])
                    # Add the ids of all adjacent islands
            area = 1
            for id in adj_islands:
                area += islands[id]
                # Calculate area from the dictionary
            max_area = area if area > max_area else max_area

if have_zero:
    return max_area
else:
    return len(grid) * len(grid[0])
    # Return number of 1s is the grid of no 0
```
**Caution**  
Note that island id start from 2 because 0 and 1 are used to represent land and sea.  
