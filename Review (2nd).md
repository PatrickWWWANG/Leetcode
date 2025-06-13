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

## Binary Tree

### 144 Binary Tree Preorder Traversal
Root -> Root.left -> Root.right  

### 94 Binary Tree Inorder Traversal
Root.left -> Root -> Root.right  

### 145 Binary Tree Postorder Traversal
Root.left -> Root.right -> Root  

### 102 Binary Tree Level Order Traversal
Use a counter variable to store the number of variables in each level. Append level list to output list each time counter is decremented to 0.  

### 107 Binary Tree Level Order Traversal II
Use level order traversal to output a list from root to leaf, then reverse and return.  

### 199 Binary Tree Right Side View
Use level order traversal, append the last element of the current level to result each time counter == 0.  

### 637 Average of Levels in Binary Tree
Use level order traversal, append the average of the current level to result each time counter == 0.  

### 589 N-ary Tree Preorder Traversal
In traversal function, if the node has children, iterate the children and use recursion. Root -> Root.children.  

### 590 N-ary Tree Postorder Traversal
Root.children -> Root  

### 429 N-ary Tree Level Order Traversal
Instead of check node.left and node.right, simple extend node.children to que when node.children is not None.  

### 515 Find Largest Value in Each Tree Row
Use level order traversal, append the max value of the current level to result each time counter == 0.  

### 116 Populating Next Right Pointers in Each Node
Use level order traversal, set the next pointers of the elements of the current level each time counter == 0.  

### 117 Populating Next Right Pointers in Each Node II
Use level order traversal, set the next pointers of the elements of the current level each time counter == 0.  

### 104 Maximum Depth of Binary Tree
Use recursion. If node is None, return depth 0. Otherwise, return the max of left depth and right depth plus 1.  

### 111 Minimum Depth of Binary Tree
Use recursion. If node is None, return depth 0. If left depth == 0, return right depth + 1 because we need to reach the leaf (both left depth and right depth are 0). If right depth == 0, return left depth + 1. Otherwise, return the min of left depth and right depth plus 1.  

### 110 Balanced Binary Tree
Use recursion. GetHeight function: return 0 if not node, return 1 + max(left, right) else. Balance function: return True if not node, return False if left and right height differs more than 1, then return left balance and right balance. Can include balance check into the getHeight function.  

### 257 Binary Tree Paths
Use DFS, record the path each time reach a leaf node.  

### 404 Sum of Left Leaves
Use DFS, when iterate to the parent, check if the parent node has a left node and if the left node is a leaf node, collect the value if so. Note that local variable of an integer is not mutable in subroutine call. Use mutable variables such as list, nonlocal variable, or self.variable.  

### 222 Count Complete Tree Nodes
Use DFS. We have equation for number of nodes in a perfect binary tree. In a complete binary tree, itself may not be perfect, but it is constructed by perfect subtrees. Check if the tree from root is perfect, return number of nodes if perfect, return 1 + search(left) + search(right) if the root tree is not perfect.  

### 513 Find Bottom Left Tree Value
Use level order traversal, only record the first node value of each layer, return the last recorded value.  

### 112 Path Sum
Use DFS with the current function. Check if the target sum equals node value at leaf nodes. In other nodes, subtract node value from target sum and search children. Return true or false at leaf nodes.  

### 113 Path Sum II
Use DFS, similar to 112. Need a dfs subroutine for this problem. Subroutine signature includes node, target sum, path, and result. Record a deep copy of path into result when target sum == node.val at leaf node. Append node value to path and subtract target sum at non-leaf nodes.  

### 106 Construct Binary Tree from Inorder and Postorder Traversal
Use recursion. Inorder is L-ROOT-R, postorder is L-R-ROOT. The last element in postorder must be root. Find the root in inorder, we can get the length of left and right. Split inorder and postorder into left part and right part, throw them into next layer of recursion.  

### 105 Construct Binary Tree form Preorder and Inorder Traversal
Use recursion. Similar to 106, despite preorder is ROOT-L-R. So use first element of preorder as root.  

### 654 Maximum Binary Tree
Use recursion. Similar to 106. Only one array in this problem. Find the maximum as the root, then split nums to left and right.  

### 617 Merge Two Binary Trees
Use recursion. Deal with four conditions: not root1 + not root2, root1 + not root2, not root1 + root2, root1 + root2. When root1 + root2, generate a new root with val = root1.val + root2.val, then recursively process root.left and root.right.  

