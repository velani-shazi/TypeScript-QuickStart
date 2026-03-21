# 🧠 Data Structures & Algorithms — Exercise Set
### TypeScript Practice Problems | Beginner → Intermediate → Advanced

---

> *"Tell me and I forget. Teach me and I remember. Involve me and I learn."*
> — Benjamin Franklin

---

## How to Use This Document

- Work through problems **in order within each tier** — they build on each other.
- Before looking for hints, spend **at least 15–20 minutes** on each problem.
- Write your solution in TypeScript and test it against the provided examples.
- Think about **time and space complexity** for every solution you write.
- Ask yourself: *"Can I do better?"*

---

## 🟢 Beginner Exercises

*These problems reinforce core concepts. Focus on correctness and understanding before optimising.*

---

### B-01 — Find the Largest Number

**Topic**: Arrays  
**Difficulty**: 🟢 Beginner

**Description**:  
Given an array of integers, return the largest number in the array. Do **not** use built-in functions like `Math.max()` or `.sort()`. Implement the logic yourself using a loop.

**Input/Output Examples**:

```
Input:  [3, 1, 9, 2, 7]
Output: 9

Input:  [-5, -2, -8, -1]
Output: -1

Input:  [42]
Output: 42
```

**Constraints**:
- The array will have at least one element.
- Elements can be negative.
- Do not use `Math.max()` or `.sort()`.

**Signature**:
```typescript
function findLargest(nums: number[]): number { ... }
```

---

### B-02 — Reverse a String

**Topic**: Arrays / Strings  
**Difficulty**: 🟢 Beginner

**Description**:  
Given a string, return it reversed. Do **not** use the built-in `.reverse()` method. Think about how you would swap characters using two pointers.

**Input/Output Examples**:

```
Input:  "hello"
Output: "olleh"

Input:  "TypeScript"
Output: "tpircSepyT"

Input:  "a"
Output: "a"

Input:  ""
Output: ""
```

**Constraints**:
- Do not use `Array.prototype.reverse()`.
- Input can be an empty string.

**Signature**:
```typescript
function reverseString(str: string): string { ... }
```

---

### B-03 — Count Occurrences

**Topic**: Hash Maps  
**Difficulty**: 🟢 Beginner

**Description**:  
Given an array of strings, return a `Map` (or object) that counts how many times each string appears.

**Input/Output Examples**:

```
Input:  ["apple", "banana", "apple", "cherry", "banana", "apple"]
Output: Map { "apple" => 3, "banana" => 2, "cherry" => 1 }

Input:  ["a", "b", "c"]
Output: Map { "a" => 1, "b" => 1, "c" => 1 }

Input:  []
Output: Map {}
```

**Constraints**:
- Return a `Map<string, number>`.
- Handle empty arrays.

**Signature**:
```typescript
function countOccurrences(items: string[]): Map<string, number> { ... }
```

---

### B-04 — Check for Palindrome

**Topic**: Strings / Two Pointers  
**Difficulty**: 🟢 Beginner

**Description**:  
A palindrome is a word that reads the same forwards and backwards (e.g., "racecar", "madam"). Given a string, return `true` if it is a palindrome, `false` otherwise. Ignore case.

**Input/Output Examples**:

```
Input:  "racecar"
Output: true

Input:  "RaceCar"
Output: true  (case insensitive)

Input:  "hello"
Output: false

Input:  "a"
Output: true

Input:  ""
Output: true
```

**Constraints**:
- Comparison should be case-insensitive.
- Consider only alphanumeric characters (bonus: ignore spaces and punctuation).

**Signature**:
```typescript
function isPalindrome(str: string): boolean { ... }
```

---

### B-05 — FizzBuzz

**Topic**: Arrays / Loops  
**Difficulty**: 🟢 Beginner

**Description**:  
Given a number `n`, return an array of strings from `1` to `n` where:
- Multiples of 3 are replaced with `"Fizz"`
- Multiples of 5 are replaced with `"Buzz"`
- Multiples of both 3 and 5 are replaced with `"FizzBuzz"`
- All other numbers are their string representation

**Input/Output Examples**:

