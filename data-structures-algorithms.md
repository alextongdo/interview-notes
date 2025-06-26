# Data Structures & Algorithms

## Quickstart
IF input array is sorted
- [Binary Search]()
- [Two Pointers]()

IF asked for all permutations/subsets of some condition
- [Backtracking]()

IF given a tree
- [DFS]()
- [BFS]()

IF given a linked list
- [Two Pointers]()
- [Linked List In-place Reversal]()

If recursion is banned
- [Stack]()

IF must solve in-place
- Swap corresponding values
- Store one or more different values in the same pointer
- [Linked List In-place Reversal]()

IF asked for maximum/minimum subarray/subset/options
- [Dynamic Programming]()
- [Sliding Window]()

IF asked for top/least k items
- [Heap]()
- [Top K Elements]()

IF asked for common strings
- Hashmap
- [Trie]()

ELSE
- Hashmap/Set for `O(1)` time `O(n)` space
- Sort input for `O(nlogn)` time and `O(1)` space

[Patterns](https://www.youtube.com/watch?v=DjYZk8nrXVY)

## Runtime Trick
Given the constraint for the length of the input $n$, we can make an educated guess about the necessary runtime complexity.
| Length of Input  | Runtime |
| ------------- | ------------- |
| $0\leq n\leq11$  | $O(n!),~O(n^6)$  |
| $12\leq n\leq18$ | $O(2^n\times n^2)$  |
| $19\leq n\leq22$ | $O(2^n\times n)$ |
| $23\leq n\leq100$ | $O(n^4)$ |
| $150\leq n\leq400$ | $O(n^3)$ |
| $500\leq n\leq2000$ | $O(n^2\times \log N)$ |
| $2500\leq n\leq10000$ | $O(n^2)$ |
| $15000\leq n\leq1 \text{M}$ | $O(n\times \log N)$ |
| $1.5\text{M}\leq n\leq100 \text{M}$ | $O(n),~O(\log n),~O(1)$ |

## Binary Search
```python
def binary_search(array, target):
    left = 0 # pointer
    right = length(array) - 1 # pointer

    while left <= right:
        mid = (left + right) / 2
        if array[mid] == target:
            return mid # Found the target
        else if array[mid] < target:
            left = mid + 1 # Search the right half
        else:
            right = mid - 1 # Search the left half
    return -1 # Target not found
```
`O(log n)`

## Two Pointers
- Iterates two monotonic pointers an array to search for a pair of indices that satisfies some condition.
- Possibly accompanied by a sorted array, which allows you to rule out pairs that aren't created by sliding the left or right pointer by 1.
```python
# Ex. Find 2 indices in array that sum up to target
def two_pointer(array, target):
    left = 0
    right = len(array) - 1

    while left < right:
        # Ex. Sum criteria
        current_sum = array[left] + array[right]
        if current_sum == target:
            return (left, right)  # Found a valid pair
        elif current_sum < target:
            left += 1  # Increase sum by moving left pointer
        else:
            right -= 1  # Decrease sum by moving right pointer
    return None  # No pair found
```
`O(n)`

## Backtracking
- A backtracking algorithm works by recursively exploring all possible solutions to a problem.
- It is often associated with a decision tree, because backtracking works by trying different options and undoing them if they lead to a dead end.
- For this reason, it can be similar to DFS/BFS which also search through graph structures.
```python
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return

    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```
Runtime depends on many candidates are spawned by each decision that need to be explored. For a binary decision tree, `O(2^N)`, but can potentially go up to `O(N!)`.

## Depth First Search (DFS)

- Used to explore all paths or branches in graphs/trees to solve:
- Finding a path between two nodes, checking if a graph contains a cycle, finding a topological order in a DAG, counting connected components in a graph

```python
def dfs(graph, start):

    visited = set()
    stack = [start]

    while stack:
        # Pop off the most recently added node
        node = stack.pop()
        if node not in visited:
            # Process the current node
            print(node)
            visited.add(node)
            stack.extend(graph[node])
```
`O(# vertices + # edges)`

## Breadth First Search (BFS)

- Finding the shortest path between two nodes (unweighted), printing all nodes of a tree level by level, finding all connected components in a graph

```python
def bfs(graph, start):
    visited = set()
    queue = [start]

    while queue:
        # Pop off the oldest added node
        node = queue.pop(0)
        if node not in visited:
            # Process the current node
            print(node)
            visited.add(node)
            queue.extend(graph[node])
```
`O(# vertices + # edges)`

## Dynamic Programming (DP)
- Use the results of smaller subproblems to solve the overall problem.
- Can also be though of as cacheing intermediate results.

## Sliding Window
- Use two pointers (left and right) to create a “window” or subrange.
- The problem will ask us to return the maximum or minimum subrange that satisfies a given condition.

```python
def sliding_window(array):
    left, right = 0, 0
    # Iterate over elements in our input
    while right < len(array):
        # Expand the window
        # Meet the condition to stop expansion
        while condition:
            # Process the current window   
            # Contract the window
        right += 1
```
[Extra](https://medium.com/@timpark0807/leetcode-is-easy-sliding-window-c44c11cc33e1)

## Heap

- Max-heap: Tree structure where the value of the parent is always > than child

`O(log n) insertion`

- Min-heap: Tree structure where the value of the parent is always < then child
- Sometimes used to implement a priority queue: a FIFO list with a priority that allows some elements to skip.
```python
# Badly implemented with a list
pq = []
# Sort list after every insertion
pq.append((1, "Item A"))
pq.sort(reverse=True)
pq.append((2, "Item B"))
pq.sort(reverse=True)

# Implemented in heapq
import heapq
customers = []
heapq.heappush(customers, (1, "Item A"))
heapq.heappush(customers, (2, "Item B"))

# Result
[(2, "Item B"), (1, "Item A")]
```

## Top K Elements
- Find k largest, k smallest, or k most frequent elements in a dataset
```python
# Create a max/min heap of size k
heap = [array[0], array[1], array[2]]
# Then iterate over the rest of the array, comparing elements to the top element in heap.
# This allows you to remove the top element if the current element is larger/smaller.

# To find k largest -> use a min-heap so that the top element is the smallest of the k.
# To find k smallest -> use a max-heap so that the top element is the biggest of the k.
```

<!-- ## QuickSelect
- Finds the top kth element of an unsorted dataset -->

## Trie
- Basically a tree that represents strings

<img src="./assets/Triedatastructure1.png" height="300">

## Prefix Sum
- Used to find sum of elements in a some subarray of the main array
```python
array = [1, 2, 3, 4, 5]
#           i     j
# Ex. Find sum of elements between i and j
prefix = [1, 3, 6, 10, 15]
#               k
# Calculate the sum of the prefix up to index k
assert sum(array[i:j+1]) == prefix[j] - prefix[i-1]
# Now you can calculate the sum of some subarray in O(1)
```

## Two Pointers

## Fast and Slow Pointers
- Helps to solve problems with linked lists and arrays which involves finding cycles

## Sliding Window
- Helps to find a subarray that meets some condition

## Linked List In-place Reversal
- For rearranging links in a linked list
```python
def reverse_linked_list(head):
    prev = None
    current = head

    while current is not None:
        next = current.next
        current.next = prev
        prev = current
        current = next
    return prev
```

## Monotonic Stack
- Uses a stack to find the next greater or next smaller element in an array
```python
array = [1, 2, 3, 4, 5]
# Ex. For each element, find the next greater element (subarray to the right).

def next_greater_element(array):
    n = len(array)
    stack = []
    result = [-1] * n
    for i in range(n):
        # For each element, check if its greater than the top of the stack
        while stack and array[i] > arr[stack[-1]]
            result[stack.pop()] == array[i]
        stack.append(i)
    return result
```

## Overlapping Intervals
- Useful for problems with intervals or ranges that may overlap.
- Sorting intervals by the start makes it easy to detect overlaps.

## Modified Binary Search
- Useful for problems that are almost/nearly sorted. Typically involves a small modification to binary search.

## Binary Tree Traversal
- PreOrder: root -> left -> right
- InOrder: left -> root -> right
- PostOrder: left -> right -> root
- LevelOrder: level by level
```python
def preorder(node):
    if node:
        print(node.val, end=" ")
        preorder(node.left)
        preorder(node.right)

def inorder(node):
    if node:
        preorder(node.left)
        print(node.val, end=" ")
        preorder(node.right)

def postorder(node):
    if node:
        preorder(node.left)
        preorder(node.right)
        print(node.val, end=" ")

def levelorder(node):
    # Use a queue
```

## Matrix Traversal
- Most matrix traversal problems can be seen as graph problems