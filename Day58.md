# Day58 Graph Part04

---

### 1. 127 Word Ladder
Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.  
Use bfs for this shortest path problem.  
Find all words in the wordlist that are distance 1 away from current word, mark visted or used and push them into the que.  
Use a size variable to record distance travelled.  

```
Pseudocode:
if endWord not in wordList:
    return 0

from collections import deque
distance = 0
used = [0] * len(wordList)

que = deque()
que.append(beginWord)
while que:
    size = len(que)
    distance += 1
    while size > 0:
        word = que.popleft()
        size -= 1
        for i in range(len(wordList)):
            if used[i] == 0:
                same = 0
                for j in range(len(word)):
                    if word[j] == wordList[i][j]:
                        same += 1
                if same == len(word) - 1:
                    if wordList[i] == endWord:
                        distance += 1
                        return distance
                    else:
                        used[i] = 1
                        que.append(wordList[i])
return 0
```
**Note**  
Don't forget to return 0 when no path is found.  

---

### 2. kamacoder 105 Reachbility of Directed Graph
Given a DAG, return if all node are reachable from a given node.  
Can use both dfs and bfs for this problem. Simply mark visited all nodes reachable from the given node.  

```
Pseudocode DFS:
def dfs(graph, node, visited):
    for neighbor in graph[node]:
        if visited[neighbor] == 0:
            visited[neighbor] = 1
            dfs(graph, neighbor, visited)

Pseudocode BFS:
def bfs(graph, node):
    from collections import deque
    nonlocal visited
    que = deque()
    que.append(node)
    while que:
        n = que.popleft()
        for neighbor in graph[n]:
            if visited[neighbor] == 0:
                visited[neighbor] = 1
                que.append(neighbor)
```

---

### 3. 463 Island Perimeter
You are given row x col grid representing a map where grid[i][j] = 1 represents land and grid[i][j] = 0 represents water. Determine the perimeter of the island.  
There is only one island in this problem, so we only need to do one search.  
Do a regular bfs or dfs, despite we increment perimeter when we have neighbor is edge or water, and keep searching when neighbor is land.  

```
Pseudocode:
from collections import deque
perimeter = 0
visited = [[0] * len(grid[0]) for _ in grid]

def bfs(grid, row, col):
    nonlocal perimeter
    que = deque()
    que.append([row, col])
    visited[row][col] = 1
    while que:
        [r, c] = que.popleft()
        for point in [[r - 1, c], [r + 1, c], [r, c - 1], [r, c + 1]]:
            if point[0] == -1 or point[0] == len(grid) or point[1] == -1 or point[1] == len(grid[0]):
                perimeter += 1
                continue
            elif grid[point[0]][point[1]] == 0:
                perimeter += 1
                continue
            elif grid[point[0]][point[1]] == 1 and visited[point[0]][point[1]] == 0:
                visited[point[0]][point[1]] = 1
                que.append(point)

for row in range(len(grid)):
    for col in range(len(grid[0])):
        if grid[row][col] == 1:
            bfs(grid, row, col)
            return perimeter
```
**Note**  
Using break in last step only breaks the inner for loops. We either keep a flag variable to break both loops or return directly.  