### 700 Search in a Binary Search Tree
Use recursion. If root value == val, return root; if root value < val and root has right, search right; if root value > val and root has left, search left. Otherwise return None.  

### 98 Validate Binary Search Tree
Use inorder traversal. When doing BST problems, remember inorder traversal of BST returns a sorted array. For this problem, inorder traversal the tree, and check if the result is sorted.  

### 530 Minimum Absolute Difference in BST
Use inorder traversal with two pointers. When doing inorder traversal on the BST, we are getting elements in sorted order. Use a pointer to record the previous node, then we can calculate the difference and maintain a global minimum difference.  

### 501 Find Mode in Binary Search Tree
Use inorder traversal. Use a pre pointer to record previous value and a counter to count the frequency of the value. Maintain mode list and mode count for comparison.  

### 236 Lowest Common Ancestor of a Binary Tree
Use postorder traversal. For problem like this, we want to traversal the tree from bottom level to upper level. Postorder traversal is designed for traversal like this. We return node if the node is p or q. If a node only receives return value from one side, this node is not LCA, we pass the value up. If a node receives value from both sides, this node is the LCA node, we return the node.  

### 235 Lowest Common Ancestor of a Binary Search Tree
BST has the property of left subtree < root and right subtree > root. We can simple compare the root value with p and q, and keep going left or right. The first value we encounter that has value between p and q is the LCA we are looking for.  

### 701 Insert into a Binary Search Tree
BST has the property of left subtree < root and right subtree > root. We compare val with cur.val, and go to the corresponding direction. If the direction is None, we found the correct position to insert val node.  

### 450 Delete Node in a BST
Use recursion. Case analysis: (1)If the node to be deleted is a leaf, return None to parent; (2) If the node to be deleted has only one child, return the child to parent; (3)If the node to be deleted has two children, append left subtree to the leftmost position of right subtree, then return right subtree to parent. Recursion: Conduct the case analysis logic when root value equals to key. Call function to root.left or root.right according to the relationship between root value and key. Return root at the end to pass the current node after deletion to upper level. We don't need to record the parent node in this recursion. Recursion stack automatically keeps track of parent node for all nodes. Key not in BST case is also covered. The position for key was None, and is still None after search.  

### 669 Trim a Binary Search Tree
Use recursion. If the node is smaller that range, return self function call to node.right. If the node is bigger that range, return self function call to node.left. If the node is in the range, self function call node.left and node.right respectively and attach them to node.left and node.right, and return node. If use iteration, need 2 layers of while loops to trim all nodes.  

### 108 Convert Sorted Array to Binary Search Tree
Use recursion. For a height-balanced binary search tree, the root value is the median of the nums array. Find the median, set it as the root node, than recursively self function call to nums[left] and nums[right] as root.left and root.right. Return root in the end.  

### 538 Convert BST to Greater Tree
Use reverse inorder traversal. Reverse inorder traversal R-ROOT-L of a BST gives a reverse sorted array. Keep a running_sum to record sum of all elements bigger than current element in traversal. Change node.val according to the running sum.  

## Backtracking

### 77 Combinations
Use backtracking. Backtracking template: if (end condition), collect result and return. For (candidates), add candidate, recursion, backtrack by removing candidate. In this problem, end condition is len(path) == target length. We need a start index as the input of the backtracking function. For each item in the for loop, we add it to path, recursion, and pop it. To prune, we stop when the rest range is not big enough to fulfill the remaining length of path (k - len(path)). Therefore, range of start index is for i in range(index, n - (k - len(path)) + 2).  

### 216 Combination Sum III
Use backtracking. Similar to 77. In this problem we need an extra target input for the backtracking function to keep track of the sum of path. We also need new end conditions, which are length of path > k and target < 0. The pruning is similar to 77.  

### 17 Letter Combinations of a Phone Number
Use backtracking. This problem needs two for loops in the backtracking function. The first loops the length of digits. The second loops the corresponding letters for a digit.  

### 39 Combination Sum
Use backtracking. In this problem, we can reuse the elements in candidates. We still control for i in range(index, len(candidates)), because when we get to 3, we have done everything with 2. We don't want [2, 3] and [3, 2], they are duplicate. However, in backtracking we input backtracking(i) instead of backtracking(i + 1) because we can reuse candidates. Prune by sorting candidates and break the for loop at the first position we encounter diff < 0.  

