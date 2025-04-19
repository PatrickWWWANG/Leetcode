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

### 203 Remove Linked List Elements
Since we may need to change head, we use a dummy head to make the algorithm simpler. Use a cur pointer, each time check the value of cur.next, redirect the next pointer if cur.next is target.  

### 707 Design Linked List
Initialize the linked list with head is None and size is 0. Be careful with the next pointers operation sequence, and be care of the edge case of empty linked list.  

### 206 Reverse Linked List
Use a temp pointer to store the next node before reversing arrow. Use pre and cur pointers to control the working ndoes. Be careful with the operation sequence.  

### 24 Swap Nodes in Pairs
Use a dummy head to help processing the head node. Use first, second, temp pointers to control the working ndoes. Be careful with the operation sequence.  

### 19 Remove Nth Node From End of List
Use a dummy head to help processing the head node. Use pre, cur pointers to control the working ndoes. Move the cur by n step, and move pre and cur together till cur is at tail. Then delete pre.next by set pre.next to pre.next.next. Be careful with the operation sequence and pointer position.  

### 160 Intersection of Two Linked Lists
Get the length of the two linked lists. Move the pointer on the longer linked list forward such the remaining length is the same as the shorter linked list. Then move pointers on both linked lists togerther, stop when two pointers are equal.  

### 142 Linked List Cycle II
Check cycle: slow pointer and fast pointer, if they meet in iteartion, there is cycle.  
Find start of cycle: linked list = l (head to start of cycle) + l1 (start of cycle to slow and fast meet) + l2 (slow and fast meet to start of cycle). l = k * (l1 + l2) + l2. Move two pointers together from head and meet point, they will meet at the start of cycle.  

## Hash Table

### 242 Valid Anagram
Use a dict to store number of appearences of characters in s and subtract each appearence in t. Can use python ord() function to check the unicode int of the character. Can use a list rather than a dictionary as the hash map in this problem.  

### 349 Intersection of Two Arrays
Use set() method to remove duplicates and check if each item in set1 is also in set2. In python, can use list(set1 & set2) to find the intersection and output as a list.  

### 202 Happy Number
A number is not a happy number when the sum digit square appears twice in the loop. Store all sum digit square in a set. Return True when sum digit square is 1 and return False when sum digit square is already in the set.  

### 1 Two Sum
Use a dictionary to store (target - nums) : index when iterating the list. If a number is in the keys of the dictionary, we find the two numbers that sum to the target and can return the indexes.  

### 454 4Sum II
Iterate four lists together is O(n^4). Iterate first two, store the sum and count in a dictionary. Then iterate the remaining two lists, check if the target is in dictionary and increment the counter. Reduce time efficiency to O(n^2).  

### 383 Ransom Note
Almost the same as problem 242. Note that in this problem we add characters in magazine and subtract characters in ransom note. We may have unused letters from magazine and that is acceptable. Return False only when we have negative values.  

### 15 3Sum
Hash map and brute force are not appropriate for this problem because they are too time inefficient and hard to prune. Two pointer method works better for this problem.  
Sort the list first. Make a cur pointer iterating through the list, set left and right pointers to cur + 1 and the last element. The target is 0 minus the cur element. If left + right is too big, move right pointer back one position. If too small, move left pointer forward one position. If meets target, record cur, left, right in output.  
To remove duplicate, check each cur, if cur == cur - 1, continue to iterate the next element. Moreover, each time after we record a output, move left and right together, skip if the next left or right has the same value.  
To further prune, return immediately when cur is larger than target (zero).  

### 18 4Sum
This problem is similar to 15 and we use two pointers method to solve. For this problem we use two layers of for loop to iterate two cur positions and then use left and right pointers. Sort the list before iteration is key to the solution.  

## String

### 344 Reverse String
Use two pointers, swap elements from edge to middle. In reality, call list.reverse() directly.  

### 541 Reverse String II
Use a cur pointer to and process k elements after cur each time. Check with the length of the list and handle edge cases.  

### Kamacoder 54 Substitute Number
The trick is find the number of numbers in string, calculate the final length after subsititution, and use two pointers to fill the new string (in a list) from end to start.  