```
Input:  n = 15
Output: ["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]

Input:  n = 5
Output: ["1","2","Fizz","4","Buzz"]

Input:  n = 1
Output: ["1"]
```

**Constraints**:
- `1 <= n <= 10,000`

**Signature**:
```typescript
function fizzBuzz(n: number): string[] { ... }
```

---

### B-06 — Implement a Stack

**Topic**: Stacks  
**Difficulty**: 🟢 Beginner

**Description**:  
Implement a generic `Stack<T>` class from scratch **without** using any built-in stack or queue data structures. It should support the following operations:

- `push(item)` — add an item to the top
- `pop()` — remove and return the top item (throw an error if empty)
- `peek()` — return the top item without removing it
- `isEmpty()` — return `true` if the stack has no elements
- `size()` — return the number of items

**Input/Output Examples**:

```
const stack = new Stack<number>();
stack.push(10);
stack.push(20);
stack.push(30);
stack.peek()    → 30
stack.pop()     → 30
stack.pop()     → 20
stack.size()    → 1
stack.isEmpty() → false
stack.pop()     → 10
stack.isEmpty() → true
stack.pop()     → throws Error
```

**Constraints**:
- Must be generic (works with `number`, `string`, etc.)
- `pop()` on an empty stack must throw a descriptive error.

---

### B-07 — Sum of Array Using Recursion

**Topic**: Recursion  
**Difficulty**: 🟢 Beginner

**Description**:  
Given an array of numbers, calculate the sum using **recursion only** — no loops allowed.

**Input/Output Examples**:

```
Input:  [1, 2, 3, 4, 5]
Output: 15

Input:  [10, 20, 30]
Output: 60

Input:  []
Output: 0

Input:  [7]
Output: 7
```

**Constraints**:
- No loops (`for`, `while`, `forEach`, `.reduce()`, etc.)
- Must use recursion.

**Signature**:
```typescript
function sumArray(nums: number[]): number { ... }
```

---

### B-08 — Remove Duplicates from Array

**Topic**: Sets  
**Difficulty**: 🟢 Beginner

**Description**:  
Given an array, return a new array with all duplicate values removed. Preserve the original order of first appearances.

**Input/Output Examples**:

```
Input:  [1, 2, 2, 3, 4, 4, 5]
Output: [1, 2, 3, 4, 5]

Input:  ["a", "b", "a", "c", "b"]
Output: ["a", "b", "c"]

Input:  [1, 1, 1, 1]
Output: [1]

Input:  []
Output: []
```

**Constraints**:
- Return a new array — do not mutate the original.
- Preserve order of first appearance.

**Signature**:
```typescript
function removeDuplicates<T>(arr: T[]): T[] { ... }
```

---

### B-09 — Check if Array is Sorted

**Topic**: Arrays  
**Difficulty**: 🟢 Beginner

**Description**:  
Given an array of numbers, return `true` if it is sorted in **non-decreasing** (ascending) order, and `false` otherwise. An empty or single-element array is considered sorted.

**Input/Output Examples**:

```
Input:  [1, 2, 3, 4, 5]
Output: true

Input:  [1, 1, 2, 3]
Output: true  (equal elements are allowed)

Input:  [5, 3, 1]
Output: false

Input:  [1]
Output: true

Input:  []
Output: true
```

**Signature**:
```typescript
function isSorted(nums: number[]): boolean { ... }
```

---

### B-10 — Implement a Queue

**Topic**: Queues  
**Difficulty**: 🟢 Beginner

**Description**:  
Implement a generic `Queue<T>` class supporting:

- `enqueue(item)` — add item to the rear
- `dequeue()` — remove and return item from the front (throw error if empty)
- `peek()` — return front item without removing
- `isEmpty()` — return `true` if empty
- `size()` — return number of items

**Dequeue must be O(1) — do not use an array's `.shift()` method.**

**Input/Output Examples**:

```
const q = new Queue<string>();
q.enqueue("A");
q.enqueue("B");
q.enqueue("C");
q.peek()     → "A"
q.dequeue()  → "A"
q.dequeue()  → "B"
q.size()     → 1
q.isEmpty()  → false
```