### 40 Combination Sum II
Use backtracking. This problem doesn't allow repeat use of one element so need backtracking(i + 1). Remove duplicate is important. The key to remove duplicate is, when we have candidates[i] == candidates[i - 1], we need to remove duplicate if we are in the same tree layer, but keep the path if we are in a branch. Two methods: (1) Use a new used array to track the elements we used in a path, when candidates[i] == candidates[i - 1], if used[i - 1] is True, we are in a branch, keep it; if used[i - 1] is False, we are moving to the next iteration in the same layer, we need to skip this. (2) Also check i > index with candidates[i] == candidates[i - 1], because when we have multiple elements with same value, process and keep the path using the first element ensures we have no duplicate. Prune similar to 40. Continue when we need to process next element (remove duplicate), break when prune.  

### 131 Palindrome Partitioning
Use backtracking. We still need the start index input. We iteratively check each i, s[start : i], is a palindrome or not. If yes, we add s[start : i] to partition and set start to i in next recursion. Set to i because s[start : i] is open on the right end. If we have start == len(s), we reached a partition for the whole s string to palindromes, we can collect the result.  

### 93 Restore IP Addresses
Use backtracking. End condition is number of partition is 4 and start index is at the end of s. There are 3 pruning conditions: (1) if partition > 255, break; (2) if partition starts with 0 and length is bigger than 1, break; (3) if already 4 parts and index still not at the end, break.  

### 78 Subsets
Use backtracking. For this problem, instead of collect result at the end condition, we want to collect ALL nodes in the backtracking tree. Therefore, the first line of backtracking function should be collect result, regardless of end condition. The end condition is start index at the end of nums array, but we don't need to write it explicitly because for loop ends and function exits automatically when index at the end of nums array since we control the range of i in for loop.

### 90 Subsets II
Use backtracking. Collect subsets in each backtraking function call regardless of end condition, similar to 78. Remove duplicate (tree layer) similar to 40, use used array or i > index check.  

### 491 Non-decreasing Subsequences
Use backtracking. This problem requires preservation of original sequence, so we can't sort nums, while still need to remove duplicate. End condition is collect result as long as len(path) >= 2. Add nums[i] to path when len(path) > 0 and nums[i] >= path[-1]. To remove duplicate: (1) Maintain a set for each level, record the numbers used in this tree level, and continue is nums[i] is already in the set; (2) Check and continue if nums[i] in nums[index : i], which implies nums[i] is processed in this level. Note that used array doesn't work for this problem since we can't sort, so elements with same value may not appear next to each other.  

### 46 Permutations
Use backtracking. For permutation problems, order matters. Same elements in different order are considered as different paths in this problem. Therefore, start index is not required in this problem since we process the whole nums array each time. We need to prevent the element already in path from being added into path again. To do this, we can: (1) Maintain a used array to track elements in path; (2) Check and continue when nums[i] in path.  

### 47 Permutations II
Use backtracking. The collection of results is similar to 46. Remove duplicate in tree level is similar to 40. In this problem, we don't have start index since it's a permutation problem, so we have to use the used array method to remove duplicate. The i > start index mathod doesn't work for this problem.  

### 332 Reconstruct Itinerary
Eulerian graph problem, introduction of Hierholzer algorithm. For this problem, first origin has out-degree - in-degree == 1, final destination has in-degree - out-degree == 1, all other nodes have out-degree == in-degree. First step is iterate the tickets and construct a dictionary of origin : [destinations]. Since we need the final output be the smallest one in lexical order, we need to sort the values of the dictionary. Then, we start from first origin and recursively visit every edge. We take out the edge when visiting. When we reach the final destination, which is either not in dictionary keys or has empty destination list. Then when we exit the recursion stack step by step, we construct the path in reverse order. If a node has multiple out degrees, the algorithm will again put them into recursion stack because we use while loop. While loop ensures all edges are used at the end of algortihm. To output the result, we reverse the path.  

### 51 N-Queens
Use 2-D backtracking. We want place one queen on each row, then go to next row. We also want to try every position. We use row index instead of start index in the backtracking function for this problem. Inside the backtracking function, we iterate each column position, then check if the board is valid if a queen is placed at the current position. If so, we put a queen, and send next row to a recursive call of backtracking function. For the check valid function, we don't need to check for row because the recursion ensures only one queen is placed at each row. We check for column and diagonal. Also, for diagonal, we only need to check [-1, -1] and [-1, 1] directions because rows under the current row do not have any queen.  

### 52 N-Queens II
Use 2-D backtracking. Same as 51. Instead of maintain an array for valid board, simply increment a valid count each time we have a valid result.  

