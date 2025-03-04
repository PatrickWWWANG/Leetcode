# Day56 Graph Part02

---

### 1. 200 Number of Islands
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.  
The main idea of this problem is to iterate the grid, increment the counter when we meet an unvisited land, search from the land to mark visited all connected land.  
We use a visited matrix to keep track of the iteration.  
We can use both BFS and DFS for the problem.  

```
Pseudocode DFS:
counter = 0
visited = [[0] * len(grid[0]) for _ in range(len(grid))]

def dfs(grid, row, col):
    for point in [[row - 1, col], [row + 1, col], [row, col - 1], [row, col + 1]]:
        if point[0] == -1 or point[0] == len(grid) or point[1] == -1 or point[1] == len(grid[0]):
            continue
        if grid[point[0]][point[1]] == '1' and visited[point[0]][point[1]] == 0:
            visited[point[0]][point[1]] = 1
            dfs(grid, point[0], point[1])

for row in range(len(grid)):
    for col in range(len(grid[0])):
        if grid[row][col] == '1' and visited[row][col] == 0:
            counter += 1
            visited[row][col] = 1
            dfs(grid, row, col)

return counter

Pseudocode BFS:
from collections import deque
counter = 0
visited = [[0] * len(grid[0]) for _ in range(len(grid))]

def bfs(grid, row, col):
    que = deque()
    que.append([row, col])

    while que:
        [r, c] = que.popleft()
        for point in [[r - 1, c], [r + 1, c], [r, c - 1], [r, c + 1]]:
            if point[0] == -1 or point[0] == len(grid) or point[1] == -1 or point[1] == len(grid[0]):
                continue
            if grid[point[0]][point[1]] == '1' and visited[point[0]][point[1]] == 0:
                visited[point[0]][point[1]] = 1
                que.append([point[0], point[1]])

for row in range(len(grid)):
    for col in range(len(grid[0])):
        if grid[row][col] == '1' and visited[row][col] == 0:
            counter += 1
            visited[row][col] = 1
            bfs(grid, row, col)

return counter
```
**Caution**  
In these matrix problems, always use **grid[row][col]** to prevent confusion.  

---

### 2. 695 Max Area of Island
You are given an m x n binary matrix grid. An island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) Return the maximum area of an island in grid. If there is no island, return 0.  
This problem is similar to previous problem. Instead of keeping a counter, we use a variable to keep track of the biggest area we found so far and update in each graph search.  
Again we can use both DFS and BFS.  

```
Pseudocode BFS:
from collections import deque
max_area = 0
visited = [[0] * len(grid[0]) for _ in range(len(grid))]

def bfs(grid, row, col):
    nonlocal max_area
    area = 1
    que = deque()
    que.append([row, col])
    while que:
        [r, c] = que.popleft()
        for point in [[r - 1, c], [r + 1, c], [r, c - 1], [r, c + 1]]:
            if point[0] == -1 or point[0] == len(grid) or point[1] == -1 or point[1] == len(grid[0]):
                continue
            if grid[point[0]][point[1]] == 1 and visited[point[0]][point[1]] == 0:
                area += 1
                visited[point[0]][point[1]] = 1
                que.append(point)
    max_area = area if area > max_area else max_area

for row in range(len(grid)):
    for col in range(len(grid[0])):
        if grid[row][col] == 1 and visited[row][col] == 0:
            visited[row][col] = 1
            bfs(grid, row, col)

return max_area
```
**Note**  
Don't forget to declare nonlocal max_area in bfs function.  
