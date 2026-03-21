# 📘 Data Structures & Algorithms in TypeScript
### A Comprehensive Tutorial — Beginner to Intermediate

---

> *"Bad programmers worry about the code. Good programmers worry about data structures and their relationships."*
> — Linus Torvalds

---

## Table of Contents

1. [Introduction to DSA](#1-introduction-to-dsa)
2. [Time & Space Complexity](#2-time--space-complexity)
3. [Core Data Structures](#3-core-data-structures)
   - [Arrays](#31-arrays)
   - [Linked Lists](#32-linked-lists)
   - [Stacks](#33-stacks)
   - [Queues](#34-queues)
   - [Hash Maps](#35-hash-maps)
   - [Sets](#36-sets)
   - [Trees](#37-trees)
   - [Graphs](#38-graphs)
4. [Algorithms](#4-algorithms)
   - [Searching](#41-searching)
   - [Sorting](#42-sorting)
   - [Recursion](#43-recursion)
   - [Traversals (DFS & BFS)](#44-traversals-dfs--bfs)

---

## 1. Introduction to DSA

### 1.1 What Are Data Structures?

Imagine you are moving into a new apartment. You have hundreds of books, clothes, kitchen utensils, and documents. How do you organise them?

- Books go on **shelves** (easy to browse, find by title)
- Documents go in **folders** (grouped, labelled)
- Clothes go in a **wardrobe** (stacked or hung)

A **data structure** is exactly this — a way of **organising and storing data** in a computer so that it can be accessed and modified efficiently. The choice of data structure directly affects how fast and how much memory your program uses.

Common data structures include: arrays, linked lists, stacks, queues, trees, graphs, and hash maps.

### 1.2 What Are Algorithms?

An **algorithm** is a step-by-step set of instructions to solve a problem. Think of it as a recipe. Given certain ingredients (input), follow the recipe (algorithm) to produce a dish (output).

For example, an algorithm to find the largest number in a list:
1. Start with the first number as the "current largest"
2. Look at each remaining number
3. If it is bigger than "current largest", update
4. Return the final "current largest"

### 1.3 Why Do They Matter?

**Performance**: Without efficient data structures and algorithms, your application could be unacceptably slow. Imagine searching through 1 billion users one by one vs. using a hash map (nearly instant lookup).

**Interviews**: Major tech companies (Google, Meta, Amazon, Microsoft) heavily test DSA in interviews. It is the universal language of software engineering.

**Problem-solving mindset**: Learning DSA trains you to think systematically, break down complex problems, and reason about trade-offs.

**Real-world impact**:
- Google Search uses complex graph algorithms
- GPS navigation uses shortest-path algorithms (Dijkstra's)
- Databases use tree structures (B-Trees) for indexing
- Compilers use stacks to parse expressions

---

## 2. Time & Space Complexity

### 2.1 Why Measure Efficiency?

Two programs can produce the same output but behave very differently at scale. One might handle 100 items fine but grind to a halt at 1,000,000. We need a way to measure and compare efficiency — that is where **complexity analysis** comes in.

### 2.2 Big-O Notation

**Big-O notation** describes how the running time (or memory usage) of an algorithm **grows relative to the size of its input**. We call the input size `n`.

Big-O ignores constants and lower-order terms because we care about **growth trends**, not exact milliseconds.

#### The Most Common Complexities (Best → Worst)

| Notation     | Name         | Analogy                                         |
|:-------------|:-------------|:------------------------------------------------|
| O(1)         | Constant     | Looking up your name in your own contacts       |
| O(log n)     | Logarithmic  | Searching a phone book by halving each time     |
| O(n)         | Linear       | Reading every page of a book                    |
| O(n log n)   | Linearithmic | Merge sort — divide and conquer                 |
| O(n²)        | Quadratic    | Checking every pair of items in a list          |
| O(2ⁿ)        | Exponential  | Every possible subset of a set                  |
| O(n!)        | Factorial    | Every possible ordering of items                |

#### Visual Intuition

```
Operations
│
│                                              O(n!)
│                                    O(2ⁿ)
│                          O(n²)
│                O(n log n)
│         O(n)
│      O(log n)
│   O(1)
└─────────────────────────────────────── Input size (n)
```

The flatter the curve, the better your algorithm scales.

### 2.3 Constant Time — O(1)

```typescript
// O(1) — Accessing an element by index in an array
// No matter how large the array is, this ALWAYS takes the same time.
function getFirstElement(arr: number[]): number {
  return arr[0]; // Direct memory access — one operation, done.
}

// O(1) — Adding a key to a hash map
function addToMap(map: Map<string, number>, key: string, value: number): void {
  map.set(key, value); // Hash maps are designed for instant lookup and insertion
}
```

### 2.4 Linear Time — O(n)

```typescript
// O(n) — Finding the maximum value in an unsorted array
// We MUST look at every element at least once.
// If there are 100 elements → ~100 operations
// If there are 1,000,000 elements → ~1,000,000 operations
function findMax(arr: number[]): number {
  let max = arr[0]; // Start with first element as the assumed maximum

  for (let i = 1; i < arr.length; i++) {
    // Visit each element one time — this is what makes it O(n)
    if (arr[i] > max) {
      max = arr[i]; // Update max if we find something bigger
    }
  }

  return max;
}

// Example usage:
console.log(findMax([3, 1, 9, 2, 7])); // Output: 9
```

### 2.5 Quadratic Time — O(n²)

```typescript
// O(n²) — Checking for duplicate values using nested loops
// For each element (n), we compare it against every other element (n again)
// Total comparisons: n × n = n²
// With 100 elements → 10,000 operations
// With 1,000 elements → 1,000,000 operations — gets slow fast!

function hasDuplicates(arr: number[]): boolean {
  for (let i = 0; i < arr.length; i++) {       // Outer loop: each element
    for (let j = i + 1; j < arr.length; j++) { // Inner loop: every element after i
      if (arr[i] === arr[j]) {
        return true; // Found a duplicate
      }
    }
  }
  return false;
}

// Note: This can be done in O(n) using a Set — we will see that later!
```

### 2.6 Logarithmic Time — O(log n)

The key intuition: **every step cuts the problem in half**.

```typescript
// O(log n) — Binary search (requires a sorted array)
// With 1,000,000 elements, you only need about 20 steps!
// log₂(1,000,000) ≈ 20

function binarySearch(arr: number[], target: number): number {
  let left = 0;               // Start of search range
  let right = arr.length - 1; // End of search range

  while (left <= right) {
    // Find the middle index (avoids integer overflow vs. (left+right)/2)
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;      // Found it!
    } else if (arr[mid] < target) {
      left = mid + 1;  // Target must be in the RIGHT half — discard left
    } else {
      right = mid - 1; // Target must be in the LEFT half — discard right
    }
    // Each iteration HALVES the search space → O(log n)
  }

  return -1; // Target not found
}
```

### 2.7 Space Complexity

Space complexity measures how much **extra memory** your algorithm uses relative to input size.

```typescript
// O(1) Space — Reverse an array in-place (no extra storage needed)
function reverseInPlace(arr: number[]): number[] {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    // Swap elements using destructuring — no temp variable needed
    [arr[left], arr[right]] = [arr[right], arr[left]];
    left++;
    right--;
  }
  return arr;
}

// O(n) Space — Reverse by creating a new array
function reverseNew(arr: number[]): number[] {
  const result: number[] = []; // NEW array grows with input size → O(n) space
  for (let i = arr.length - 1; i >= 0; i--) {
    result.push(arr[i]);
  }
  return result;
}
```

> **Golden rule**: Always ask — "How does this scale? What happens when n = 1,000,000?"

---

## 3. Core Data Structures

---

### 3.1 Arrays

#### What Is an Array?

An array is the most fundamental data structure — a **contiguous block of memory** that stores elements of the same type, accessed by a numeric **index** starting at 0.

Think of it as a row of numbered mailboxes. To get mailbox #5, you go directly to position 5 — no searching needed.

```
Index:   0     1     2     3     4
       ┌─────┬─────┬─────┬─────┬─────┐
       │ 10  │ 20  │ 30  │ 40  │ 50  │
       └─────┴─────┴─────┴─────┴─────┘
```

#### Characteristics

| Operation         | Time Complexity | Why                                    |
|:------------------|:----------------|:---------------------------------------|
| Access by index   | O(1)            | Direct memory address calculation      |
| Search (unsorted) | O(n)            | May need to check every element        |
| Search (sorted)   | O(log n)        | Binary search possible                 |
| Insert at end     | O(1) amortised  | Just append (usually)                  |
| Insert at middle  | O(n)            | Must shift elements to make room       |
| Delete at middle  | O(n)            | Must shift elements to fill the gap    |

#### TypeScript Array Operations

```typescript
// ─── Declaration ───────────────────────────────────────────────────────────

// Typed array — TypeScript enforces that only numbers go in here
const scores: number[] = [95, 87, 72, 100, 68];

// Alternative syntax using generic notation
const names: Array<string> = ["Alice", "Bob", "Charlie"];

// ─── Accessing Elements ─────────────────────────────────────────────────────

console.log(scores[0]);               // 95  — First element (index 0)
console.log(scores[scores.length - 1]); // 68 — Last element

// ─── Common Built-in Methods ────────────────────────────────────────────────

scores.push(88);      // Add to END      → O(1): [95,87,72,100,68,88]
scores.pop();         // Remove from END → O(1): [95,87,72,100,68]
scores.unshift(50);   // Add to START    → O(n): [50,95,87,72,100,68] (shifts all)
scores.shift();       // Remove from START → O(n): [95,87,72,100,68] (shifts all)

// splice(startIndex, deleteCount, ...itemsToInsert)
scores.splice(2, 0, 99); // Insert 99 at index 2 → [95,87,99,72,100,68]
scores.splice(2, 1);     // Delete element at index 2 → [95,87,72,100,68]

// ─── Iteration ──────────────────────────────────────────────────────────────

// Classic for loop — gives you index control
for (let i = 0; i < scores.length; i++) {
  console.log(`Score at index ${i}: ${scores[i]}`);
}

// for...of — cleaner when you don't need the index
for (const score of scores) {
  console.log(score);
}

// forEach — functional style
scores.forEach((score, index) => {
  console.log(`${index}: ${score}`);
});

// ─── Transformation Methods ─────────────────────────────────────────────────

// map — transform every element, returns NEW array
const doubled = scores.map(s => s * 2); // [190, 174, 144, 200, 136]

// filter — keep only elements that pass a test
const passing = scores.filter(s => s >= 80); // [95, 87, 100]

// reduce — collapse the whole array into a single value
const total = scores.reduce((sum, s) => sum + s, 0); // 452
const average = total / scores.length;               // 90.4

// find — return FIRST element that matches
const firstHigh = scores.find(s => s > 90); // 95

// ─── Practical Example: Kadane's Algorithm (Maximum Subarray) ───────────────

// Problem: Given an array of integers, find the contiguous subarray
// with the largest sum.
// Example: [-2, 1, -3, 4, -1, 2, 1, -5, 4] → Answer: 6 (subarray [4,-1,2,1])

function maxSubarraySum(nums: number[]): number {
  // currentSum: best sum ending AT the current position
  let currentSum = nums[0];
  // maxSum: best sum we have seen anywhere so far
  let maxSum = nums[0];

  // Start from index 1 since we initialised with nums[0]
  for (let i = 1; i < nums.length; i++) {
    // Should we extend the previous subarray, or start fresh from nums[i]?
    // If currentSum is negative, it's a burden — start fresh.
    currentSum = Math.max(nums[i], currentSum + nums[i]);

    // Track the overall best
    maxSum = Math.max(maxSum, currentSum);
  }

  return maxSum;
}

console.log(maxSubarraySum([-2, 1, -3, 4, -1, 2, 1, -5, 4])); // 6
```

---

### 3.2 Linked Lists

#### What Is a Linked List?

Unlike arrays (contiguous memory), a linked list stores elements as **nodes** scattered anywhere in memory. Each node contains:
1. **Data** — the value stored
2. **Pointer** — the memory address of the NEXT node

Think of it like a **treasure hunt**: each clue (node) tells you where the next clue is, but you cannot jump to clue #5 without following clues 1 → 2 → 3 → 4 → 5.

```
HEAD
 │
 ▼
┌──────┬──────┐    ┌──────┬──────┐    ┌──────┬──────┐
│  10  │  ●───┼───▶│  20  │  ●───┼───▶│  30  │ null │
└──────┴──────┘    └──────┴──────┘    └──────┴──────┘
  Node 1               Node 2               Node 3 (tail)
```

#### When to Use a Linked List vs Array?

| Factor                    | Array         | Linked List         |
|:--------------------------|:--------------|:--------------------|
| Access by index           | O(1) ✅        | O(n) ❌              |
| Insert/Delete at front    | O(n) ❌        | O(1) ✅              |
| Insert/Delete in middle   | O(n)          | O(n) (traverse to find position) |
| Memory                    | Contiguous    | Scattered (extra pointer overhead) |
| Best for                  | Random access | Frequent front insertions/deletions |

#### Implementation

```typescript
// ─── Node Class ─────────────────────────────────────────────────────────────

// A single "link" in the chain
class ListNode<T> {
  data: T;           // The value stored in this node
  next: ListNode<T> | null; // Reference to the next node (null if last)

  constructor(data: T) {
    this.data = data;
    this.next = null; // When first created, a node points to nothing
  }
}

// ─── Singly Linked List Class ────────────────────────────────────────────────

class LinkedList<T> {
  head: ListNode<T> | null; // The first node (entry point to the list)
  size: number;             // Track how many nodes we have

  constructor() {
    this.head = null; // Empty list — no head yet
    this.size = 0;
  }

  // ── Insert at the front — O(1) ─────────────────────────────────────────
  // This is the key advantage of linked lists over arrays!
  prepend(data: T): void {
    const newNode = new ListNode(data); // Create the new node
    newNode.next = this.head;           // New node points to old head
    this.head = newNode;                // Update head to be new node
    this.size++;
  }

  // ── Insert at the end — O(n) ───────────────────────────────────────────
  // We must traverse to the last node first (no direct tail access here)
  append(data: T): void {
    const newNode = new ListNode(data);

    // Special case: list is empty — new node becomes the head
    if (!this.head) {
      this.head = newNode;
      this.size++;
      return;
    }

    // Traverse to the last node
    let current = this.head;
    while (current.next !== null) {
      current = current.next; // Move to the next node
    }
    // current is now the last node
    current.next = newNode; // Link last node to new node
    this.size++;
  }

  // ── Delete a node by value — O(n) ─────────────────────────────────────
  delete(data: T): boolean {
    if (!this.head) return false; // Empty list — nothing to delete

    // Special case: the node to delete is the head
    if (this.head.data === data) {
      this.head = this.head.next; // Move head forward (old head gets garbage collected)
      this.size--;
      return true;
    }

    // Traverse, keeping track of the PREVIOUS node
    // We need previous because we must update previous.next to skip the deleted node
    let current = this.head;
    while (current.next !== null) {
      if (current.next.data === data) {
        // Found it! Skip over the node to delete it
        // Before: current → target → target.next
        // After:  current → target.next
        current.next = current.next.next;
        this.size--;
        return true;
      }
      current = current.next;
    }

    return false; // Data not found in list
  }

  // ── Search — O(n) ──────────────────────────────────────────────────────
  contains(data: T): boolean {
    let current = this.head;
    while (current !== null) {
      if (current.data === data) return true;
      current = current.next;
    }
    return false;
  }

  // ── Print the list (for debugging) ────────────────────────────────────
  print(): void {
    const elements: T[] = [];
    let current = this.head;
    while (current !== null) {
      elements.push(current.data);
      current = current.next;
    }
    console.log(elements.join(' → ') + ' → null');
  }

  // ── Reverse the linked list — O(n) — Classic interview question! ───────
  reverse(): void {
    let prev: ListNode<T> | null = null;
    let current: ListNode<T> | null = this.head;

    while (current !== null) {
      const nextNode = current.next; // Save next before overwriting
      current.next = prev;           // Reverse the pointer direction
      prev = current;                // Move prev forward
      current = nextNode;            // Move current forward
    }

    this.head = prev; // prev is now the new head (old tail)
  }
}

// ─── Usage ──────────────────────────────────────────────────────────────────

const list = new LinkedList<number>();
list.append(10);
list.append(20);
list.append(30);
list.prepend(5);
list.print();   // 5 → 10 → 20 → 30 → null

list.delete(20);
list.print();   // 5 → 10 → 30 → null

list.reverse();
list.print();   // 30 → 10 → 5 → null

console.log(list.contains(10)); // true
console.log(list.size);         // 3
```

---

### 3.3 Stacks

#### What Is a Stack?

A stack is a **Last In, First Out (LIFO)** data structure. The last item you put in is the first item you take out — exactly like a stack of plates. You always add and remove from the **top**.

```
     │ PUSH → adds here
     ▼
  ┌──────┐
  │  30  │ ← TOP (last in, first out)
  ├──────┤
  │  20  │
  ├──────┤
  │  10  │ ← BOTTOM (first in, last out)
  └──────┘
     ▲
     │ POP → removes from here
```

#### Real-World Uses
- **Browser back button**: Each page you visit is pushed; back pops the last page
- **Undo/Redo**: Ctrl+Z pops the last action off the undo stack
- **Function call stack**: When a function calls another, the call is pushed; when it returns, it's popped
- **Expression evaluation**: Compilers use stacks to evaluate `(3 + 4) * (2 - 1)`
- **Balanced parentheses**: Checking if brackets are properly matched

#### Implementation

```typescript
class Stack<T> {
  // We use a private array as the underlying storage.
  // The END of the array serves as the top of the stack.
  private items: T[] = [];

  // ── push — O(1) ─────────────────────────────────────────────────────────
  // Add an item to the top of the stack
  push(item: T): void {
    this.items.push(item); // Array.push adds to end → top of stack
  }

  // ── pop — O(1) ──────────────────────────────────────────────────────────
  // Remove and return the top item
  pop(): T | undefined {
    if (this.isEmpty()) {
      throw new Error("Stack underflow: Cannot pop from an empty stack");
    }
    return this.items.pop(); // Array.pop removes from end → top of stack
  }

  // ── peek — O(1) ─────────────────────────────────────────────────────────
  // Look at the top item WITHOUT removing it
  peek(): T | undefined {
    if (this.isEmpty()) return undefined;
    return this.items[this.items.length - 1]; // Last element = top
  }

  // ── isEmpty — O(1) ──────────────────────────────────────────────────────
  isEmpty(): boolean {
    return this.items.length === 0;
  }

  // ── size — O(1) ─────────────────────────────────────────────────────────
  size(): number {
    return this.items.length;
  }
}

// ─── Practical Application: Balanced Parentheses Checker ────────────────────
// Problem: Given a string of brackets, determine if they are all matched.
// "({[]})" → valid
// "([)]"   → invalid
// "{[]"    → invalid

function isBalanced(expression: string): boolean {
  const stack = new Stack<string>();

  // Map each closing bracket to its matching opening bracket
  const matchingOpen: Record<string, string> = {
    ')': '(',
    ']': '[',
    '}': '{',
  };

  for (const char of expression) {
    if ('([{'.includes(char)) {
      // Opening bracket — push it onto the stack
      stack.push(char);
    } else if (')]}'.includes(char)) {
      // Closing bracket — check if it matches the top of stack
      if (stack.isEmpty() || stack.peek() !== matchingOpen[char]) {
        return false; // Mismatch or stack is empty when it shouldn't be
      }
      stack.pop(); // Matched! Remove the opening bracket
    }
    // Ignore non-bracket characters (letters, spaces, numbers)
  }

  // If the stack is empty, all brackets were matched
  return stack.isEmpty();
}

console.log(isBalanced("({[]})")); // true
console.log(isBalanced("([)]"));   // false
console.log(isBalanced("{[]"));    // false
console.log(isBalanced(""));       // true (empty string is balanced)
```

---

### 3.4 Queues

#### What Is a Queue?

A queue is a **First In, First Out (FIFO)** data structure — like a queue at a supermarket checkout. The first person to join the line is the first to be served.

```
ENQUEUE → │ 30 │ 20 │ 10 │ → DEQUEUE
(add rear)  rear         front  (remove front)
```

#### Real-World Uses
- **Print queue**: Documents print in the order they were submitted
- **CPU task scheduling**: Processes wait in a queue to get CPU time
- **Breadth-First Search (BFS)**: Explores nodes level by level
- **Message queues**: Kafka, RabbitMQ — messages processed in order
- **Keyboard buffer**: Keystrokes are processed in the order they were pressed

#### Implementation

```typescript
class Queue<T> {
  // We use two pointers for O(1) enqueue AND dequeue.
  // A plain array with shift() would give O(n) dequeue — inefficient!
  private items: { [key: number]: T } = {}; // Object used as indexed storage
  private front: number = 0;  // Points to the front (oldest item)
  private rear: number = 0;   // Points to where next item will go

  // ── enqueue — O(1) ──────────────────────────────────────────────────────
  // Add to the rear of the queue
  enqueue(item: T): void {
    this.items[this.rear] = item; // Store item at rear index
    this.rear++;                   // Move rear forward
  }

  // ── dequeue — O(1) ──────────────────────────────────────────────────────
  // Remove and return from the front of the queue
  dequeue(): T | undefined {
    if (this.isEmpty()) {
      throw new Error("Queue underflow: Cannot dequeue from an empty queue");
    }
    const item = this.items[this.front]; // Grab front item
    delete this.items[this.front];        // Free memory
    this.front++;                          // Move front forward
    return item;
  }

  // ── peek — O(1) ─────────────────────────────────────────────────────────
  peek(): T | undefined {
    return this.items[this.front];
  }

  // ── isEmpty — O(1) ──────────────────────────────────────────────────────
  isEmpty(): boolean {
    return this.rear === this.front;
  }

  // ── size — O(1) ─────────────────────────────────────────────────────────
  size(): number {
    return this.rear - this.front;
  }
}

// ─── Usage ──────────────────────────────────────────────────────────────────

const printQueue = new Queue<string>();
printQueue.enqueue("Document A");
printQueue.enqueue("Document B");
printQueue.enqueue("Document C");

console.log(printQueue.dequeue()); // "Document A" — first in, first out
console.log(printQueue.dequeue()); // "Document B"
console.log(printQueue.peek());    // "Document C" — just looking, not removing
console.log(printQueue.size());    // 1
```

---

### 3.5 Hash Maps

#### What Is a Hash Map?

A hash map (also called a hash table or dictionary) stores **key-value pairs**. Given a key, you can retrieve its associated value in O(1) time on average.

**How does it work?** A **hash function** converts the key into an array index. The value is stored at that index. When you look up the key again, the hash function produces the same index, giving you instant access.

```
Key: "Alice"
         │
         ▼ hash("Alice") = 3
┌───┬───┬───┬───────────────┬───┬───┐
│   │   │   │ "Alice" → 92  │   │   │
└───┴───┴───┴───────────────┴───┴───┘
  0   1   2        3          4   5
```

#### When to Use a Hash Map
- Counting frequencies (how many times each word appears)
- Caching / memoization
- Looking up data by a unique key
- Removing duplicates
- Two-sum type problems (complement lookups)

#### TypeScript: `Map` vs Plain Objects

```typescript
// ─── Using a plain object as a hash map ─────────────────────────────────────
// Good for simple string keys, but has limitations (inherits prototype keys)

const wordCount: Record<string, number> = {};
const sentence = "the cat sat on the mat the cat";

for (const word of sentence.split(" ")) {
  // If word exists in our map, increment; otherwise, initialise to 1
  wordCount[word] = (wordCount[word] || 0) + 1;
}

console.log(wordCount);
// { the: 3, cat: 2, sat: 1, on: 1, mat: 1 }

// ─── Using TypeScript's Map class (preferred) ────────────────────────────────
// Allows ANY type as key (not just strings), preserves insertion order,
// and has a cleaner API.

const phoneBook = new Map<string, string>();

// Setting key-value pairs
phoneBook.set("Alice", "555-0101");
phoneBook.set("Bob", "555-0202");
phoneBook.set("Charlie", "555-0303");

// Getting a value by key — O(1)
console.log(phoneBook.get("Alice")); // "555-0101"
console.log(phoneBook.get("Dave"));  // undefined — key not found

// Checking for existence — O(1)
console.log(phoneBook.has("Bob"));   // true
console.log(phoneBook.has("Dave"));  // false

// Deleting a key — O(1)
phoneBook.delete("Charlie");

// Iterating
phoneBook.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});

// Size
console.log(phoneBook.size); // 2

// ─── Practical Application: Two Sum Problem ─────────────────────────────────
// Given an array of numbers and a target sum, find the INDICES of two numbers
// that add up to the target.
// Example: nums = [2, 7, 11, 15], target = 9 → Output: [0, 1] (2 + 7 = 9)

function twoSum(nums: number[], target: number): [number, number] | null {
  // Map stores: number → its index
  const seen = new Map<number, number>();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i]; // What number do we NEED to reach target?

    if (seen.has(complement)) {
      // We already saw the complement! Return both indices.
      return [seen.get(complement)!, i];
    }

    // Haven't found the complement yet — record this number and its index
    seen.set(nums[i], i);
  }

  return null; // No solution found
}

// Walk-through with [2, 7, 11, 15], target = 9:
// i=0: nums[0]=2, complement=7, seen={}, add 2→0. seen={2:0}
// i=1: nums[1]=7, complement=2, seen has 2! → return [0, 1]

console.log(twoSum([2, 7, 11, 15], 9));  // [0, 1]
console.log(twoSum([3, 2, 4], 6));        // [1, 2]
```

---

### 3.6 Sets

#### What Is a Set?

A **Set** stores a collection of **unique values** — no duplicates allowed. Like a hash map, it offers O(1) average time for add, delete, and lookup. Unlike a map, it has no keys — just values.

Think of it like a club membership list: each person can only be on the list once.

```typescript
// ─── TypeScript Set Basics ───────────────────────────────────────────────────

const uniqueVisitors = new Set<string>();

uniqueVisitors.add("user_1");
uniqueVisitors.add("user_2");
uniqueVisitors.add("user_1"); // Duplicate — silently ignored
uniqueVisitors.add("user_3");

console.log(uniqueVisitors.size); // 3 — not 4!

// Checking membership — O(1)
console.log(uniqueVisitors.has("user_2")); // true
console.log(uniqueVisitors.has("user_9")); // false

// Deleting — O(1)
uniqueVisitors.delete("user_2");

// Converting to array when needed
const visitorArray = [...uniqueVisitors]; // ["user_1", "user_3"]

// ─── Practical Application: Remove Duplicates from Array ─────────────────────

function removeDuplicates<T>(arr: T[]): T[] {
  // Set constructor accepts an iterable — all duplicates are automatically dropped
  return [...new Set(arr)];
}

console.log(removeDuplicates([1, 2, 2, 3, 4, 4, 5])); // [1, 2, 3, 4, 5]
console.log(removeDuplicates(["a", "b", "a", "c"]));  // ["a", "b", "c"]

// ─── Set Operations ──────────────────────────────────────────────────────────

function intersection<T>(setA: Set<T>, setB: Set<T>): Set<T> {
  // Elements present in BOTH sets
  const result = new Set<T>();
  for (const item of setA) {
    if (setB.has(item)) result.add(item);
  }
  return result;
}

function union<T>(setA: Set<T>, setB: Set<T>): Set<T> {
  // All elements from EITHER set (no duplicates)
  return new Set([...setA, ...setB]);
}

function difference<T>(setA: Set<T>, setB: Set<T>): Set<T> {
  // Elements in setA but NOT in setB
  const result = new Set<T>();
  for (const item of setA) {
    if (!setB.has(item)) result.add(item);
  }
  return result;
}

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([3, 4, 5, 6]);

console.log(intersection(setA, setB)); // Set {3, 4}
console.log(union(setA, setB));        // Set {1, 2, 3, 4, 5, 6}
console.log(difference(setA, setB));   // Set {1, 2}
```

---

### 3.7 Trees

#### What Is a Tree?

A **tree** is a hierarchical data structure made up of **nodes**, where each node has:
- A **value**
- Zero or more **children** (subtrees)

Unlike linked lists (linear), trees **branch out** — they represent hierarchical relationships.

```
        Terminology:
            1          ← root (no parent)
           / \
          2   3        ← internal nodes
         / \   \
        4   5   6      ← leaf nodes (no children)

- root: node with no parent (node 1)
- leaf: node with no children (4, 5, 6)
- edge: connection between parent and child
- depth: distance from root
- height: distance from node to deepest leaf
```

#### Real-World Uses
- **File systems**: Folders contain sub-folders and files
- **HTML DOM**: `<html>` contains `<body>` which contains `<div>` etc.
- **Organisation charts**: CEO → Managers → Employees
- **Decision trees**: Used in machine learning and game AI
- **BST**: Used in database indexing

#### Binary Trees

A **binary tree** is a tree where each node has **at most two children** — a `left` and a `right` child.

#### Binary Search Trees (BST)

A **BST** is a binary tree with one powerful property:
> For every node N:  
> All values in the **left subtree** are **less than** N  
> All values in the **right subtree** are **greater than** N

This property allows O(log n) search, insertion, and deletion on a **balanced** BST.

```
         8
        / \
       3   10
      / \    \
     1   6    14
        / \   /
       4   7 13
```

Search for 7:
- Start at 8 — 7 < 8, go left
- At 3 — 7 > 3, go right
- At 6 — 7 > 6, go right
- At 7 — found! (3 steps, not 8)

#### Implementation

```typescript
// ─── Tree Node ───────────────────────────────────────────────────────────────

class TreeNode {
  value: number;
  left: TreeNode | null;
  right: TreeNode | null;

  constructor(value: number) {
    this.value = value;
    this.left = null;  // No left child yet
    this.right = null; // No right child yet
  }
}

// ─── Binary Search Tree ──────────────────────────────────────────────────────

class BinarySearchTree {
  root: TreeNode | null = null; // Empty tree has no root

  // ── Insert — O(log n) average, O(n) worst (unbalanced tree) ────────────
  insert(value: number): void {
    const newNode = new TreeNode(value);

    if (!this.root) {
      this.root = newNode; // First node becomes the root
      return;
    }

    // Navigate the tree to find the correct position
    let current = this.root;
    while (true) {
      if (value === current.value) return; // BST typically ignores duplicates

      if (value < current.value) {
        // Go LEFT
        if (current.left === null) {
          current.left = newNode; // Found the empty spot — insert here
          return;
        }
        current = current.left; // Keep going left
      } else {
        // Go RIGHT
        if (current.right === null) {
          current.right = newNode; // Found the empty spot — insert here
          return;
        }
        current = current.right; // Keep going right
      }
    }
  }

  // ── Search — O(log n) average ───────────────────────────────────────────
  contains(value: number): boolean {
    let current = this.root;

    while (current !== null) {
      if (value === current.value) return true;  // Found!
      if (value < current.value) {
        current = current.left;  // Search left subtree
      } else {
        current = current.right; // Search right subtree
      }
    }

    return false; // Reached a null — value not in tree
  }

  // ── In-Order Traversal — visits nodes in SORTED order for a BST ─────────
  // Left → Root → Right
  inOrderTraversal(node: TreeNode | null = this.root, result: number[] = []): number[] {
    if (node === null) return result; // Base case: nothing to visit

    this.inOrderTraversal(node.left, result);  // Visit entire left subtree first
    result.push(node.value);                   // Visit current node
    this.inOrderTraversal(node.right, result); // Visit entire right subtree

    return result;
  }

  // ── Find Minimum — go all the way LEFT ──────────────────────────────────
  findMin(): number | null {
    if (!this.root) return null;
    let current = this.root;
    while (current.left !== null) {
      current = current.left;
    }
    return current.value;
  }

  // ── Find Maximum — go all the way RIGHT ─────────────────────────────────
  findMax(): number | null {
    if (!this.root) return null;
    let current = this.root;
    while (current.right !== null) {
      current = current.right;
    }
    return current.value;
  }

  // ── Height of the Tree — O(n) ───────────────────────────────────────────
  // Height = longest path from root to a leaf
  height(node: TreeNode | null = this.root): number {
    if (node === null) return -1; // Convention: empty tree has height -1

    const leftHeight = this.height(node.left);   // Height of left subtree
    const rightHeight = this.height(node.right); // Height of right subtree

    // Height of current node = 1 + height of the taller subtree
    return 1 + Math.max(leftHeight, rightHeight);
  }
}

// ─── Usage ──────────────────────────────────────────────────────────────────

const bst = new BinarySearchTree();
[8, 3, 10, 1, 6, 14, 4, 7, 13].forEach(v => bst.insert(v));

console.log(bst.inOrderTraversal()); // [1, 3, 4, 6, 7, 8, 10, 13, 14] — sorted!
console.log(bst.contains(7));         // true
console.log(bst.contains(9));         // false
console.log(bst.findMin());           // 1
console.log(bst.findMax());           // 14
console.log(bst.height());            // 3
```

---

### 3.8 Graphs

#### What Is a Graph?

A **graph** is a collection of **nodes** (also called vertices) connected by **edges**. Unlike trees, graphs have no strict hierarchical structure — any node can connect to any other node, and there can be cycles.

```
   A ── B ── E
   │    │
   C ── D
```

#### Types of Graphs

| Type        | Description                              | Example                    |
|:------------|:-----------------------------------------|:---------------------------|
| Undirected  | Edges have no direction                  | Facebook friendships       |
| Directed    | Edges have a direction (A → B ≠ B → A)  | Twitter follows, web links |
| Weighted    | Edges have a numeric weight              | Road distances, flight costs |
| Unweighted  | All edges are equal                      | Simple connections         |
| Cyclic      | Contains at least one cycle              | Most social networks       |
| Acyclic     | No cycles (DAG: Directed Acyclic Graph)  | Git commit history         |

#### Graph Representations

**Adjacency List** — Most common. Stores each node's list of neighbours.  
**Adjacency Matrix** — A 2D grid where `matrix[i][j] = 1` means edge from i to j.

Adjacency lists are preferred for sparse graphs (fewer edges). Matrices suit dense graphs.

```typescript
// ─── Adjacency List Graph ────────────────────────────────────────────────────

class Graph {
  // Map: node → list of neighbours
  private adjacencyList: Map<string, string[]>;

  constructor() {
    this.adjacencyList = new Map();
  }

  // ── Add a vertex (node) ──────────────────────────────────────────────────
  addVertex(vertex: string): void {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, []); // New node starts with no neighbours
    }
  }

  // ── Add an edge (undirected — both nodes point to each other) ────────────
  addEdge(vertex1: string, vertex2: string): void {
    this.addVertex(vertex1); // Ensure both vertices exist
    this.addVertex(vertex2);

    this.adjacencyList.get(vertex1)!.push(vertex2); // v1 connects to v2
    this.adjacencyList.get(vertex2)!.push(vertex1); // v2 connects to v1 (undirected)
  }

  // ── Get neighbours of a node ─────────────────────────────────────────────
  getNeighbors(vertex: string): string[] {
    return this.adjacencyList.get(vertex) || [];
  }

  // ── Print the graph ──────────────────────────────────────────────────────
  print(): void {
    this.adjacencyList.forEach((neighbors, vertex) => {
      console.log(`${vertex} → [${neighbors.join(", ")}]`);
    });
  }
}

// ─── Usage ──────────────────────────────────────────────────────────────────

const graph = new Graph();
graph.addEdge("A", "B");
graph.addEdge("A", "C");
graph.addEdge("B", "D");
graph.addEdge("B", "E");
graph.addEdge("C", "D");

graph.print();
// A → [B, C]
// B → [A, D, E]
// C → [A, D]
// D → [B, C]
// E → [B]
```

---

## 4. Algorithms

---

### 4.1 Searching

#### Linear Search

The simplest search — check every element one by one until found.

```typescript
// O(n) time, O(1) space
// Works on ANY array (sorted or not)

function linearSearch<T>(arr: T[], target: T): number {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i; // Return the index where target was found
    }
  }
  return -1; // Target not in array
}

// Step-by-step example: search for 30 in [10, 50, 30, 70, 20]
// i=0: arr[0]=10, 10≠30 → continue
// i=1: arr[1]=50, 50≠30 → continue
// i=2: arr[2]=30, 30=30 → return 2 ✓

console.log(linearSearch([10, 50, 30, 70, 20], 30)); // 2
console.log(linearSearch([10, 50, 30, 70, 20], 99)); // -1
```

#### Binary Search

Efficient search on a **sorted** array by repeatedly halving the search space.

```typescript
// O(log n) time, O(1) space
// REQUIRES sorted array — this is the key precondition!

function binarySearch(arr: number[], target: number): number {
  let left = 0;                // Left boundary of search range
  let right = arr.length - 1; // Right boundary of search range

  while (left <= right) {
    // Calculate midpoint (this avoids integer overflow)
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;       // 🎯 Direct hit!
    } else if (arr[mid] < target) {
      left = mid + 1;   // Target is in right half → move left boundary up
    } else {
      right = mid - 1;  // Target is in left half → move right boundary down
    }
  }

  return -1; // Target not found — search range exhausted
}

// Step-by-step: search for 23 in [1, 5, 8, 12, 16, 23, 38, 56, 72, 91]
// left=0, right=9 → mid=4 → arr[4]=16 < 23 → left=5
// left=5, right=9 → mid=7 → arr[7]=56 > 23 → right=6
// left=5, right=6 → mid=5 → arr[5]=23 = 23 → return 5 ✓

const sorted = [1, 5, 8, 12, 16, 23, 38, 56, 72, 91];
console.log(binarySearch(sorted, 23)); // 5
console.log(binarySearch(sorted, 50)); // -1
```

---

### 4.2 Sorting

Sorting is one of the most studied problems in CS. Understanding sorting algorithms teaches fundamental concepts like divide-and-conquer, comparisons, and stability.

#### Bubble Sort

**Idea**: Repeatedly compare adjacent elements and swap if out of order. Larger elements "bubble up" to their correct position.

```typescript
// O(n²) time, O(1) space — Simple but slow; mostly educational

function bubbleSort(arr: number[]): number[] {
  const n = arr.length;
  const result = [...arr]; // Don't mutate the original

  // Outer loop: each pass guarantees the LARGEST unsorted element is placed
  for (let i = 0; i < n - 1; i++) {
    let swapped = false; // Optimisation: if no swaps, array is already sorted

    // Inner loop: compare adjacent pairs
    // After each outer iteration, the last (i) elements are already sorted
    for (let j = 0; j < n - 1 - i; j++) {
      if (result[j] > result[j + 1]) {
        // Swap — this pair is out of order
        [result[j], result[j + 1]] = [result[j + 1], result[j]];
        swapped = true;
      }
    }

    if (!swapped) break; // Array is already sorted — no need to continue!
  }

  return result;
}

// Pass-by-pass trace on [64, 34, 25, 12]:
// Pass 1: [34,25,12,64] — 64 bubbles to end
// Pass 2: [25,12,34,64] — 34 settles
// Pass 3: [12,25,34,64] — done!

console.log(bubbleSort([64, 34, 25, 12, 22, 11, 90]));
// [11, 12, 22, 25, 34, 64, 90]
```

#### Selection Sort

**Idea**: Find the minimum element from the unsorted portion and swap it into its correct position. "Select" the smallest each time.

```typescript
// O(n²) time, O(1) space — Makes exactly n-1 swaps (fewer than bubble sort)

function selectionSort(arr: number[]): number[] {
  const result = [...arr];
  const n = result.length;

  for (let i = 0; i < n - 1; i++) {
    // Assume current position has the minimum
    let minIndex = i;

    // Find the ACTUAL minimum in the remaining unsorted portion
    for (let j = i + 1; j < n; j++) {
      if (result[j] < result[minIndex]) {
        minIndex = j; // Found a new minimum
      }
    }

    // Swap the minimum with the current position (only if needed)
    if (minIndex !== i) {
      [result[i], result[minIndex]] = [result[minIndex], result[i]];
    }
    // Now result[0..i] is sorted ✓
  }

  return result;
}

console.log(selectionSort([64, 25, 12, 22, 11]));
// [11, 12, 22, 25, 64]
```

#### Insertion Sort

**Idea**: Build the sorted array one element at a time. For each new element, insert it into its correct position among the already-sorted elements.

Like sorting a hand of playing cards — you pick up one card at a time and slide it into the right spot.

```typescript
// O(n²) worst/average, O(n) best (already sorted) — Excellent for small or nearly-sorted data

function insertionSort(arr: number[]): number[] {
  const result = [...arr];
  const n = result.length;

  // Start from index 1 — the first element is trivially "sorted"
  for (let i = 1; i < n; i++) {
    const current = result[i]; // The element we are inserting
    let j = i - 1;             // Start comparing with the element before current

    // Shift elements that are greater than 'current' one position to the right
    // This makes room for 'current' to be inserted in the correct position
    while (j >= 0 && result[j] > current) {
      result[j + 1] = result[j]; // Shift right
      j--;                        // Move left
    }

    result[j + 1] = current; // Place current in its correct position
  }

  return result;
}

// Trace on [5, 3, 8, 1]:
// i=1: current=3, shift 5 right → [5,5,8,1], place 3 → [3,5,8,1]
// i=2: current=8, 8>5? no → [3,5,8,1]
// i=3: current=1, shift 8,5,3 right → place 1 → [1,3,5,8]

console.log(insertionSort([5, 3, 8, 1, 9, 2]));
// [1, 2, 3, 5, 8, 9]
```

#### Merge Sort

**Idea**: Divide the array in half, recursively sort each half, then **merge** the two sorted halves. Classic **divide and conquer**.

This is one of the most important sorting algorithms — it is efficient and stable.

```typescript
// O(n log n) time always, O(n) space — The gold standard for stable sorting

function mergeSort(arr: number[]): number[] {
  // Base case: an array of 0 or 1 elements is already sorted
  if (arr.length <= 1) return arr;

  // ─ Divide ──────────────────────────────────────────────────────────────
  const mid = Math.floor(arr.length / 2);
  const left = arr.slice(0, mid);  // Left half
  const right = arr.slice(mid);    // Right half

  // ─ Conquer ─────────────────────────────────────────────────────────────
  // Recursively sort each half
  const sortedLeft = mergeSort(left);
  const sortedRight = mergeSort(right);

  // ─ Combine ─────────────────────────────────────────────────────────────
  return merge(sortedLeft, sortedRight);
}

// Merge two sorted arrays into one sorted array
function merge(left: number[], right: number[]): number[] {
  const result: number[] = [];
  let l = 0; // Pointer into left array
  let r = 0; // Pointer into right array

  // Compare front elements of each array, take the smaller one
  while (l < left.length && r < right.length) {
    if (left[l] <= right[r]) {
      result.push(left[l]); // Left is smaller — take it
      l++;
    } else {
      result.push(right[r]); // Right is smaller — take it
      r++;
    }
  }

  // Append any remaining elements (one array may finish before the other)
  while (l < left.length) result.push(left[l++]);
  while (r < right.length) result.push(right[r++]);

  return result;
}

// Execution tree for [38, 27, 43, 3]:
//            [38,27,43,3]
//           /             \
//      [38,27]          [43,3]
//      /    \           /    \
//   [38]   [27]      [43]   [3]
//      \   /            \  /
//     [27,38]          [3,43]
//            \        /
//           [3,27,38,43]

console.log(mergeSort([38, 27, 43, 3, 9, 82, 10]));
// [3, 9, 10, 27, 38, 43, 82]
```

#### Quick Sort

**Idea**: Choose a **pivot** element, then partition the array so all elements smaller than the pivot go left and all larger go right. Recursively sort each partition.

```typescript
// O(n log n) average, O(n²) worst (bad pivot selection)
// O(log n) space (call stack) average
// In practice, often faster than merge sort due to better cache performance

function quickSort(arr: number[], low: number = 0, high: number = arr.length - 1): number[] {
  const result = [...arr];

  function partition(arr: number[], low: number, high: number): number {
    const pivot = arr[high]; // Choose LAST element as pivot (simple strategy)
    let i = low - 1;          // i tracks the boundary of smaller elements

    for (let j = low; j < high; j++) {
      if (arr[j] <= pivot) {
        i++;
        // Swap arr[j] to the "smaller" side
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
    }

    // Place pivot in its correct final position
    [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];
    return i + 1; // Return the pivot's final index
  }

  function sort(arr: number[], low: number, high: number): void {
    if (low >= high) return; // Base case: 0 or 1 element — already sorted

    const pivotIndex = partition(arr, low, high);

    // Recursively sort elements BEFORE and AFTER the pivot
    // The pivot itself is already in its final sorted position!
    sort(arr, low, pivotIndex - 1);   // Sort left partition
    sort(arr, pivotIndex + 1, high);  // Sort right partition
  }

  sort(result, low, high);
  return result;
}

console.log(quickSort([10, 80, 30, 90, 40, 50, 70]));
// [10, 30, 40, 50, 70, 80, 90]
```

#### Sorting Algorithm Comparison

| Algorithm      | Best     | Average   | Worst    | Space  | Stable? |
|:---------------|:---------|:----------|:---------|:-------|:--------|
| Bubble Sort    | O(n)     | O(n²)     | O(n²)    | O(1)   | ✅ Yes   |
| Selection Sort | O(n²)    | O(n²)     | O(n²)    | O(1)   | ❌ No    |
| Insertion Sort | O(n)     | O(n²)     | O(n²)    | O(1)   | ✅ Yes   |
| Merge Sort     | O(n logn)| O(n log n)| O(n logn)| O(n)   | ✅ Yes   |
| Quick Sort     | O(n logn)| O(n log n)| O(n²)    | O(logn)| ❌ No    |

> **Stable** means equal elements maintain their original relative order after sorting. This matters when you sort objects by one field and want to preserve a previous sort on another field.

---

### 4.3 Recursion

#### What Is Recursion?

Recursion is when a **function calls itself** to solve a smaller version of the same problem. Every recursive solution has two essential parts:

1. **Base case**: The simplest possible input where we can answer directly (stops the recursion)
2. **Recursive case**: Break the problem into smaller pieces and call yourself

Think of it like Russian nesting dolls: each doll contains a smaller version of itself, until you reach the tiniest doll that contains nothing (base case).

#### The Call Stack

When a function calls itself, each call is pushed onto the **call stack** and waits until the inner call returns. Understanding this is key to understanding recursion.

```typescript
// ─── Example 1: Factorial ────────────────────────────────────────────────────
// 5! = 5 × 4 × 3 × 2 × 1 = 120
// Notice: 5! = 5 × 4! and 4! = 4 × 3! and so on...

function factorial(n: number): number {
  // Base case: 0! = 1 and 1! = 1 — stop recursing here
  if (n <= 1) return 1;

  // Recursive case: n! = n × (n-1)!
  return n * factorial(n - 1);
}

// Call stack visualisation for factorial(4):
// factorial(4)
//   → 4 * factorial(3)
//          → 3 * factorial(2)
//                   → 2 * factorial(1)
//                            → 1           (base case — returns 1)
//                   → 2 * 1 = 2            (returns 2)
//          → 3 * 2 = 6                     (returns 6)
//   → 4 * 6 = 24                           (returns 24)

console.log(factorial(5)); // 120
console.log(factorial(0)); // 1

// ─── Example 2: Fibonacci ────────────────────────────────────────────────────
// Sequence: 0, 1, 1, 2, 3, 5, 8, 13, 21...
// Each number is the sum of the two before it.
// fib(n) = fib(n-1) + fib(n-2)

// Naive recursive — O(2ⁿ) — VERY slow due to repeated calculations
function fibNaive(n: number): number {
  if (n <= 1) return n;              // fib(0)=0, fib(1)=1
  return fibNaive(n - 1) + fibNaive(n - 2); // Redundant calculations!
}

// Why is it slow? fib(5) calculates fib(3) TWICE:
// fib(5) = fib(4) + fib(3)
// fib(4) = fib(3) + fib(2)  ← fib(3) calculated here too!

// ─── Memoization — O(n) time, O(n) space ────────────────────────────────────
// Cache results to avoid recalculating

function fibMemo(n: number, memo: Map<number, number> = new Map()): number {
  if (n <= 1) return n;

  // Check if we already computed this value
  if (memo.has(n)) return memo.get(n)!;

  // Compute and CACHE the result before returning
  const result = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
  memo.set(n, result);
  return result;
}

console.log(fibMemo(10));  // 55
console.log(fibMemo(50));  // 12586269025 — fast! (naive would freeze)

// ─── Example 3: Power of Recursion — Flatten a Nested Array ─────────────────
// Input: [1, [2, [3, [4]], 5]] → Output: [1, 2, 3, 4, 5]

function flatten(arr: (number | any[])[]): number[] {
  const result: number[] = [];

  for (const item of arr) {
    if (Array.isArray(item)) {
      // If item is an array, recursively flatten it and add all its elements
      result.push(...flatten(item));
    } else {
      // If item is a number, add it directly
      result.push(item);
    }
  }

  return result;
}

console.log(flatten([1, [2, [3, [4]], 5]])); // [1, 2, 3, 4, 5]

// ─── Example 4: Binary Search — Recursive Version ───────────────────────────

function binarySearchRecursive(
  arr: number[],
  target: number,
  left: number = 0,
  right: number = arr.length - 1
): number {
  // Base case: search space is exhausted
  if (left > right) return -1;

  const mid = Math.floor((left + right) / 2);

  if (arr[mid] === target) return mid;

  if (arr[mid] < target) {
    // Recurse on right half — passing updated left boundary
    return binarySearchRecursive(arr, target, mid + 1, right);
  } else {
    // Recurse on left half — passing updated right boundary
    return binarySearchRecursive(arr, target, left, mid - 1);
  }
}

// ─── When NOT to use Recursion ──────────────────────────────────────────────
// 1. Very deep recursion → stack overflow (each call uses stack space)
// 2. When an iterative solution is just as clear
// A common rule: if recursion depth could exceed ~10,000, use iteration
```

> **Mental model for recursion**: Trust that the smaller version of your function works correctly. Your job is just to handle the current case using that smaller result. Don't try to trace every call mentally — it becomes overwhelming.

---

### 4.4 Traversals (DFS & BFS)

Graph and tree traversal algorithms answer: **"How do I visit every node exactly once?"**

#### Depth-First Search (DFS)

**Go as deep as possible** along one path before backtracking. Like exploring a maze by always turning left — you eventually cover everything by backtracking when you hit dead ends.

```
Start at A:
A → B → D (dead end, backtrack)
    → E (dead end, backtrack)
→ C → F (dead end, backtrack)
    → G

Visited order: A, B, D, E, C, F, G
```

```typescript
// ─── DFS on a Graph (Iterative using Stack) ──────────────────────────────────

function dfsIterative(graph: Map<string, string[]>, startVertex: string): string[] {
  const visited = new Set<string>(); // Track visited nodes to avoid cycles
  const stack: string[] = [startVertex]; // Use a stack (LIFO) — DFS property
  const traversalOrder: string[] = [];

  while (stack.length > 0) {
    const vertex = stack.pop()!; // Take from TOP of stack

    if (visited.has(vertex)) continue; // Already visited — skip

    visited.add(vertex);
    traversalOrder.push(vertex);

    // Push all unvisited neighbours onto the stack
    const neighbors = graph.get(vertex) || [];
    for (const neighbor of neighbors) {
      if (!visited.has(neighbor)) {
        stack.push(neighbor); // Will be explored AFTER we finish deeper paths
      }
    }
  }

  return traversalOrder;
}

// ─── DFS on a Graph (Recursive) ─────────────────────────────────────────────

function dfsRecursive(
  graph: Map<string, string[]>,
  vertex: string,
  visited: Set<string> = new Set(),
  result: string[] = []
): string[] {
  visited.add(vertex);     // Mark as visited
  result.push(vertex);     // Record this node

  const neighbors = graph.get(vertex) || [];
  for (const neighbor of neighbors) {
    if (!visited.has(neighbor)) {
      dfsRecursive(graph, neighbor, visited, result); // Go deeper first
    }
  }

  return result;
}

// ─── DFS on a Binary Tree ────────────────────────────────────────────────────
// Three types of tree DFS, differing only in WHEN you visit the root:

// Pre-order: Root → Left → Right (used to copy/serialise a tree)
function preOrder(node: TreeNode | null, result: number[] = []): number[] {
  if (!node) return result;
  result.push(node.value);        // Visit ROOT first
  preOrder(node.left, result);    // Then left subtree
  preOrder(node.right, result);   // Then right subtree
  return result;
}

// In-order: Left → Root → Right (gives SORTED output for BSTs)
function inOrder(node: TreeNode | null, result: number[] = []): number[] {
  if (!node) return result;
  inOrder(node.left, result);     // Left subtree first
  result.push(node.value);        // Visit ROOT in the middle
  inOrder(node.right, result);    // Then right subtree
  return result;
}

// Post-order: Left → Right → Root (used to delete a tree — children before parent)
function postOrder(node: TreeNode | null, result: number[] = []): number[] {
  if (!node) return result;
  postOrder(node.left, result);   // Left subtree first
  postOrder(node.right, result);  // Right subtree
  result.push(node.value);        // Visit ROOT last
  return result;
}
```

#### Breadth-First Search (BFS)

**Visit all nodes at the current depth before going deeper**. Like ripples spreading out from a stone dropped in water — you explore all neighbours before their neighbours.

```
Start at A (depth 0):
Level 0: A
Level 1: B, C
Level 2: D, E, F, G

Visited order: A, B, C, D, E, F, G
```

```typescript
// ─── BFS on a Graph ─────────────────────────────────────────────────────────
// BFS uses a QUEUE (FIFO) — this ensures we visit nodes level by level

function bfsGraph(graph: Map<string, string[]>, startVertex: string): string[] {
  const visited = new Set<string>();
  const queue = new Queue<string>(); // Our Queue from earlier!
  const traversalOrder: string[] = [];

  visited.add(startVertex);
  queue.enqueue(startVertex);

  while (!queue.isEmpty()) {
    const vertex = queue.dequeue()!; // Take from FRONT (oldest unprocessed)
    traversalOrder.push(vertex);

    const neighbors = graph.get(vertex) || [];
    for (const neighbor of neighbors) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);   // Mark as visited WHEN ENQUEUED (not when dequeued)
        queue.enqueue(neighbor); // Add to back of queue — process later
      }
    }
  }

  return traversalOrder;
}

// ─── BFS on a Tree — Level Order Traversal ─────────────────────────────────
// Very common interview question!

function levelOrder(root: TreeNode | null): number[][] {
  if (!root) return [];

  const result: number[][] = [];
  const queue: TreeNode[] = [root];

  while (queue.length > 0) {
    const levelSize = queue.length; // How many nodes are at this level?
    const currentLevel: number[] = [];

    // Process ALL nodes at the current level
    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift()!; // Dequeue from front
      currentLevel.push(node.value);

      // Enqueue children (they belong to the NEXT level)
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    result.push(currentLevel); // Save this level's values
  }

  return result;
}

// ─── DFS vs BFS — When to Use Which? ────────────────────────────────────────

// Use DFS when:
// - You want to explore all paths (e.g., solve a maze)
// - You need to detect cycles
// - You are solving path-finding in trees (in-order, pre-order, etc.)
// - Memory is a concern (DFS only keeps the current path in memory)
// - You suspect the answer is deep in the tree/graph

// Use BFS when:
// - You want the SHORTEST path in an unweighted graph
// - You want level-by-level traversal
// - The target is likely near the start
// - You are solving "minimum steps" problems

// ─── BFS Practical Application: Shortest Path ───────────────────────────────

function shortestPath(
  graph: Map<string, string[]>,
  start: string,
  end: string
): string[] | null {
  if (start === end) return [start];

  const visited = new Set<string>();
  // Queue stores: [current node, path taken to reach it]
  const queue: [string, string[]][] = [[start, [start]]];
  visited.add(start);

  while (queue.length > 0) {
    const [vertex, path] = queue.shift()!;

    for (const neighbor of (graph.get(vertex) || [])) {
      if (neighbor === end) {
        return [...path, neighbor]; // Found the end! Return the full path.
      }

      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push([neighbor, [...path, neighbor]]); // Track path to each node
      }
    }
  }

  return null; // No path exists
}

// Build a graph and find shortest path
const cityGraph = new Map<string, string[]>([
  ["A", ["B", "C"]],
  ["B", ["A", "D", "E"]],
  ["C", ["A", "F"]],
  ["D", ["B"]],
  ["E", ["B", "F"]],
  ["F", ["C", "E"]],
]);

console.log(shortestPath(cityGraph, "A", "F")); // ["A", "C", "F"]
```

---

## Summary

Congratulations on completing this tutorial! Here is a quick reference of everything covered:

| Concept             | Key Insight                                             | Best For                          |
|:--------------------|:--------------------------------------------------------|:----------------------------------|
| Array               | O(1) access by index, O(n) insert/delete               | Fixed-size data, random access    |
| Linked List         | O(1) insert at head, O(n) search                       | Frequent insertions at front      |
| Stack               | LIFO — last in, first out                              | Undo, parsing, DFS                |
| Queue               | FIFO — first in, first out                             | BFS, task scheduling              |
| Hash Map            | O(1) average lookup, insert, delete                    | Key-value storage, frequency count|
| Set                 | O(1) average, unique values only                       | Deduplication, membership test    |
| BST                 | O(log n) ops on balanced tree                          | Sorted data, range queries        |
| Graph               | Nodes + edges, models relationships                    | Networks, paths, connectivity     |
| Binary Search       | O(log n) on sorted array                               | Fast lookup in sorted data        |
| Merge Sort          | O(n log n), stable, divide & conquer                   | General sorting, stable required  |
| Quick Sort          | O(n log n) average, in-place                           | General sorting in practice       |
| Recursion           | Function calls itself with smaller input               | Trees, divide & conquer, backtrack|
| DFS                 | Go deep first, uses stack                              | Paths, cycles, tree traversal     |
| BFS                 | Go wide first, uses queue                              | Shortest path, level order        |

---

*Keep practising! The only way to truly internalise DSA is to solve problems regularly. Move on to `exercises.md` to test your understanding.*