### 37 Sudoku Solver
Use 2-D backtracking. This problem is different from N-queens, because it needs to fill in all blanks, not 1 quenn per row. To improve efficiency, use 3 lists of sets to store numbers used in each row, column, and subbox. Also, store all empty grids in an array. The backtracking function takes an index, which indicates the grid that we are processing in empty grids array. For nums from '1' to '9', we check with the lists of sets to see if there is a conflict. If there is no conflict, we add it to grid, update lists of sets, and recursively call backtracking function with index + 1, meaning the next empty grid in empty grids list. Then we write backtracking steps. With this method, we trade space efficiency for time efficiency, otherwise the problem go TLE error.  

### 282 Expression Add Operators
Use backtracking. This problem is special on having multiple cases at each seaching position, so we need multiple recursive calls of backtracking function in each step. We check if num[index] is '0', if so, i can only be == index, we break when i > index. Then, we deal with the special case of index == 0, because we can't have an operator before first number, so only one recursive call here. For other cases, we make 3 recursive calls for +, -, and *. Note that the input of backtracking function includes index, path, res, current, and last. This is because the calculation sequence, * first, then + and -. When operation is + or -, we simply add or minus new number from current and last is plus or minus new number. When operation is *, new current is current - last + last * new num, and new last is last * new num.  

## Greedy

### 455 Assign Cookies
Sort g and s. Greedily assign biggest available cookie to biggest child, use two pointers and increment pointers accordingly.  

### 376 Wiggle Subsequence
Use greedy. Record the previous slope, if the current slope is opposite to previous slope or there is no previous slope, update current slope and increment subsequence count. Note that we need to ignore plains, if nums[i] == nums[i - 1] we simply continue, otherwise it makes the algorithm complicated. This problem is also solvable by DP, but requires 2-D dp, one for index in nums, one for use the current value as maxima or minima. DP is less efficient for this problem.  

### 53 Maximum Subarray
Use greedy here. Iterate curSum through the nums array. For each step, curSum + nums[i], if result is smaller than 0, reset curSum to 0. Maintain a maxSum variable to record max value of curSum + nums[i] throughout the process. Can also use DP with 2 variables. In each step, DP[1] is max(DP[0] + nums[i], nums[i]). Record global maximum DP[1] throughout the process.  

### 122 Best Time to Buy and Sell Stock II
The greedy solution is: compare each day from day 1 with the previous. If the difference (profit) is positive, collect the profit and we can get the max profit at the end. DP solution will be discussed in DP section.  

### 55 Jump Game
The greedy solution is: iterate the nums array, calculate the jump range that can be covered by the steps. If the jump range can cover the last index, then return True. We don't need to bother how many steps are we jumping exactly from each point. This can be done within one iteration (O(n)).

### 45 Jump Game II
The greedy solution is still use range. For this problem, we need two ranges. Current range is the points that we can reach in current step. While iterating current range points, we maintain a next range variable, which is the maximum range we can reach if we take one more step. If the point we are iterating is larger than current range, we increment step counter and set next range to be new current range. If the next range reaches destination, we immediately return step + 1.

### 1005 Maximize Sum Of Array After K Negations
The greedy solution is: sort the array by absolute value and in reverse order. Iterate the array from start, negate value if k > 0 and value is negative. After iteration, if k still > 0, do nothing if k is even and negate the last value in the array if k is odd. Return the sum.  

### 134 Gas Station
The greedy solution is: initialize start point at 0, iterate the gas and cost, at each point, calculate the rest fuel = gas - cost. Increment rest fuel to both cursum and total sum. If cursum becomes < 0 at a point, the previous start point is not possible. We reset cursum to 0 and start to iteration index + 1. After finish iteration, if totsum < 0, the loop is not possible, we return -1. Otherwise, the loop must be possible, and since we eliminated all impossible regions, the current value of start must be valid.  

### 135 Candy
The greedy solution is: first iterate from left to right and check, then iterate from right to left and check. Key points: (1) Only depend on values that will not be changed in this iteration. So, from left to right, compare current element and current - 1 element; from right to left, compare current element and current + 1 element. (2) When doing second iteration, use a max operation make sure when changing candy value, we only change it when making the larger, keep it the same if the value we want change is smaller than the current value, otherwise we mess up the result of first iteration.  

### 860 Lemonade Change
Greedy solution: keep track of bills on hand, check all change possibilities, return False if we have number of bills negative.  

### 406 Queue Reconstruction by Height
Sort the queue with primary key person[0] from high to low, and secondary key person[1] from low to high. Then we use list.insert to create the output list. Insert each person the current output from tallest to shortest, to position person[1]. Since we start from tallest, insert person to position person[1] ensures that there are person[1] people taller or equal to current person in the output. Then, insert shorter person to any position will not change this number.  

