# Day67 Conclusion

### Day 1-2 Array
### Day 3-4 Linked List
### Day 6-7 Hash Table
### Day 8-9 String
### Day 10-11 Stack and Queue
### Day 13-27 Binary Tree
### Day 28-31 Backtracking
### Day 32-36 Greedy
### Day 37-51 Dynamic Programming
### Day 52-53 Monotone Stack
### Day 55-66 Graph

# Review (2nd)

## Array

### 704 Binary Search
Use left and right pointers. Find the mid between left and right, check relationship betweem nums[mid] and target, modify left and right accordingly. Use a while loop to ensure left <= right.  

### 35 Search Insert Position
Easy method: iterate the list and find the first element larger than target.  
Binary search method: use binary search to find the first element larger than target.  

### 34 Find First and Last Position of Element in Sorted Array
Use binary research to find target, expand to left and right to find the span.  

### 27 Remove Element
Use two pointers. Right pointer move to the right and assign left = right with right is not target.  

### 977 Squares of a Sorted Array
1. Find the largest negative and smallest positive, use two pointers to compare absolute values and cover the array.  
2. Square everything, result must be large -> small -> large. Use two pointers from both ends to middle, and build the output from large to small.  

### 209 Minimum Size Subarray Sum
Sliding window: iterate the array, add new entries to sum when the sum is smaller than target. Update result using window size and subtract entries from the left side when the sum is larger than target.  

### 59 Spiral Matrix II
There is no special algorithm for this problem, do brutal force. Fill each edge (edge - 1) numbers each time. Be careful of the boundary conditions.  

### 303 Range Sum Query - Immutable
Use a dictionary to store the sum from firs element up until each position, then work with the dictionary to find the range sums.  

## Linked List

