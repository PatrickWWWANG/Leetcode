# Day34 Greedy Part 03

---

### 1. 134 Gas Station
Given two integer arrays gas and cost, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique.  
Brute force will exceed time limit.  
Maintain two arrays, keep track of current sum and total sum of **difference between gas and cost**.  
If total sum < 0, then no solution, automatically return -1.  
When iterating, reset current sum to 0 and start index to i + 1 when we have current sum < 0. This is because if current sum of previous slice < 0, it is impossible to choose any index from previous slice as the starting point.  
After iteration finishes, and if there is solution, it must be the last start point recorded.  
No need to construct and simulate actual path in this method. Save time.  

```
Pseudocode:
cur_sum, tot_sum, start = 0, 0, 0

for i in range(len(gas)):
    diff = gas[i] - cost[i]
    cur_sum += diff
    tot_sum += diff
    if cur_sum < 0:
        cur_sum = 0
        start = i + 1

return -1 if tot_sum < 0 else start
```

### 2. 135 Candy
You are giving candies to these children subjected to the following requirements:  
Each child must have at least one candy.  
Children with a higher rating get more candies than their neighbors.  
Return the minimum number of candies you need to have to distribute the candies to the children.  
Do not try to use one iteration to deal with both sides.  
Use one iteration to check left to right, and another iteration to check right to left.  

```
Pseudocode:
candies = [1 for _ in range(len(ratings))]

for i in range(len(ratings) - 1):
    if ratings[i + 1] > rating[i]:
        candies[i + 1] = candies[i] + 1

for j in range(len(ratings) - 1, 0, -1):
    if ratings[j - 1] > ratings[j] and candies[j - 1] <= candies[j]:
        candies[j - 1] = candies[j] + 1

return sum(candies)
```
**Note**  
The second iteration has to be from right to left.  
The if statement in second iteration has also to check if candies[i - 1] is already > candies[i]. If so do not change, otherwise mess up first direction.  

---

### 3. 860 Lemonade Change
Given an integer array bills where bills[i] is the bill the ith customer pays, return true if you can provide every customer with the correct change, or false otherwise.  
List out all possible conditions.  

```
Pseudocode:
five, ten = 0, 0

for i in bills:
    if i == 5:
        five += 1
    elif i == 10:
        ten += 1
        five -= 1
        if five < 0:
            return False
    elif i == 20:
        if ten > 0:
            ten -= 1
            five -= 1
        else:
            five -= 3
        if five < 0:
            return False

return True 
```

---

### 4. 406 Queue Reconstruction by Height
Reconstruct and return the queue that is represented by the input array people. The returned queue should be formatted as an array queue, where queue[j] = [hj, kj] is the attributes of the jth person in the queue (queue[0] is the person at the front of the queue).  
Sort the array in height first, then rearrange the array for taller or equal height people at the front of the queue.  
This question asks for taller or equal height people at the front of the queue, so the sort for height must be from tall to short.  
When sorting height, must also sort equal height people by number of people at the front of the queue from small to large, otherwise mess up the queue when rearranging.  
Then iterate queue and rearrange based on number of people at the front of the queue.  

```
Pseudocode:
people.sort(key=lambda x: (-x[0], x[1]))

for i in range(len(people)):
    cur = people[i]
    pos = people[i][1]
    people[pos + 1 : i + 1] = people[pos : i]
    people[pos] = cur

return people

Pseudocode Using Insert:
people.sort(key=lambda x: (-x[0], x[1]))
out = []

for person in people:
    out.insert(person[1], person)

return out
```
**Note**  
Note the usage of the sort method.  
'Key' takes a function and pass each element to this function and use the return as the key of sorting.  
'Key' can take a tuple to use as primary key, secondary key etc.  
Note that we use (-x[0], x[1]) to indicate that we want to sort the primary key with reverse order and secondary key with normal order.  
Use 'insert' can be more time efficient.  