### 452 Minimum Number of Arrows to Burst Balloons
Greedy overlap region problem. Sort the array according to x_end. Iterate the points, if x_start <= current arrow position, current arrow can burst the point, continue. Otherwise, we need one more arrow and position it to x_end to burst as many ballons as possible.  

### 435 Non-overlapping Intervals
Greedy overlap region problem. Similar to 452. Sort the array according to end position. Delete the current interval if it starts before current end, otherwise update current end.  

### 763 Partition Labels
(1) Write a find next part subroutine, use str.rfind() method to find the last occurance of characters in s. A part is found when self index equals rfind and equals to maintained end variable for current part. (2) Use a dictionary to store the last index of chracters in s. Simply iterate the enumeration of s, the dictionary automatically updates itself to the last index. Then iterate the enumeration again, update end using numbers from dictionary. A part is found when current index == last index of char and current index == end.  

### 56 Merge Intervals
Greedy overlap region problem. For this problem, we also need to consider the start point for output, so we can sort useing start as key. Then, we check each interval in intervals, if the start of current interval is smaller than previous end, we combine them by selecting the bigger end as the new end.  

### 738 Monotone Increasing Digits
Check from right to left. If the current number is smaller than previous number, change current position to the end to 9 and decrement previous number by 1. Make sure to change current position till end, otherwise it may not be the biggest monotone increasing number.  

### 968 Binary Tree Cameras
DFS the tree. The dfs returns the state of each node, which can either be have camera, covered, uncovered. At node, we return 0 because we treat None as covered to minimize number of cameras. If either side is uncovered, we return camera; if either side is camera, we return covered, otherwise we return uncovered. Note that if one side is None, we treat it as a covered side. Also, the sequence of state check can't be switched. Must check uncovered first, then check camera. Because if one side is uncovered and other side is camera, we still need to return camera. Use a nonlocal variable to record number of cameras used. Finally, if the root state is uncovered, we need to add an extra camera at root, then return.  

## Dynamic Programming

### 509 Fibonacci Number
DP array is [fib(n - 2), fib(n - 1)]. Transfer function is: temp = pre fib, pre fib = pre pre fib + temp, pre pre fib = temp. Iterate the transfer function for n - 1 times. Return DP[1].  

### 70 Climbing Stairs
Distinct ways to stair n equals to distinct ways to stair n - 1 plus distinct ways to stair n - 2. DP array is [stair(n - 2), stair(n - 1)]. Transfer function is: temp = stair(n - 1), stair(n - 1) = stair(n - 2) + temp, stair(n - 2) = temp. Iterate the transfer function for n - 1 times. Return DP[1].  

### 746 Min Cost Climbing Stairs
Min cost to stair n equals to min between min cost to stair n - 1 plus cost of stair n - 1 and min cost to stair n - 2 plus cost of stair n - 2. DP array is min cost to each stair. Transfer function is to find min cost using costs of previous two stairs and dp number of previous two stairs.  

### 62 Unique Paths
DP array is m x n, standing for unique paths to each grid. Transfer function is: unique paths to each grid is unique paths to left grid plus unique paths to above grid. Since we only need information from above row, we can use a 2 x n rolling DP array.  

### 63 Unique Paths II
Similar to 62. DP array is m x n, standing for unique paths to each grid. Transfer function is: unique paths to each grid is unique paths to left grid plus unique paths to above grid. To initialize first row and first column, set dp to 1 moving from start point to right and down. If encounter an obstacle, break the search and keep everything beyond 0 since they are not reachable. In dp iteration, if the grid is obstacle, keep it 0, otherwise do regular dp transfer calculation.  

### 343 Integer Break
DP is 1-D, standing for max product we can get by breaking i. Transfer function is: for each position dp[i], we iterate a second variable j, from 1 to i//2. At each j, we compare j * (i - j) and j * dp[i - j], where dp[i - j] is max product by breaking (i - j). We record the maximum value we can get when iterating j, and put it to dp[i].  

### 96 Unique Binary Search Trees
DP is 1-D, standing for unique BSTs for each node number. DP[0] and DP[1] are initialized to 1. Transfer function is: for each node number, we can choose each one of them to be the root of the BST, then, under this condition, the unique BST number is the product of unique left subBST number and unique right subBST number. We iterate different number of nodes in left subBST and right subBST, which are j and i - j - 1. Use DP numbers and calculate the product and add each product to DP[i]. Remember to use product, not sum, in calculation.  

