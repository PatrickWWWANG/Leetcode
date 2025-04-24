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

### 151 Reverse Words in a String
Use library function: split and reverse.  
Detail realization: reverse the whole string, use slow and fast pointers to detect words, deal with blanks and reverse each word. Be careful when getting snippet from a string, i.e. string[slow : fast][::-1]. This is because string[fast - 1 : slow - 1 : -1] doesn't work as expected when slow == 0.  

### Kamacoder 55 Rotating String
Reverse the whole string. Cut the string into 2 parts. The first part is the n elements, the second part is the rest len(s) - n elements. Then reverse each part individually. We essentially rotate the last n elements to the start of the string.  

### 28 Find the Index of the First Occurrence in a String
Easy method is iterate over the haystack string and compare each snippet with needle, return the first match.  
KMP Algorithm:  
Firstly, construct a prefix array for the needle string:  
1. Initialize next array as all zeros, j pointer = 0;  
2. Iterate i pointer from 1 to the end of needle string;  
3. **while** j > 0 and needle[i] != needle[j], set j = next[j - 1];  
4. **if** needle[i] == needle[j], increment j += 1;  
5. Set next[i] = j in each iteration step.  

Then, back to main function:  
1. Call function to get next array, and initialize i and j pointers to 0;  
2. Iterate i from 0 to the end of haystack string;  
3. In each step of iteration, **while** j > 0 and haystack[i] != needle[j], set j = next[j - 1];  
4. Then, check **if** haystack[i] == needle[j], first check if j is at the end of needle. If so, match found, return i - len(needle) + 1 as the start index of match. If not at the end of needle, increment j += 1;  
5. If no match found after the iteration, return -1.  

### 459 Repeated Substring Pattern
Method 1: Concat s + s, and find s in new ss[1:-1] (remove first and last element). If we can find s in ss[1:-1], s can be constructed by taking a substring of it and appending multiple copies of the substring together. Can use find function or KMP algorithm.  
Method 2: Use the next array in KMP algorithm. Find the longest common prefix and postfix of s. If it is bigger than 0 and the difference between length of s and longest common prefix and postfix of s can divide length of s, then return True. The part of s not included in longest common prefix and postfix is the substring being repeated.  

## Stack and Queue

### 232 Implement Queue using Stacks
Use 2 stacks (realized with deque()). Always push new elements to st1. When pop or peek, if st2 is not empty, simply return the top of st2, otherwise pop elements from st1 and push them to st2 until st1 is empty, then return the top of st2. Maintain a size variable to check empty easier.  

### 225 Implement Stack using Queues
Use 2 queues (realized with deque()). Always push new elements to que1. When pop, check if que1 has more than 1 elements, if so, popleft and push all element from que1 to que2 except the last one, then popleft and return the last element. If que1 is empty, then pop all elements form que2 to que1 except the last one, then popleft and return the last element. When peek, similar to pop, expect don't keep the last element, move all elements, and return the last element moved. Maintain a size variable to check empty easier.  

### 20 Valid Parentheses
Use a stack to solve. Each time encounter a left parentheses, push to stack. Otherwise, pop from the stack and check if the left parentheses is the counterpart of the right parentheses. If not, return False. Also, if the stack is empty when encountering a right parentheses or stack is not empty after iteration finishes, return False.  

### 1047 Remove All Adjacent Duplicates In String
Use a stack. If stack is not empty and the incoming element is the same as the top of the stack. Pop the top of stack and continue to next element. Otherwise, push the element to stack. Concat and output the remaining elements in the stack after the iteration.  

### 150 Evaluate Reverse Polish Notation
Maintain a stack. When encounter a number, push to stack. When encounter a symbol, pop two elements, do calculation, push back to stack.  

### 239 Sliding Window Maximum
Use a monotone decreasing (left to right) queue to solve the problem. Each time, the element at the exit of the queue is the maximum of the current window. For incoming element, pop element out from entrance if the incoming element is bigger than the last element in the queue. For out going element, if it equals to the element at the exit of the queue, pop the exit element. Maintain first k elements to the queue before iteration and append the exit element to the max list in each iteration.  

### 347 Top K Frequent Elements
Method 1 is brute force method: use a dictionary to store the frequency of each element. Use another dictionary to store a list of elements for each frequency. Make a list of the keys of the second dictionary, sort the list in reverse order, extend output list with each the elements of each frequency from the largest frequency. Return the the length of output list is k.  
Method 2 uses min-heap (priority queue). Min-heap automatically put the incoming element to the right place, and each time it pops out the smallest item in the heap. We iterate the frequency dictionary, add tuple (frequency, element) to the min-heap. If the length of heap is bigger than k, we pop out the smallest item. Use heapq library.  