**Constraints**:
- `dequeue()` must run in O(1) time.
- Throw an error when dequeuing from an empty queue.

---

## 🟡 Intermediate Exercises

*These problems require combining multiple concepts and thinking more carefully about efficiency.*

---

### I-01 — Two Sum

**Topic**: Arrays, Hash Maps  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given an array of integers `nums` and a target integer `target`, return the **indices** of the two numbers that add up to `target`. You may assume exactly one solution exists, and you cannot use the same element twice.

**Input/Output Examples**:

```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]   (nums[0] + nums[1] = 2 + 7 = 9)

Input:  nums = [3, 2, 4], target = 6
Output: [1, 2]   (nums[1] + nums[2] = 2 + 4 = 6)

Input:  nums = [3, 3], target = 6
Output: [0, 1]
```

**Constraints**:
- `2 <= nums.length <= 10,000`
- One solution is guaranteed to exist.
- Your solution must run in **O(n) time**.

**Signature**:
```typescript
function twoSum(nums: number[], target: number): [number, number] { ... }
```

---

### I-02 — Valid Parentheses

**Topic**: Stacks  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given a string containing only the characters `(`, `)`, `{`, `}`, `[`, `]`, determine if the string is valid. A string is valid if:
- Every opening bracket has a corresponding closing bracket of the same type.
- Brackets must be closed in the correct order.

**Input/Output Examples**:

```
Input:  "()"
Output: true

Input:  "()[]{}"
Output: true

Input:  "(]"
Output: false

Input:  "([)]"
Output: false

Input:  "{[]}"
Output: true

Input:  ""
Output: true
```

**Constraints**:
- Input string contains only `(){}[]`.
- `0 <= s.length <= 10,000`

**Signature**:
```typescript
function isValid(s: string): boolean { ... }
```

---

### I-03 — Linked List: Detect a Cycle