### 416 Partition Equal Subset Sum
2-D DP. Size len(nums) * (target + 1). Return False when sum is odd, set target to sum // 2 otherwise. Each DP grid means given first i numbers, and maximum possible target value j, we can reach a maximum value of dp[i][j]. Transfer function is: take the maximum between, not take current number, dp[i - 1][j], and take current number, dp[i - 1][j - nums[i]] + nums[i]. Initialize first column 0, first row 0 when j < nums[0], and nums[0] otherwise. For each row iteration, copy previous row when j < nums[i], and calculate transfer otherwise. Since each iteration only depends on one previous row. We can compress DP to 2-D len(nums) * 2 rolling DP.  

### 1049 Last Stone Weight II
2-D DP. Similar to 416. Target is sum(stones) // 2. Use DP to find the cloest number we can choose to reach target, and that is the cancelled weight. Final output is sum(stones) - 2 * cancelled weight.  

### 494 Target Sum
Can use brute force dfs, will go time limit exceeded.  
Typical problem for: Number of different methods filling a knapsack to target. We have left + right = sum; left - right = target. Combining them gives right = (sum - target) / 2. First of all, if (sum - target) % 2 == 1, we return 0 because it's impossible to have solution.  
If use 2-D dp, be careful: need to count number of zeros up to each nums position and set dp[n][0] to 2^num_zero because there are 2^num_zeros ways to reach zero when there are num_zero zeros.  
Can use 1-D dp. In 1-D dp, make sure the iteration of target is from right to left because we need previous left numbers to calculate right entries. Make sure dp[nums[0]] += 1 in initialization to include nums[0] == 0 case.  
Key transfer funtion: **dp[j] += dp[j - nums[i]] for number of different methods knapsack problem**.  

### 474 Ones and Zeroes
3-D dp problem, can compress to 2-D dp, with dp[n][m] means max length of subset containing less than n ones and m zeros. Transfer function is take current iterating string or not take it. max(dp[n - num_ones][m - num_zeros] + 1, dp[n][m]). Remember, after compress, both m and n should be iterated in reverse order.  

### 518 Coin Change II
Complete knapsack problem, each item can be used infinite times. Count different methods similar to 494, using dp[j] += dp[j - nums[i]]. Because we reuse item multiple times, we iterate target from left to right. In this way, we calculate new value with one item large value with same item small value, hence reuse the item.  

### 377 Combination Sum IV
Permutation -> Consider order -> Iterate knapsack target first, then item -> Because this order considers each item in each different position.  
Combination -> Not consider order -> Iterate item first, then knapsack -> Later item always considered in later position.   
This is a permutation problem, so need to iterate knapsack target first, then item. DP transfer for counting different methods similar to 518 and 494.  

### 70 Climbing Stairs
Solved before using dp[n] = dp[n - 1] + dp[n - 2]. Can also consider this as a complete knapsack permutation problem. We have nums = [1, 2], and we find number of permutations to reach target, which is n. We iterate knapsack first, then item, for permutation. Similar to 377.  

### 322 Coin Change
This is a complete knapsack like problem, because we can reuse same coin, so we iterate knapsack from left to right. This problem asks for minimum number of coins, not related to order, so either iteration order is fine. Things to consider: 1. We need to find minimum number of coins, so we initialize dp to float('inf'); 2. dp[0] is 0 in this problem, because 0 coin is needed to reach 0; 3. Transfer function is min(dp[j], dp[j - coins[i]] + 1).  

### 279 Perfect Squares
This problem is the same as 322, despite we need to create the nums array ourselves using perfect square number with m ** 2 up to n.  

### 139 Word Break
DFS recursion goes time limit exceeded. 1-D dp is if s[0 : j] can be broken into words in wordDict. DP[0] is initialized to True. We can reuse words, and order matters, so we use complete knapsack and permutation iteration order. Knapsack first, then items, and from left to right. Note the transfer function is dp[i] **or** (i is end position for the item we are looking at **and** dp[i - len(item)]).  

### 198 House Robber
1-D DP. DP[i] means max rob value up to position i. Transfer function is max(dp[i - 1], dp[i - 2] + nums[i]), which is max(not rob current, rob current). Initialize DP[0] to nums[0], and DP[1] to max(nums[0], nums[1]) because at most one house can be robbed in two houses.  

### 213 House Robber II
Since we can't rob first and last house at the same time, we build two new arrays, one is everything except last one, another is everything except first one. We do two DPs for each of them, same as 198. Return the larger result.  

### 337 House Robber III
Binary Tree DP problem. For binary tree dp, we don't keep a complete dp array or matrix. We do dfs to the tree, and return dp values as the output of dfs function. For this problem, the return is an array [not take current, take current]. Boundry condition is return [0, 0] when root is None. Otherwise, not take current is max(left) + max(right), take current is node.val + left[0] + right[0]. When not taking, we can freely choose the max of left and right, not necessarily take child. When taking, we need to make sure children are not taken.  

### 121 Best Time to Buy and Sell Stock
DP matrix is 2 * len(prices) matrix. DP[i][0] is max cash of having a share at day i, DP[i][1] is not having a share at day i. Initialize DP[0][0] as -prices[0], simulating buy share at day 0. Transfer function for taking share is max(DP[i - 1][0], -prices[i]), which is max(take share from previous day, buy share today), -prices[i] because we can only buy share one time in total, so always cash 0 when buying. Transfer function for not taking share is max(DP[i - 1][1], DP[i - 1][0] + prices[i]), which is max(cash previous day, stock previous day and sell today). Return DP[len(prices) - 1][1] because always sell to make all cash to output.  

### 122 Best Time to Buy and Sell Stock II
For this problem, we can buy and sell multiple times, the only restriction is at most 1 stock on hand at a time point. Everything is the same as 121, except transfer function for taking share becomes max(DP[i - 1][0], DP[i - 1][1] - prices[i]). This is because we can use previus trading profit cash to buy share today, the cash on hand when buying is not necessarily 0 now.  

### 123 Best Time to Buy and Sell Stock III
Limit buy and sell at most 2 times. Use 4 * len(prices) DP matrix, which stands for [first stock, first cash, second stock, second cash]. Transfer function can be inferred similar to 122. Note that **stock for both first and second should be initilized to -prices[0] at the first day**. This is similar to buy-sell-buy at the first day. This initialization is important.  

### 188 Best Time to Buy and Sell Stock IV
Limit buy and sell at most k times. Modify 123 algorithm, use (2 * k) * len(prices) DP matrix. Initialize all buy positions at first day to prices[0]. Transfer functions can be constructed using a for loop except dp[i][0]. Use (-1)^n to control minus or plus prices[i].  

### 309 Best Time to Buy and Sell Stock with Cooldown
One cooldown day, meaning after sell, can't buy the next day, need to wait for one day. The key is, the transfer function of having stock now replies on cash of 2 days ago, now becomes max(dp[i - 1][0], dp[i - 2][1] - prices[i]). Two methods to initialize: (1) Initialize both day 1 and 2, day 2 initialization is **dp[1][0] = max(-prices[0], -prices[1])**, dp[1][1] = max(0, prices[1] - prices[0]); (2) Use 3 * len(prices) DP matrix, take an extra item to record cash of two days ago, only need to initialize day1 in this method.  

### 714 Best Time to Buy and Sell Stock with Transaction Fee
Same as 122, only different is to subtract fee when selling stock, include it into the transfer function of dp[i][1].  

### 674 Longest Continuous Increasing Subsequence
DP using one number. Initialize to 1. Iterate the array, if the item is larger than previous, increment dp variable, otherwise reset to 1. Reocrd the max number ever appeared in dp variable.  

### 300 Longest Increasing Subsequence
O(n^2) DP. In first iteration, at each position, do a second iteration up to this position. If nums[j] < nums[i], we can do transfer dp[i] = max(dp[i], dp[j] + 1). DP[i] means longest increasing subsequence **ends exactly** at position i. Initialize to 1 because each position has at least itself. Return max(dp) because longest increasing subsequence not necessarily ends at last position.  

### 718 Maximum Length of Repeated Subarray
2-D DP array. For each position of nums1, check each position of nums2, if number is the same, dp[i][j] = dp[i - 1][j - 1] + 1. We can use dp array of size (len(nums1) + 1) * (len(nums2) + 1), and iteration in range(1, len(numsx) + 1) and compare nums1[i - 1] amd nums2[j - 1], then we can skip initialization. Otherwise if do array size not plus 1, we need to initialize first row and first column in 2 for loops by setting equal positions to 1. Can compress to 1-D dp array, iterate j from right to left if compress.  

### 1143 Longest Common Subsequence
2-D DP array. DP matrix and initialization, iteration setup same as 718. DP array means longest common subsequence ends at position i, j. Since LCS doesn't reset when i-1 and j-1 are different, we can simply return dp[-1][-1]. If characters are the same, dp[i][j] = dp[i - 1][j - 1], otherwise, it's max(dp[i - 1][j], dp[i][j - 1]).  