**Topic**: Linked Lists, Two Pointers  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given the head of a singly-linked list, determine if the list contains a **cycle** (i.e., a node's `next` pointer points back to a previous node, forming a loop).

Use **Floyd's Cycle Detection Algorithm** (the "tortoise and hare" approach):  
- Use two pointers — a slow one (moves 1 step at a time) and a fast one (moves 2 steps).
- If they ever meet, there is a cycle.
- If the fast pointer reaches `null`, there is no cycle.

**Input/Output Examples**:

```
List: 3 → 2 → 0 → -4 → (back to node 2)
Output: true

List: 1 → 2 → (back to node 1)
Output: true

List: 1 → 2 → 3 → null
Output: false

List: 1 → null
Output: false
```

**Constraints**:
- Must solve in **O(1) extra space** (no extra data structures like Sets).
- This requires Floyd's algorithm.

**Signature**:
```typescript
function hasCycle(head: ListNode<number> | null): boolean { ... }
```

---

### I-04 — Binary Search on a Sorted Array

**Topic**: Binary Search  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given a sorted array of integers and a target value, return the **index** of the target if found, or `-1` if not. Your solution must run in O(log n) time.

**Bonus**: Implement both the **iterative** and **recursive** versions.

**Input/Output Examples**:

```
Input:  nums = [-1, 0, 3, 5, 9, 12], target = 9
Output: 4

Input:  nums = [-1, 0, 3, 5, 9, 12], target = 2
Output: -1

Input:  nums = [5], target = 5
Output: 0

Input:  nums = [5], target = 0
Output: -1
```

**Constraints**:
- Array is sorted in ascending order.
- No duplicate values.
- Must be O(log n).

---

### I-05 — Merge Sort Implementation

**Topic**: Sorting, Recursion  
**Difficulty**: 🟡 Intermediate

**Description**:  
Implement **Merge Sort** from scratch. Your function should take an array of numbers and return a new sorted array in ascending order. Ensure your implementation:
1. Divides the array in half
2. Recursively sorts each half
3. Merges the two sorted halves

**Input/Output Examples**:

```
Input:  [38, 27, 43, 3, 9, 82, 10]
Output: [3, 9, 10, 27, 38, 43, 82]

Input:  [5, 1]
Output: [1, 5]

Input:  [1]
Output: [1]

Input:  []
Output: []
```

**Constraints**:
- Do not use `.sort()`.
- Must have O(n log n) time complexity.
- Must return a **new** array (do not mutate the input).

---

### I-06 — Maximum Depth of a Binary Tree

**Topic**: Trees, Recursion / DFS  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given the root of a binary tree, return its **maximum depth** — the number of nodes along the longest path from the root node down to the farthest leaf node.

**Input/Output Examples**:

```
Tree:
        3
       / \
      9   20
         /  \
        15   7

Output: 3

Tree:
    1
     \
      2

Output: 2

Tree: null
Output: 0
```

**Constraints**:
- The number of nodes is in the range `[0, 10,000]`.
- Think about both recursive and iterative (BFS) approaches.

**Signature**:
```typescript
function maxDepth(root: TreeNode | null): number { ... }
```

---

### I-07 — Level Order Traversal of a Binary Tree

**Topic**: Trees, BFS, Queues  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given the root of a binary tree, return the **level order traversal** of its nodes' values (i.e., from left to right, level by level). Each level should be its own sub-array.

**Input/Output Examples**:

```
Tree:
        3
       / \
      9   20
         /  \
        15   7

Output: [[3], [9, 20], [15, 7]]

Tree:
    1

Output: [[1]]

Tree: null
Output: []
```

**Constraints**:
- Must use BFS (a queue-based approach).
- The number of nodes can be up to 2,000.

**Signature**:
```typescript
function levelOrder(root: TreeNode | null): number[][] { ... }
```

---

### I-08 — BST Validity Check

**Topic**: Trees, DFS  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given the root of a binary tree, determine if it is a **valid Binary Search Tree (BST)**. A valid BST satisfies:
- The left subtree of a node contains only nodes with values **less than** the node's value.
- The right subtree contains only values **greater than** the node's value.
- Both subtrees must also be valid BSTs.

**Watch out**: A common mistake is only comparing a node with its immediate children. You must enforce the rule across the entire subtree.

**Input/Output Examples**:

```
Tree:
     2
    / \
   1   3
Output: true

Tree:
     5
    / \
   1   4
      / \
     3   6
Output: false  (4 is less than 5 but is in the right subtree)

Tree:
       10
      /  \
     5    15
         /  \
        6    20
Output: false  (6 < 10 but is in the right subtree)
```

**Constraints**:
- Think about passing valid **min/max bounds** down through recursion.

**Signature**:
```typescript
function isValidBST(root: TreeNode | null): boolean { ... }
```

---

### I-09 — Number of Islands

**Topic**: Graphs, DFS/BFS, 2D Grids  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given a 2D grid of `"1"` (land) and `"0"` (water), count the number of **islands**. An island is formed by connecting adjacent lands **horizontally or vertically**. Assume the grid is surrounded by water.

**Input/Output Examples**:

```
Input:
[
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1

Input:
[
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

**Constraints**:
- `1 <= grid.length, grid[i].length <= 300`
- You may modify the input grid (mark visited cells to avoid revisiting).

**Signature**:
```typescript
function numIslands(grid: string[][]): number { ... }
```

---

### I-10 — Fibonacci with Memoization

**Topic**: Recursion, Dynamic Programming  
**Difficulty**: 🟡 Intermediate

**Description**:  
Implement a function to compute the `n`th Fibonacci number (0-indexed: `fib(0) = 0`, `fib(1) = 1`, `fib(2) = 1`, etc.) using **memoization** to achieve O(n) time complexity.

Then, also implement it using a **bottom-up iterative approach** (tabulation) with O(1) space.

**Input/Output Examples**:

```
Input:  0  → Output: 0
Input:  1  → Output: 1
Input:  5  → Output: 5
Input:  10 → Output: 55
Input:  20 → Output: 6765
Input:  50 → Output: 12586269025
```

**Constraints**:
- Your memoized version must not recalculate the same subproblem twice.
- The iterative version must use O(1) space (only two variables).

**Signatures**:
```typescript
function fibMemo(n: number): number { ... }
function fibIterative(n: number): number { ... }
```

---

### I-11 — Longest Consecutive Sequence

**Topic**: Sets, Arrays  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given an unsorted array of integers, find the length of the **longest consecutive elements sequence**. Your algorithm must run in **O(n)** time.

**Input/Output Examples**:

```
Input:  [100, 4, 200, 1, 3, 2]
Output: 4   (sequence: 1, 2, 3, 4)

Input:  [0, 3, 7, 2, 5, 8, 4, 6, 0, 1]
Output: 9   (sequence: 0, 1, 2, 3, 4, 5, 6, 7, 8)

Input:  [1]
Output: 1

Input:  []
Output: 0
```

**Constraints**:
- O(n) time complexity required — no sorting allowed.
- **Hint**: Use a `Set` to check if a number is the start of a sequence.

**Signature**:
```typescript
function longestConsecutive(nums: number[]): number { ... }
```

---

### I-12 — Reverse a Linked List

**Topic**: Linked Lists  
**Difficulty**: 🟡 Intermediate

**Description**:  
Given the head of a singly linked list, reverse the list and return the new head. Implement both the **iterative** and **recursive** approaches.

**Input/Output Examples**:

```
Input:  1 → 2 → 3 → 4 → 5 → null
Output: 5 → 4 → 3 → 2 → 1 → null

Input:  1 → 2 → null
Output: 2 → 1 → null

Input:  1 → null
Output: 1 → null

Input:  null
Output: null
```

**Constraints**:
- Number of nodes: 0 to 5000.
- Implement both iterative (O(1) space) and recursive (O(n) space) versions.

---

## 🔴 Advanced Exercises

*These problems require combining multiple data structures, algorithmic strategies (divide & conquer, greedy, dynamic programming), and deeper analysis.*

---

### A-01 — LRU Cache

**Topic**: Hash Maps, Doubly Linked Lists  
**Difficulty**: 🔴 Advanced

**Description**:  
Design and implement an **LRU (Least Recently Used) Cache**. It should support the following operations in **O(1)** time each:

- `get(key)` — return the value of the key if it exists, otherwise return `-1`. Also marks the key as recently used.
- `put(key, value)` — insert or update the value. If the cache reaches its capacity, evict the **least recently used** item before inserting.

**Input/Output Examples**:

```
const cache = new LRUCache(2); // capacity = 2

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);    → 1   (key 1 is now most recently used)
cache.put(3, 3); → evicts key 2 (least recently used)
cache.get(2);    → -1  (key 2 was evicted)
cache.put(4, 4); → evicts key 1
cache.get(1);    → -1  (evicted)
cache.get(3);    → 3
cache.get(4);    → 4
```

**Constraints**:
- Both `get` and `put` must be O(1).
- Capacity is a positive integer.
- **Hint**: Combine a `Map` (for O(1) access) with a doubly linked list (to track usage order efficiently).

---

### A-02 — Graph: Detect a Cycle in a Directed Graph

**Topic**: Graphs, DFS  
**Difficulty**: 🔴 Advanced

**Description**:  
Given a directed graph represented as an adjacency list, determine if the graph contains a **cycle**. A directed graph has a cycle if there is any path that leads back to a node already on the current DFS path.

**Input/Output Examples**:

```
Graph 1 (with cycle):
0 → 1 → 2 → 0
Output: true