### 1035 Uncrossed Lines
Same as 1143. Find longest common sequence ensures no cross.  

### 53 Maximum Subarray
For the dp version of this problem, dp[i] means maximum subarray that **ends exactly at** position i. Therefore, there are only two ways to get dp[i], which are previous sum plus nums[i] or nums[i] itself, and the transfer function is max(dp[i - 1] + nums[i], nums[i]). We need to return the max(dp) because maximum subarray doesn't necessarily ends that last position.  

### 392 Is Subsequence
This problem is easy to do with two pointers. For DP version of this problem, we are essentially finding if the length of longest common subsequence equals to the length of s. Then same as 1143.  

### 115 Distinct Subsequences
2-D DP array. Size (len(s) + 1) * (len(t) + 1). **Initialization is important.** For this problem, we need to initialize the whole first row to 1, representing there is one method to get an empty string from s, which is delete everything. Transfer function is: When s[i - 1] == t[j - 1], we still have every methods we had before, which is dp[i - 1][j], and we can use the new s[i - 1] position character and attach it to each method of t[j - 2], which is dp[i - 1][j - 1]. **So, dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j].** If s[i - 1] != t[j - 1], we keep dp[i - 1][j].  

### 583 Delete Operation for Two Strings
2-D DP array similar to 115. Initialization is delete every thing from one string if the other string is empty. If s[i - 1] == t[j - 1], no extra operation is required, so dp[i][j] = dp[i - 1][j - 1]. If s[i - 1] != t[j - 1], we need to delete at least one of these positions, so we take min(dp[i - 1][j] + 1, dp[i][j - 1] + 1). Delete both two positions needs two operstions, so it is included in previous two scenarios.  

### 72 Edit Distance
Almost the same as 583. Since we can replace now, if s[i - 1] != t[j - 1], delete any of them is 1 operation, change one to become the same as another is also 1 operation. So the transfer function when s[i - 1] != t[j - 1] is now min(dp[i - 1][j] + 1, dp[i][j - 1] + 1, dp[i - 1][j - 1] + 1), added replace calculation from 583.  

### 647 Palindromic Substrings
2-D DP array. DP matrix size len(s) * len(s). DP[i][j] is 0 or 1, meaning if s[i...j] (inclusive) is a palindrome. If s[i] != s[j], not palindrome. If s[i] == s[j], when i == j or i + 1 == j, automatically palindrome, otherwise, we look at dp[i + 1][j - 1]. Note that dp[i][j] relies on dp[i + 1][j - 1], so **iteration order i backward and j forward**.  

### 516 Longest Palindromic Subsequence
Similar to 647. This DP[i][j] means length of longest palindromic subsequence in s[i...j] (inclusive). If s[i] != s[j], dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]) because can't take both ends. If s[i] == s[j], record 1 or 2 when i == j or i + 1 == j, otherwise dp[i][j] = dp[i + 1][j - 1] + 2 because we can put in both start and end together. Iteration order same as 647.  

## Monotone Stack

### 739 Daily Temperatures
Use a monotonic temperature decreasing stack that stores index. When the incoming index refers to a temperature larger than top of stack, pop the top, use index difference to calculate days to wait, store answer in output array, and push new index to stack. Can finish in one iteration, O(1).  

### 496 Next Greater Element I
Use an array of size = len(nums2), and a monotonic decreasing stack, to store the next greater element for each element in nums2. Also, maintain a dictionary to map elements to indexes in nums2. Then, simply output the next greater element in nums2 for nums1 elements using the dictionary and the helper array.  

### 503 Next Greater Element II
Same as 739. Since we have circular integer array in this problem, we simply make nums = nums * 2, and in for loop only update result array when the pop index is in range of length of original nums array.  

### 42 Trapping Rain Water
Use a monotonic decreasing stack. Incoming larger item is edge for water. Height for pop position is min(right, left), right is incoming i, left is new top of stack. If stack is empty after the pop, the pop position can't hold any rain. Width is right - left - 1.  

### 84 Largest Rectangle in Histogram
Use a monotonic increasing stack. Incoming smaller item is edge for rectangle. Height is pop index, left and right is stack[-1] and i, if not stack, left is -1. Keep track of maximum area in the for and while loop. Need to append a 0 to heights at begining to make sure all histograms are considered. In 42, rain water can never be at first and last position, but in this problem first and last positions can also form rectangle.  

## Graph