Graph 2 (no cycle — DAG):
0 → 1 → 3
0 → 2 → 3
Output: false

Graph 3:
0 → 1
1 → 2
2 → 3
Output: false
```

**Constraints**:
- The graph may be disconnected (check all nodes).
- Must use DFS with a "currently in recursion stack" tracking set.
- A "visited" set alone is not sufficient — you need to distinguish between fully processed nodes and nodes on the current DFS path.

**Signature**:
```typescript
function hasCycleDirected(graph: Map<number, number[]>, numNodes: number): boolean { ... }
```

---

### A-03 — Serialize and Deserialise a Binary Tree

**Topic**: Trees, Strings, BFS/DFS  
**Difficulty**: 🔴 Advanced

**Description**:  
Design an algorithm to **serialize** a binary tree to a string and **deserialize** the string back to the exact same tree. Serialisation is the process of converting a data structure into a format that can be stored/transmitted and reconstructed later.

**Input/Output Examples**:

```
Tree:
    1
   / \
  2   3
     / \
    4   5

serialize(root) → "1,2,null,null,3,4,null,null,5,null,null"  (or similar format)
deserialize("1,2,null,null,3,4,null,null,5,null,null") → same tree structure
```

**Constraints**:
- Your `deserialize` applied to the output of `serialize` must reproduce the original tree exactly.
- Handle `null` nodes explicitly in your string format.
- Both functions should run in O(n).

**Signatures**:
```typescript
function serialize(root: TreeNode | null): string { ... }
function deserialize(data: string): TreeNode | null { ... }
```

---

### A-04 — Word Ladder (BFS Shortest Path)

**Topic**: Graphs, BFS  
**Difficulty**: 🔴 Advanced

**Description**:  
Given two words `beginWord` and `endWord`, and a word list `wordList`, return the **minimum number of word transformations** to go from `beginWord` to `endWord`. Each transformation must:
1. Change exactly **one letter** at a time.
2. The resulting word must be in the `wordList`.

Return `0` if no such sequence exists.

**Input/Output Examples**:

```
Input:  beginWord = "hit", endWord = "cog"
        wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: "hit" → "hot" → "dot" → "dog" → "cog"

Input:  beginWord = "hit", endWord = "cog"
        wordList = ["hot","dot","dog","lot","log"]
Output: 0   ("cog" is not in wordList)

Input:  beginWord = "a", endWord = "c"
        wordList = ["a", "b", "c"]
Output: 2   ("a" → "c")
```

**Constraints**:
- `1 <= beginWord.length <= 10`
- `beginWord.length == endWord.length`
- All words are lowercase English letters.
- Use BFS to guarantee the shortest path.

**Signature**:
```typescript
function ladderLength(beginWord: string, endWord: string, wordList: string[]): number { ... }
```

---

### A-05 — Merge k Sorted Lists

**Topic**: Linked Lists, Heaps / Divide & Conquer  
**Difficulty**: 🔴 Advanced

**Description**:  
You are given an array of `k` sorted linked lists. Merge all of them into one **sorted** linked list and return its head.

**Input/Output Examples**:

```
Input:  lists = [
          1 → 4 → 5,
          1 → 3 → 4,
          2 → 6
        ]
Output: 1 → 1 → 2 → 3 → 4 → 4 → 5 → 6

Input:  lists = []
Output: null

Input:  lists = [ [] ]
Output: null
```

**Constraints**:
- `k == lists.length`, `0 <= k <= 10,000`
- Total number of nodes across all lists: up to 500,000.
- Must be more efficient than merging lists one at a time (O(kN) → aim for O(N log k)).
- **Hint**: Use the divide-and-conquer approach — repeatedly merge pairs of lists.

---

### A-06 — Trapping Rainwater

**Topic**: Arrays, Two Pointers  
**Difficulty**: 🔴 Advanced

**Description**:  
Given an array of non-negative integers `height` representing an elevation map where the width of each bar is 1, compute how much water can be **trapped after raining**.

**Input/Output Examples**:

```
Input:  [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6

Visualised:
       █
   █ ▒ █ ▒ █
█ ▒ █ ▒ ▒ █ █ ▒ █

(▒ = trapped water)

Input:  [4,2,0,3,2,5]
Output: 9

Input:  [3,0,0,2,0,4]
Output: 10

Input:  [1,0,1]
Output: 1
```

**Constraints**:
- `0 <= height[i] <= 100,000`
- Must solve in **O(n) time** and **O(1) space** using the two-pointer technique.

**Signature**:
```typescript
function trap(height: number[]): number { ... }
```

---

### A-07 — Implement a Trie (Prefix Tree)

**Topic**: Trees, Strings  
**Difficulty**: 🔴 Advanced

**Description**:  
A **Trie** (pronounced "try") is a tree data structure used to efficiently store and retrieve strings. Implement a `Trie` class with the following methods:

- `insert(word)` — insert a word into the trie
- `search(word)` — return `true` if the exact word exists in the trie
- `startsWith(prefix)` — return `true` if any word in the trie starts with the given prefix

**Input/Output Examples**:

```
const trie = new Trie();
trie.insert("apple");
trie.search("apple")    → true
trie.search("app")      → false  (not a complete word)
trie.startsWith("app")  → true
trie.insert("app");
trie.search("app")      → true   (now "app" is also inserted)
trie.startsWith("xyz")  → false
```

**Constraints**:
- All inputs consist of lowercase English letters only.
- `1 <= word.length <= 2,000`
- At most 30,000 calls total to `insert`, `search`, `startsWith`.

---

### A-08 — Shortest Path in a Weighted Graph (Dijkstra's Algorithm)

**Topic**: Graphs, Priority Queue  
**Difficulty**: 🔴 Advanced

**Description**:  
Given a weighted, directed graph, find the **shortest path** from a source node to all other nodes using **Dijkstra's Algorithm**. Return a map of `{ node → minimum distance from source }`.

**Input/Output Examples**:

```
Graph edges (node, neighbour, weight):
A → B (4)
A → C (2)
C → B (1)
B → D (5)
C → D (8)
C → E (10)
B → E (2)
D → E (2)

Start: "A"

Output: {
  A: 0,
  B: 3,   (A→C→B: 2+1=3, better than A→B: 4)
  C: 2,
  D: 8,   (A→C→B→D: 2+1+5=8)
  E: 5    (A→C→B→E: 2+1+2=5)
}
```

**Constraints**:
- Edge weights are non-negative (Dijkstra's doesn't work with negative weights).
- You will need to implement a simple **min-priority queue** or use a sorted structure.
- The graph can have up to 1,000 nodes.

---

### A-09 — Longest Common Subsequence

**Topic**: Dynamic Programming  
**Difficulty**: 🔴 Advanced

**Description**:  
Given two strings `text1` and `text2`, return the length of their **longest common subsequence (LCS)**. A subsequence is a sequence derived from another sequence by deleting some elements without changing the order of the remaining elements.

**Input/Output Examples**:

```
Input:  text1 = "abcde", text2 = "ace"
Output: 3   (LCS is "ace")

Input:  text1 = "abc", text2 = "abc"
Output: 3   (LCS is "abc")

Input:  text1 = "abc", text2 = "def"
Output: 0   (no common subsequence)

Input:  text1 = "AGGTAB", text2 = "GXTXAYB"
Output: 4   (LCS is "GTAB")
```

**Constraints**:
- `1 <= text1.length, text2.length <= 1,000`
- Must solve using **dynamic programming** (a 2D table), not brute force.

**Signature**:
```typescript
function longestCommonSubsequence(text1: string, text2: string): number { ... }
```

---

### A-10 — Design a Graph & Run BFS/DFS

**Topic**: Graphs, BFS, DFS  
**Difficulty**: 🔴 Advanced

**Description**:  
This is a synthesis problem. Complete the following steps:

1. Implement a `WeightedGraph` class with an adjacency list where each neighbour is stored as `{ node: string, weight: number }`.
2. Add methods: `addVertex`, `addEdge` (directed), `getNeighbors`, `print`.
3. Implement `DFS(start)` that returns nodes in DFS traversal order.
4. Implement `BFS(start)` that returns nodes in BFS traversal order.
5. Implement `hasPath(start, end)` that returns `true` if any path exists from `start` to `end`.

**Input/Output Examples**:

```
const g = new WeightedGraph();
g.addEdge("A", "B", 4);
g.addEdge("A", "C", 2);
g.addEdge("B", "D", 5);
g.addEdge("C", "D", 8);
g.addEdge("D", "E", 2);

g.DFS("A")         → ["A", "B", "D", "E", "C"]  (or valid DFS order)
g.BFS("A")         → ["A", "B", "C", "D", "E"]  (level by level)
g.hasPath("A","E") → true
g.hasPath("E","A") → false  (directed graph, no reverse edge)
g.hasPath("A","Z") → false  (Z doesn't exist)
```

**Constraints**:
- Directed graph (edges go one way unless you explicitly add both directions).
- Use a `Set` to track visited nodes and prevent infinite loops.
- `hasPath` should use DFS or BFS.

---

## Bonus Challenges

*For those who want to go further — these tie everything together.*

---

### Bonus-01 — Design Twitter (Mini System Design)

Design a simplified version of Twitter using data structures. Implement a `Twitter` class with:
- `postTweet(userId, tweetId)` — compose a tweet
- `getNewsFeed(userId)` — retrieve the 10 most recent tweet IDs in the user's news feed (from themselves and people they follow), ordered by most recent
- `follow(followerId, followeeId)`
- `unfollow(followerId, followeeId)`

**Hint**: Use hash maps for user data and a max-heap or sorted structure for the news feed.

---

### Bonus-02 — Build an Expression Evaluator

Given a string representing a mathematical expression with `+`, `-`, `*`, `/`, and parentheses (e.g., `"3 + (4 * 2) - 1"`), evaluate it and return the result as a number.

**Hint**: Use two stacks — one for operators and one for numbers.

---

### Bonus-03 — Find All Paths in a Graph

Given a directed graph and a source and destination node, find **all possible paths** from source to destination.

```
Graph:
0 → 1
0 → 2
1 → 3
2 → 3
3 → 4

source = 0, destination = 4
Output: [[0,1,3,4], [0,2,3,4]]
```

---

## Progress Tracker

Use this table to track your progress:

| #      | Problem                          | Difficulty  | Status |
|:-------|:---------------------------------|:------------|:-------|
| B-01   | Find the Largest Number          | 🟢 Beginner  | ☐      |
| B-02   | Reverse a String                 | 🟢 Beginner  | ☐      |
| B-03   | Count Occurrences                | 🟢 Beginner  | ☐      |
| B-04   | Check for Palindrome             | 🟢 Beginner  | ☐      |
| B-05   | FizzBuzz                         | 🟢 Beginner  | ☐      |
| B-06   | Implement a Stack                | 🟢 Beginner  | ☐      |
| B-07   | Sum Using Recursion              | 🟢 Beginner  | ☐      |
| B-08   | Remove Duplicates                | 🟢 Beginner  | ☐      |
| B-09   | Check if Array is Sorted         | 🟢 Beginner  | ☐      |
| B-10   | Implement a Queue                | 🟢 Beginner  | ☐      |
| I-01   | Two Sum                          | 🟡 Intermediate| ☐    |
| I-02   | Valid Parentheses                | 🟡 Intermediate| ☐    |
| I-03   | Detect Cycle in Linked List      | 🟡 Intermediate| ☐    |
| I-04   | Binary Search                    | 🟡 Intermediate| ☐    |
| I-05   | Merge Sort                       | 🟡 Intermediate| ☐    |
| I-06   | Max Depth of Binary Tree         | 🟡 Intermediate| ☐    |
| I-07   | Level Order Traversal            | 🟡 Intermediate| ☐    |
| I-08   | BST Validity Check               | 🟡 Intermediate| ☐    |
| I-09   | Number of Islands                | 🟡 Intermediate| ☐    |
| I-10   | Fibonacci with Memoization       | 🟡 Intermediate| ☐    |
| I-11   | Longest Consecutive Sequence     | 🟡 Intermediate| ☐    |
| I-12   | Reverse a Linked List            | 🟡 Intermediate| ☐    |
| A-01   | LRU Cache                        | 🔴 Advanced  | ☐      |
| A-02   | Cycle in Directed Graph          | 🔴 Advanced  | ☐      |
| A-03   | Serialize/Deserialize BST        | 🔴 Advanced  | ☐      |
| A-04   | Word Ladder                      | 🔴 Advanced  | ☐      |
| A-05   | Merge k Sorted Lists             | 🔴 Advanced  | ☐      |
| A-06   | Trapping Rainwater               | 🔴 Advanced  | ☐      |
| A-07   | Implement a Trie                 | 🔴 Advanced  | ☐      |
| A-08   | Dijkstra's Algorithm             | 🔴 Advanced  | ☐      |
| A-09   | Longest Common Subsequence       | 🔴 Advanced  | ☐      |
| A-10   | Full Graph Design                | 🔴 Advanced  | ☐      |

---

*Good luck — and remember, struggling with a problem is not failing. It is learning. 💪*
