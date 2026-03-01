# TypeScript Practice & Exercise Sheet
### For JavaScript Developers Learning TypeScript

> **How to use this sheet:** Work through exercises in order — each section builds on the last. Try to solve each exercise yourself before looking at the hint. The project challenges at the end tie everything together.

---

## Section 1: Type Basics

### Exercise 1.1 — Annotate the Variables

Add explicit type annotations to the following variables. Some are straightforward, some are tricky.

```ts
// Add type annotations to each variable

let firstName = "Jordan";
let score = 99.5;
let isLoggedIn = false;
let sessionId = null;
let pageCount = undefined;
let bigNumber = 9007199254740991n;

// Challenge: What type should this be?
let mystery; // declared but not assigned yet
```

**Expected learning:** Primitive types, `null`, `undefined`, `bigint`, `any` vs explicit types.

---

### Exercise 1.2 — Fix the Type Errors

The following code has type errors. Identify and fix all of them.

```ts
let age: number = "thirty";
let isActive: boolean = 1;
let username: string = null;
let count: number = undefined;

function getAge(): number {
  return "I am 25 years old";
}
```

**Hint:** Think about `strictNullChecks`. How would you allow `null` in a type?

---

### Exercise 1.3 — `unknown` vs `any`

Rewrite the following `any`-typed function to use `unknown` safely.

```ts
// ❌ Using any — unsafe
function processData(data: any) {
  console.log(data.toUpperCase()); // could crash at runtime
  return data.length;
}

// ✅ Your task: Rewrite using unknown with proper type guards
function processDataSafely(data: unknown) {
  // Your code here
}
```

---

## Section 2: Functions

### Exercise 2.1 — Type the Functions

Add full type annotations (parameters + return types) to these functions:

```ts
// 1. Returns the full name from first and last
function getFullName(first, last) {
  return `${first} ${last}`;
}

// 2. Calculates tip — tip percent is optional (default 18%)
function calculateTip(billAmount, tipPercent) {
  return billAmount * ((tipPercent ?? 18) / 100);
}

// 3. Takes any number of scores, returns their average
function average(...scores) {
  return scores.reduce((sum, s) => sum + s, 0) / scores.length;
}

// 4. A callback-style function — cb receives an error or a result string
function fetchData(url, cb) {
  // implementation not important
}
```

---

### Exercise 2.2 — Function Types

Define a type alias for each of the following function signatures, then write a function that matches it.

```ts
// 1. Takes two numbers, returns a boolean
type Comparator = /* your type here */;

// 2. Takes a string, returns nothing
type Logger = /* your type here */;

// 3. Takes an array of numbers and a callback that transforms each number, returns a number array
type Transformer = /* your type here */;

// Now write one function that matches each type alias
```

---

### Exercise 2.3 — Overloads

Write a function `formatValue` with overloads that:
- When passed a `number`, returns a string formatted as currency (e.g. `"$42.00"`)
- When passed a `string`, returns the string trimmed and capitalized
- When passed a `boolean`, returns `"Yes"` or `"No"`

```ts
// Write your overload signatures and implementation here
```

---

## Section 3: Objects & Interfaces

### Exercise 3.1 — Define the Interface

A user-management system needs these object shapes. Define an interface for each:

```ts
// 1. A Product in an e-commerce store
//    - id (number, read-only)
//    - name (string)
//    - price (number)
//    - description (optional string)
//    - category ("electronics" | "clothing" | "food" | "books")
//    - inStock (boolean)

interface Product {
  // fill this in
}

// 2. An Address
//    - street, city, country (all strings)
//    - state (optional string)
//    - zipCode (string)

interface Address {
  // fill this in
}

// 3. A Customer that has a name, email, an Address, and a list of Products
interface Customer {
  // fill this in
}
```

---

### Exercise 3.2 — Extend Interfaces

```ts
interface Vehicle {
  make: string;
  model: string;
  year: number;
  startEngine(): void;
}

// 1. Create an ElectricVehicle interface that extends Vehicle
//    and adds: batteryCapacityKwh (number), chargeLevel (number 0-100), charge() method

// 2. Create a Truck interface that extends Vehicle
//    and adds: payloadCapacityKg (number), numAxles (number)

// 3. Write a function that accepts any Vehicle and logs its make/model/year
```

---

### Exercise 3.3 — Index Signatures

Create an interface `ConfigStore` that:
- Has a required property `version` (number)
- Allows any additional `string` keys with `string | number | boolean` values

Then write a function `getConfig(store: ConfigStore, key: string)` that returns the value or `undefined`.

```ts
// Your solution here
```

---

## Section 4: Union & Intersection Types

### Exercise 4.1 — Union Types

```ts
// 1. Create a type ID that can be a string or number
// 2. Create a type StringOrStringArray that is string | string[]
// 3. Write a function normalize(input: StringOrStringArray) that always returns string[]

// 4. Create a union type for a traffic light: "red" | "yellow" | "green"
//    Write a function getAction(light) that returns what a driver should do

// 5. Create a union type Padding that is:
//    - a number (all sides equal)
//    - { top: number, bottom: number, left: number, right: number }
//    Write a function getPaddingCSS(p: Padding): string
```

---

### Exercise 4.2 — Discriminated Unions

Model the states of an async data fetch using discriminated unions:

```ts
// A fetch can be in one of three states:
// - Idle: hasn't started
// - Loading: in progress
// - Success: completed, has data (generic type T)
// - Error: failed, has an error message

type FetchState<T> = /* your union here */;

// Write a function render<T>(state: FetchState<T>): string
// that returns a string describing the current state
// TypeScript should warn you if you forget to handle any case

function render<T>(state: FetchState<T>): string {
  // your code here
}
```

---

### Exercise 4.3 — Intersection Types

```ts
interface WithId { id: number }
interface WithTimestamps { createdAt: Date; updatedAt: Date }
interface WithSoftDelete { deletedAt: Date | null }

interface Post { title: string; body: string; authorId: number }

// 1. Create a type DatabasePost that combines Post with ID and timestamps
// 2. Create a type SoftDeletablePost that can also be soft-deleted
// 3. Write a function createPost(data: Omit<Post, never>) that returns a DatabasePost
//    (you'll need to add id and timestamps)
```

---

## Section 5: Arrays & Tuples

### Exercise 5.1 — Array Types

```ts
// Type the following and fix any errors

// 1. A list of product names
let productNames = ["Laptop", "Phone", "Tablet"];

// 2. A list of prices that should NOT be modified after creation
let prices = [999, 499, 299];

// 3. An array of User objects (use your User interface from earlier)
let users = [];

// 4. Write a function that takes a number array and returns a new array
//    with each value doubled — do NOT modify the original
function doubleValues(nums: /* type */ ): /* return type */ {
  // your code
}
```

---

### Exercise 5.2 — Tuples

```ts
// 1. Define a tuple type for a coordinate: [longitude, latitude]
//    Write a function distance(a: Coordinate, b: Coordinate): number

// 2. Define a tuple type for a CSV row entry: [id, name, email, age]
//    where id is number, others are strings, age is optional number
//    Write a function parseRow(row: CSVRow): User

// 3. Build a simple useState-like function:
function useState<T>(initial: T): [T, (newValue: T) => void] {
  let value = initial;
  const setValue = (newValue: T) => { value = newValue; };
  return [value, setValue];
}
// Test it with a string, then with a number
```

---

# Section 6: Generics

Generics let you write functions, interfaces, and classes that work with **any type** while still being fully type-safe. Think of them as "type variables" — instead of hardcoding `string` or `number`, you write `T` and let TypeScript fill it in at the call site.

```typescript
// Without generics — only works for strings
function identity(value: string): string {
  return value;
}

// With generics — works for any type, and TypeScript tracks which type you used
function identity<T>(value: T): T {
  return value;
}

const s = identity("hello"); // TypeScript knows: s is string
const n = identity(42);      // TypeScript knows: n is number
const b = identity(true);    // TypeScript knows: b is boolean
```

---

## Exercise 6.0 — Warm-Up: Read and Predict

Before writing any generics yourself, read these examples and answer the questions in comments.

```typescript
// Example 1
function wrap<T>(value: T): T[] {
  return [value];
}

const a = wrap("hello");
const b = wrap(123);
const c = wrap({ name: "Alice" });

// Q: What is the type of `a`?  →
// Q: What is the type of `b`?  →
// Q: What is the type of `c`?  →


// Example 2
function pair<A, B>(first: A, second: B): [A, B] {
  return [first, second];
}

const p1 = pair("age", 30);
const p2 = pair(true, ["x", "y"]);

// Q: What is the type of `p1`?  →
// Q: What is the type of `p2`?  →


// Example 3 — TypeScript infers the type argument from usage
function echo<T>(value: T, times: number): T[] {
  return Array(times).fill(value);
}

const words = echo("hey", 3);  // string[]
const nums  = echo(0, 5);      // number[]

// Q: Can you call echo() without providing <T> explicitly? Why or why not?  →
```

---

## Exercise 6.1 — Your First Generic Functions

Start simple: write these one at a time and test each in your editor.

```typescript
// 1a. Write a generic function `first` that returns the first element of any array,
//     or undefined if the array is empty.
//
// Example usage:
//   first([1, 2, 3])          // → 1       (type: number)
//   first(["a", "b"])         // → "a"     (type: string)
//   first([])                 // → undefined
function first<T>(arr: T[]): T | undefined {
  // your code here
}


// 1b. Write a generic function `last` — same idea but returns the last element.
//
// Example usage:
//   last([10, 20, 30])        // → 30
//   last(["only"])            // → "only"
//   last([])                  // → undefined
function last<T>(arr: T[]): T | undefined {
  // your code here
}


// 1c. Write a generic function `repeat` that takes a value and a count,
//     and returns an array with that value repeated count times.
//
// Example usage:
//   repeat("ha", 3)           // → ["ha", "ha", "ha"]
//   repeat(0, 4)              // → [0, 0, 0, 0]
//   repeat(true, 2)           // → [true, true]
function repeat<T>(value: T, count: number): T[] {
  // your code here
}


// 1d. Write a generic function `compact` that removes null and undefined
//     from an array. The return type should NOT include null or undefined.
//
// Example usage:
//   compact([1, null, 2, undefined, 3])  // → [1, 2, 3]   (type: number[])
//   compact(["a", null, "b"])            // → ["a", "b"]  (type: string[])
function compact<T>(arr: (T | null | undefined)[]): T[] {
  // your code here
}
```

---

## Exercise 6.2 — Multiple Type Parameters

Some generic functions need more than one type variable.

```typescript
// Here's an example with two type parameters:
function zipWith<A, B, C>(
  arr1: A[],
  arr2: B[],
  fn: (a: A, b: B) => C
): C[] {
  return arr1.map((item, i) => fn(item, arr2[i]));
}

// Usage:
zipWith([1, 2, 3], [10, 20, 30], (a, b) => a + b);
// → [11, 22, 33]

zipWith(["a", "b"], [1, 2], (letter, num) => `${letter}${num}`);
// → ["a1", "b2"]


// Now try these:

// 2a. Write a function `mapObject` that takes an object and a transform function,
//     and returns a new object with all values transformed.
//
// Example usage:
//   mapObject({ a: 1, b: 2, c: 3 }, n => n * 2)
//   // → { a: 2, b: 4, c: 6 }
//
//   mapObject({ name: "Alice", city: "NYC" }, s => s.toUpperCase())
//   // → { name: "ALICE", city: "NYC" }
function mapObject<K extends string, V, R>(
  obj: Record<K, V>,
  fn: (value: V, key: K) => R
): Record<K, R> {
  // your code here
}


// 2b. Write a function `partition` that takes an array and a predicate,
//     and returns two arrays: [itemsThatPass, itemsThatFail].
//
// Example usage:
//   partition([1, 2, 3, 4, 5], n => n % 2 === 0)
//   // → [[2, 4], [1, 3, 5]]
//
//   partition(["hello", "hi", "world"], s => s.length > 3)
//   // → [["hello", "world"], ["hi"]]
function partition<T>(arr: T[], predicate: (item: T) => boolean): [T[], T[]] {
  // your code here
}


// 2c. Write `groupBy` — takes an array and a key function,
//     returns an object grouping items by the key.
//
// Example usage:
//   const people = [
//     { name: "Alice", age: 20 },
//     { name: "Bob",   age: 30 },
//     { name: "Carol", age: 20 },
//   ];
//   groupBy(people, p => p.age)
//   // → { 20: [{name:"Alice",...}, {name:"Carol",...}], 30: [{name:"Bob",...}] }
function groupBy<T, K extends string | number>(
  items: T[],
  getKey: (item: T) => K
): Partial<Record<K, T[]>> {
  // your code here
}
```

---

## Exercise 6.3 — Generic Interfaces

Generics aren't just for functions — interfaces and types can be generic too.

```typescript
// Example: a generic Box that holds any value
interface Box<T> {
  value: T;
  label: string;
}

const numberBox: Box<number> = { value: 42,      label: "My number" };
const stringBox: Box<string> = { value: "hello", label: "My string" };


// 3a. Create a generic interface `Pair<A, B>` with properties `first` and `second`.
//     Then write a function `swap` that takes a Pair and returns a new Pair
//     with the values switched.
//
// Example usage:
//   const p: Pair<string, number> = { first: "age", second: 30 };
//   swap(p)  // → { first: 30, second: "age" }  (type: Pair<number, string>)
interface Pair<A, B> {
  // your code here
}

function swap<A, B>(pair: Pair<A, B>): Pair<B, A> {
  // your code here
}


// 3b. Create a generic interface `Result<T, E = Error>` that represents
//     either a success (with data) or a failure (with an error).
//     Then write helper functions `success` and `failure`.
//
// Example usage:
//   const ok  = success(42);           // Result<number>
//   const err = failure(new Error("oops")); // Result<never, Error>
//
//   if (ok.ok) {
//     console.log(ok.data);   // ✅ TypeScript knows data exists
//   } else {
//     console.log(ok.error);  // ✅ TypeScript knows error exists
//   }
type Result<T, E = Error> =
  | { ok: true;  data: T }
  | { ok: false; error: E };

function success<T>(data: T): Result<T> {
  // your code here
}

function failure<E = Error>(error: E): Result<never, E> {
  // your code here
}


// 3c. Create a generic interface `Repository<T>` — a standard pattern for
//     database access. All methods are async.
//
// Hint: The "id" field on T is always a number.
// You'll need to use Omit<T, "id"> for create() so callers don't pass the id.
interface Repository<T extends { id: number }> {
  findById(id: number): Promise<T | null>;
  findAll(): Promise<T[]>;
  create(data: Omit<T, "id">): Promise<T>;
  update(id: number, data: Partial<T>): Promise<T | null>;
  delete(id: number): Promise<boolean>;
}

// Now show how you'd use this — create an interface `UserRecord` and
// declare (don't implement) a `UserRepository` that implements Repository<UserRecord>:
interface UserRecord {
  id: number;
  name: string;
  email: string;
}

// declare const userRepo: Repository<UserRecord>;
// userRepo.findById(1)                   // → Promise<UserRecord | null>
// userRepo.create({ name: "Alice", email: "a@b.com" })  // → Promise<UserRecord>
```

---

## Exercise 6.4 — Generic Constraints

Sometimes you want to accept "any type, as long as it has certain properties." Use `extends` to add constraints.

```typescript
// Without a constraint — T could be anything, so this errors:
// function getLength<T>(value: T): number {
//   return value.length; // ❌ T might not have .length
// }

// With a constraint — we guarantee T has a .length property:
function getLength<T extends { length: number }>(value: T): number {
  return value.length; // ✅
}

getLength("hello");        // ✅ strings have .length
getLength([1, 2, 3]);      // ✅ arrays have .length
getLength({ length: 10 }); // ✅
// getLength(42);           // ❌ numbers don't have .length


// 4a. Write a function `merge` that takes two objects and combines them.
//     The return type should be the intersection of both input types.
//
// Example usage:
//   merge({ name: "Alice" }, { age: 30 })
//   // → { name: "Alice", age: 30 }  (type: { name: string } & { age: number })
function merge<T extends object, U extends object>(a: T, b: U): T & U {
  // your code here
}


// 4b. Write a fully type-safe property accessor `getProperty`.
//     The key must actually exist on the object — TypeScript enforces this.
//
// Example usage:
//   const user = { id: 1, name: "Alice", age: 30 };
//   getProperty(user, "name")   // → "Alice"  (type: string)
//   getProperty(user, "id")     // → 1        (type: number)
//   getProperty(user, "email")  // ❌ TypeScript error — "email" doesn't exist
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  // your code here
}


// 4c. Write a function `clamp` that constrains a number between min and max.
//     It should work for both number and bigint.
//
// Example usage:
//   clamp(15, 0, 10)   // → 10
//   clamp(-5, 0, 10)   // → 0
//   clamp(7,  0, 10)   // → 7
function clamp<T extends number | bigint>(value: T, min: T, max: T): T {
  // your code here
}


// 4d. Write a function `sortBy` that sorts an array of objects by any key.
//     The key's value must be comparable (string or number).
//
// Example usage:
//   const people = [{ name: "Charlie" }, { name: "Alice" }, { name: "Bob" }];
//   sortBy(people, "name")
//   // → [{ name: "Alice" }, { name: "Bob" }, { name: "Charlie" }]
function sortBy<T extends Record<string, string | number>>(
  items: T[],
  key: keyof T
): T[] {
  // your code here
}
```

---

## Exercise 6.5 — Challenge: Chaining Generics

These combine everything from this section. Take your time.

```typescript
// 5a. Write a generic `pipe` function that takes a value and a list of
//     single-argument transform functions, applying them left to right.
//     For simplicity, restrict this to a 3-function pipe.
//
// Example usage:
//   pipe(
//     "  hello world  ",
//     (s: string) => s.trim(),
//     (s: string) => s.split(" "),
//     (arr: string[]) => arr.length
//   )
//   // → 2  (type: number)
function pipe<A, B, C, D>(
  value: A,
  fn1: (a: A) => B,
  fn2: (b: B) => C,
  fn3: (c: C) => D
): D {
  // your code here
}


// 5b. Write a generic `memoize` function that wraps any single-argument
//     function and caches its results.
//
// Example usage:
//   const expensiveDouble = memoize((n: number) => {
//     console.log("computing...");
//     return n * 2;
//   });
//
//   expensiveDouble(5);  // logs "computing...", returns 10
//   expensiveDouble(5);  // returns 10 (from cache, no log)
//   expensiveDouble(3);  // logs "computing...", returns 6
function memoize<Arg, Return>(
  fn: (arg: Arg) => Return
): (arg: Arg) => Return {
  // your code here
}
```

---
---

# Section 7: Classes

TypeScript adds access modifiers, generics, abstract classes, and interface implementation on top of JavaScript's class syntax. Classes are also a key place where the **type** of an object and its **runtime behavior** are defined together.

```typescript
// A quick refresher on what TypeScript adds to classes:
class Counter {
  private count: number = 0;   // only accessible inside this class
  readonly id: string;          // can be set in constructor, never again

  constructor(id: string) {
    this.id = id;
  }

  increment(): void {
    this.count++;
  }

  get value(): number {       // getter — accessed as a property, not a method
    return this.count;
  }
}

const c = new Counter("counter-1");
c.increment();
console.log(c.value);  // 1
// c.count = 10;       // ❌ private
// c.id = "new-id";    // ❌ readonly
```

---

## Exercise 7.0 — Warm-Up: Reading Classes

Read these classes and answer the questions.

```typescript
class BankAccount {
  private balance: number;
  readonly owner: string;
  private static totalAccounts: number = 0;

  constructor(owner: string, initialBalance: number = 0) {
    this.owner = owner;
    this.balance = initialBalance;
    BankAccount.totalAccounts++;
  }

  deposit(amount: number): void {
    if (amount <= 0) throw new Error("Amount must be positive");
    this.balance += amount;
  }

  withdraw(amount: number): boolean {
    if (amount > this.balance) return false;
    this.balance -= amount;
    return true;
  }

  get currentBalance(): number {
    return this.balance;
  }

  static getAccountCount(): number {
    return BankAccount.totalAccounts;
  }
}

const acc = new BankAccount("Alice", 100);
acc.deposit(50);

// Q: What does acc.currentBalance return?  →
// Q: Can you write `acc.balance = 500` outside the class?  →
// Q: How would you call getAccountCount()?  →
// Q: What happens if you call acc.withdraw(200)?  →
// Q: Can you write `acc.owner = "Bob"`?  →
```

---

## Exercise 7.1 — Build It Step by Step: Stack<T>

A `Stack` is a last-in, first-out (LIFO) data structure. Build it in stages.

```typescript
// Stage 1: Core structure — just make it compile with the right shape.
// Don't worry about error handling yet.
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    // Add item to top of stack
  }

  pop(): T | undefined {
    // Remove and return the top item (or undefined if empty)
  }

  peek(): T | undefined {
    // Return (but don't remove) the top item
  }

  get size(): number {
    // Return the number of items
  }

  get isEmpty(): boolean {
    // Return true if no items
  }
}

// Test Stage 1:
const s1 = new Stack<number>();
s1.push(1);
s1.push(2);
console.log(s1.peek());   // 2
console.log(s1.size);     // 2
console.log(s1.isEmpty);  // false


// Stage 2: Add error handling.
// pop() and peek() should throw a descriptive error (not return undefined) when empty.
class Stack<T> {
  private items: T[] = [];

  push(item: T): void { /* your code */ }

  pop(): T {
    if (this.isEmpty) throw new Error("Stack is empty — cannot pop");
    // your code
  }

  peek(): T {
    if (this.isEmpty) throw new Error("Stack is empty — cannot peek");
    // your code
  }

  get size(): number { /* your code */ }
  get isEmpty(): boolean { /* your code */ }


  // Stage 2 additions:

  clear(): void {
    // Remove all items
  }

  toArray(): T[] {
    // Return a COPY of items (not a reference to the internal array)
    // Hint: why does returning a copy matter?
  }
}

// Test Stage 2:
const s2 = new Stack<string>();
s2.push("a");
s2.push("b");
s2.push("c");

const arr = s2.toArray();
arr.push("d");             // modifying the copy
console.log(s2.size);      // still 3 — the original is unchanged ✅

s2.clear();
console.log(s2.isEmpty);   // true

try {
  s2.pop();                // throws
} catch (e) {
  console.log(e.message);  // "Stack is empty — cannot pop"
}


// Stage 3: Add a static factory method and a `contains` method.
class Stack<T> {
  // ...everything from Stage 2...

  contains(item: T): boolean {
    // Return true if the item is in the stack
  }

  // Static factory: creates a Stack pre-loaded from an array
  // Example: Stack.from([1, 2, 3]) → Stack with 3 as the top item
  static from<T>(items: T[]): Stack<T> {
    // your code
  }
}

// Test Stage 3:
const s3 = Stack.from([10, 20, 30]);
console.log(s3.size);          // 3
console.log(s3.peek());        // 30
console.log(s3.contains(20));  // true
console.log(s3.contains(99));  // false
```

---

## Exercise 7.2 — Abstract Classes: Shape Hierarchy

Abstract classes define a contract that subclasses must fulfill. You can't instantiate them directly — they're blueprints.

```typescript
// Here's the pattern explained:
abstract class Animal {
  abstract makeSound(): string;   // subclasses MUST implement this
  abstract readonly name: string; // subclasses MUST define this

  // Concrete method — shared by all subclasses
  describe(): string {
    return `${this.name} says "${this.makeSound()}"`;
  }
}

// new Animal();           // ❌ can't instantiate abstract class
class Dog extends Animal {
  readonly name = "Dog";
  makeSound() { return "Woof"; }
}
// new Dog().describe();   // ✅ "Dog says 'Woof'"


// Now build a shape hierarchy:

// Step 1: Define the abstract base class
abstract class Shape {
  abstract get name(): string;
  abstract area(): number;
  abstract perimeter(): number;

  // Implement this concrete method — it should use area() and perimeter()
  // and return a formatted string like:
  // "Circle — Area: 78.54, Perimeter: 31.42"
  describe(): string {
    // your code here
  }
}


// Step 2: Implement concrete shapes

class Rectangle extends Shape {
  constructor(
    private width: number,
    private height: number
  ) {
    super();
  }

  get name(): string { return "Rectangle"; }

  area(): number {
    // width × height
  }

  perimeter(): number {
    // 2 × (width + height)
  }
}


class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  get name(): string { return "Circle"; }

  area(): number {
    // π × r²
  }

  perimeter(): number {
    // 2 × π × r
  }
}


class Triangle extends Shape {
  // Takes three side lengths: a, b, c
  constructor(
    private a: number,
    private b: number,
    private c: number
  ) {
    super();
  }

  get name(): string { return "Triangle"; }

  perimeter(): number {
    // a + b + c
  }

  area(): number {
    // Heron's formula:
    // s = (a + b + c) / 2
    // area = √(s × (s-a) × (s-b) × (s-c))
  }
}


// Step 3: Write utility functions that accept any Shape

// Logs the result of shape.describe()
function printShapeInfo(shape: Shape): void {
  // your code here
}

// Returns the shape with the largest area
function largestShape(shapes: Shape[]): Shape {
  // your code here
}

// Test:
const shapes: Shape[] = [
  new Rectangle(4, 6),
  new Circle(5),
  new Triangle(3, 4, 5),
];

shapes.forEach(printShapeInfo);
// Rectangle — Area: 24.00, Perimeter: 20.00
// Circle    — Area: 78.54, Perimeter: 31.42
// Triangle  — Area: 6.00,  Perimeter: 12.00

console.log(largestShape(shapes).name);  // "Circle"
```

---

## Exercise 7.3 — Interfaces & Classes

A class can implement one or more interfaces. This is useful for defining contracts across unrelated class hierarchies.

```typescript
// Example: two totally different classes sharing an interface
interface Describable {
  describe(): string;
}

class Car implements Describable {
  constructor(private make: string, private model: string) {}
  describe() { return `${this.make} ${this.model}`; }
}

class Person implements Describable {
  constructor(private name: string) {}
  describe() { return `Person: ${this.name}`; }
}

// A function that works with ANYTHING that is Describable
function printAll(items: Describable[]): void {
  items.forEach(item => console.log(item.describe()));
}

printAll([new Car("Toyota", "Camry"), new Person("Alice")]);


// Now build a Temperature class that implements two interfaces:

// 3a. Define these interfaces:
interface Comparable<T> {
  // Returns -1 if this < other, 0 if equal, 1 if this > other
  compareTo(other: T): -1 | 0 | 1;
}

interface Printable {
  // Human-readable string representation
  toString(): string;
}


// 3b. Build the Temperature class:
class Temperature implements Comparable<Temperature>, Printable {
  // Store temperature internally in Celsius (private)
  private readonly _celsius: number;

  private constructor(celsius: number) {
    this._celsius = celsius;
  }

  // Static factory methods — callers use these instead of `new`
  static fromCelsius(c: number): Temperature {
    // your code here
  }

  static fromFahrenheit(f: number): Temperature {
    // Hint: celsius = (f - 32) × 5/9
  }

  // Getters
  get celsius(): number {
    return this._celsius;
  }

  get fahrenheit(): number {
    // celsius × 9/5 + 32
  }

  // Returns a string like "100°C / 212°F"
  toString(): string {
    // your code here
  }

  compareTo(other: Temperature): -1 | 0 | 1 {
    // your code here
  }
}


// Test:
const boiling  = Temperature.fromCelsius(100);
const freezing = Temperature.fromFahrenheit(32);
const body     = Temperature.fromCelsius(37);

console.log(boiling.toString());           // "100°C / 212°F"
console.log(freezing.celsius);             // 0
console.log(body.compareTo(boiling));      // -1
console.log(boiling.compareTo(boiling));   // 0

// Sort an array of temperatures using compareTo
const temps = [boiling, freezing, body];
temps.sort((a, b) => a.compareTo(b));
temps.forEach(t => console.log(t.toString()));
// 0°C / 32°F
// 37°C / 98.6°F
// 100°C / 212°F
```

---

## Exercise 7.4 — Challenge: Generic Class with Constraints

Combine classes, generics, and interfaces into one cohesive challenge.

```typescript
// Build a `SortedList<T>` class — a list that always stays sorted.
// Elements must be Comparable (using the interface from 7.3).

class SortedList<T extends Comparable<T>> {
  private items: T[] = [];

  // Insert an item in the correct position to maintain sort order
  insert(item: T): void {
    // Hint: find the first index where item.compareTo(items[i]) <= 0
    // and splice it in. Or push and re-sort — either works.
  }

  // Remove an item by value. Return true if removed, false if not found.
  remove(item: T): boolean {
    // your code here
  }

  // Return items as a sorted array (a copy)
  toArray(): T[] {
    return [...this.items];
  }

  get size(): number {
    return this.items.length;
  }

  // Return the smallest item
  min(): T | undefined {
    return this.items[0];
  }

  // Return the largest item
  max(): T | undefined {
    return this.items[this.items.length - 1];
  }
}


// Test with Temperature (which implements Comparable<Temperature>):
const tempList = new SortedList<Temperature>();
tempList.insert(Temperature.fromCelsius(100));
tempList.insert(Temperature.fromCelsius(0));
tempList.insert(Temperature.fromCelsius(37));
tempList.insert(Temperature.fromCelsius(-10));

tempList.toArray().forEach(t => console.log(t.toString()));
// -10°C / 14°F
// 0°C / 32°F
// 37°C / 98.6°F
// 100°C / 212°F

console.log(tempList.min()?.toString());   // "-10°C / 14°F"
console.log(tempList.max()?.toString());   // "100°C / 212°F"
```

## Section 8: Type Narrowing

### Exercise 8.1 — Narrow the Type

```ts
type StringOrNumber = string | number;

// Write these functions with proper type narrowing:

// 1. double(x: StringOrNumber): StringOrNumber
//    If string, repeat it twice ("hi" → "hihi")
//    If number, multiply by 2 (5 → 10)

// 2. Given:
interface Bird  { type: "bird";  fly(): void;  feathers: number }
interface Fish  { type: "fish";  swim(): void; fins: number }
interface Snake { type: "snake"; slither(): void; length: number }
type Animal = Bird | Fish | Snake;

// Write move(animal: Animal): void using a switch on type
// TypeScript should warn you if you add a 4th type and forget to handle it
```

---

### Exercise 8.2 — Custom Type Guards

```ts
// 1. Write a type guard isString(value: unknown): value is string

// 2. Write a type guard isUser(value: unknown): value is User
//    Check that value has id (number), name (string), email (string)

// 3. Given an API that returns unknown, write a function
//    parseApiResponse<T>(data: unknown, guard: (x: unknown) => x is T): T
//    that returns T if guard passes, or throws a descriptive error

// 4. Write a type guard isNonEmpty<T>(arr: T[]): arr is [T, ...T[]]
//    (a non-empty array type)
```

---

## Section 9: Utility Types

### Exercise 9.1 — Utility Type Workout

Given this interface:

```ts
interface BlogPost {
  id: number;
  title: string;
  body: string;
  authorId: number;
  publishedAt: Date | null;
  tags: string[];
  views: number;
}
```

Use utility types to create these derived types **without rewriting properties**:

```ts
// 1. CreatePostDto — everything except id, views, and publishedAt (use Omit)
type CreatePostDto = /* your answer */;

// 2. UpdatePostDto — CreatePostDto but all fields optional (combine Omit + Partial)
type UpdatePostDto = /* your answer */;

// 3. PostSummary — only id, title, authorId, tags (use Pick)
type PostSummary = /* your answer */;

// 4. PublishedPost — BlogPost where publishedAt is Date (not null)
//    Hint: Use Omit and add the narrower type back
type PublishedPost = /* your answer */;

// 5. Create a Record type that maps post IDs to PostSummaries
type PostCache = /* your answer */;
```

---

### Exercise 9.2 — Building with Utility Types

```ts
// Build a simple type-safe event emitter using utility types

type EventMap = {
  login:   { userId: string; timestamp: Date };
  logout:  { userId: string };
  error:   { code: number; message: string };
  resize:  { width: number; height: number };
};

// Using the EventMap, implement these types:
// 1. EventName — a union of all keys in EventMap
// 2. EventPayload<K extends EventName> — the payload type for event K
// 3. EventHandler<K extends EventName> — a function that takes EventPayload<K>
// 4. EventHandlerMap — an object that can hold handlers for any event

// Then implement a simple class EventEmitter that:
// - on<K extends EventName>(event: K, handler: EventHandler<K>): void
// - emit<K extends EventName>(event: K, payload: EventPayload<K>): void
```

---

## Section 10: Async TypeScript

### Exercise 10.1 — Type Async Functions

```ts
// Type these async functions properly

// 1. Fetches a user by ID from an API
async function fetchUser(id: /* type */) /* return type */ {
  const res = await fetch(`https://api.example.com/users/${id}`);
  return res.json();
}

// 2. Saves a new post and returns the saved post (with ID)
async function createPost(data: CreatePostDto) /* return type */ {
  // implementation not important
}

// 3. Takes an array of user IDs, fetches them all in parallel, returns User[]
async function fetchMultipleUsers(ids: number[]) /* return type */ {
  // Hint: use Promise.all
}

// 4. A retry utility — takes an async function and retries up to N times
async function retry<T>(
  fn: /* type */,
  retries: number
): Promise<T> {
  // your implementation
}
```

---

### Exercise 10.2 — Error Handling

```ts
// 1. Create a type SafeResult<T> = 
//    | { success: true; data: T }
//    | { success: false; error: Error }

// 2. Write a wrapper function tryCatch<T>(fn: () => Promise<T>): Promise<SafeResult<T>>

// 3. Use your tryCatch to wrap a fetch call to a fake endpoint
//    Then handle both success and error cases with full type narrowing

// 4. Write a function withTimeout<T>(promise: Promise<T>, ms: number): Promise<T>
//    that rejects with an error if the promise doesn't resolve within ms milliseconds
```

---

## Section 11: Real-World Mini Projects

### Project 1: Type-Safe Todo App (Frontend Focus)

Build the complete type layer for a todo application. **Write types only — no implementation required** unless you want to.

```ts
// Requirements:

// 1. Define a Todo interface:
//    id, title, completed, priority ("low"|"medium"|"high"), createdAt, dueDate (optional)

// 2. Define action types for a useReducer hook:
//    ADD_TODO, TOGGLE_TODO, DELETE_TODO, UPDATE_TODO, CLEAR_COMPLETED, SET_FILTER

// 3. Define a TodoState interface for the reducer state

// 4. Write the reducer function — TypeScript should catch any unhandled action type

// 5. Define props interfaces for these components:
//    - TodoList: receives todos and a dispatch function
//    - TodoItem: receives a single todo, dispatch, and an onEdit callback
//    - TodoForm: receives onSubmit that takes a new todo (without id/createdAt)
//    - FilterBar: receives current filter and onChange handler

// 6. Write a custom hook useTodos() that returns:
//    { todos, addTodo, toggleTodo, deleteTodo, filteredTodos, filter, setFilter }
```

---

### Project 2: Express REST API Types (Backend Focus)

```ts
// Type a complete Express REST API for a blog system

// 1. Define interfaces: Post, User, Comment, Tag
//    Include appropriate optional and readonly fields

// 2. Define DTO types: CreatePostDto, UpdatePostDto, CreateCommentDto

// 3. Define typed route handlers for:
//    GET    /posts              → returns Post[]
//    GET    /posts/:id          → returns Post or 404
//    POST   /posts              → accepts CreatePostDto, returns Post
//    PUT    /posts/:id          → accepts UpdatePostDto, returns Post
//    DELETE /posts/:id          → returns { success: boolean }
//    GET    /posts/:id/comments → returns Comment[]
//    POST   /posts/:id/comments → accepts CreateCommentDto, returns Comment

// 4. Create a typed middleware that:
//    - Reads a JWT from Authorization header
//    - Attaches a decoded User to req.user
//    - Extends Express Request type via declaration merging

// 5. Create a generic error response type and a success response type
//    Write a helper that wraps any Express response in the success format
```

---

### Project 3: Generic Data Table Component

Build a fully type-safe, reusable data table component type system:

```ts
// A DataTable component should be generic over the row data type T
// and support:

// 1. A Column<T> type that defines:
//    - key: keyof T
//    - header: string
//    - render?: (value: T[keyof T], row: T) => React.ReactNode  (optional custom renderer)
//    - sortable?: boolean
//    - width?: number | string

// 2. A DataTableProps<T> interface with:
//    - data: T[]
//    - columns: Column<T>[]
//    - onRowClick?: (row: T) => void
//    - loading?: boolean
//    - emptyMessage?: string
//    - pagination?: { page: number; pageSize: number; total: number; onPageChange: (page: number) => void }

// 3. Write the DataTable component signature (just the type, not full implementation):
//    function DataTable<T extends Record<string, unknown>>(props: DataTableProps<T>): JSX.Element

// 4. Show usage examples with:
//    - A User data table
//    - A Product data table
//    Both should have full type checking on column keys
```

---

## Section 12: Challenge Problems

These are harder problems to stretch your understanding.

### Challenge 1: DeepReadonly

Implement a `DeepReadonly<T>` utility type that makes all nested properties readonly:

```ts
type DeepReadonly<T> = /* your solution */;

interface Config {
  server: { host: string; port: number };
  database: { url: string; name: string; options: { ssl: boolean } };
}

const config: DeepReadonly<Config> = { /* ... */ };
config.server.port = 3000;           // ❌ should be an error
config.database.options.ssl = true;  // ❌ should be an error
```

---

### Challenge 2: Builder Pattern

Implement a type-safe query builder:

```ts
// The builder should track which methods have been called using the type system
// so that calling .where() twice should be a type error

interface QueryBuilder<
  HasTable extends boolean = false,
  HasWhere extends boolean = false
> {
  from(table: string): QueryBuilder<true, HasWhere>;
  where(condition: string): HasTable extends true ? QueryBuilder<true, true> : never;
  limit(n: number): HasTable extends true ? QueryBuilder<HasTable, HasWhere> : never;
  build(): HasTable extends true ? string : never;
}

// Usage:
// const q = builder.from("users").where("id = 1").limit(10).build() ✅
// const q = builder.where("id = 1").build() ❌ should error — no table
```

---

### Challenge 3: Flatten Type

Write a type `Flatten<T>` that takes a nested object type and flattens it with dot notation keys:

```ts
type Flatten<T> = /* your solution */;

interface Nested {
  a: string;
  b: {
    c: number;
    d: {
      e: boolean;
    };
  };
}

type Flat = Flatten<Nested>;
// Should be: { "a": string; "b.c": number; "b.d.e": boolean }
```

---

### Challenge 4: Event System with Type Inference

Build a fully type-safe pub/sub event system where the type of the payload is automatically inferred from the event name:

```ts
class TypedEventEmitter<Events extends Record<string, unknown>> {
  on<K extends keyof Events>(
    event: K,
    listener: (payload: Events[K]) => void
  ): this;

  emit<K extends keyof Events>(
    event: K,
    payload: Events[K]
  ): boolean;

  off<K extends keyof Events>(
    event: K,
    listener: (payload: Events[K]) => void
  ): this;
}

// Usage:
const emitter = new TypedEventEmitter<{
  message: { text: string; from: string };
  connect: { userId: string };
  disconnect: void;
}>();

emitter.on("message", (payload) => {
  console.log(payload.text); // ✅ payload inferred as { text: string; from: string }
});

emitter.emit("message", { text: "hello", from: "Alice" }); // ✅
emitter.emit("message", { wrong: "shape" }); // ❌ Error
```

---

## Answer Hints

> Only read these if you're truly stuck!

**Exercise 1.3:** Use `typeof input === "string"` inside an if block. TS narrows inside the block.

**Exercise 2.3:** Write function overloads as separate declarations above the implementation. The implementation signature must accept all overloaded cases.

**Exercise 4.2:** A discriminated union with `{ status: "idle" }`, `{ status: "loading" }`, `{ status: "success"; data: T }`, `{ status: "error"; message: string }`. Use a `switch(state.status)` to get exhaustiveness checking.

**Exercise 6.3 (groupBy):** The return type is `Partial<Record<K, T[]>>` or `Record<K, T[]>`. Use `Object.keys`, `reduce`, or a for loop.

**Exercise 9.2:** `keyof EventMap` gives you the event names. Index access types `EventMap[K]` gives you the payload.

**Challenge 1:** Use conditional types + mapped types: `type DeepReadonly<T> = { readonly [K in keyof T]: T[K] extends object ? DeepReadonly<T[K]> : T[K] }`.

**Challenge 3:** Look up "recursive conditional types" and "template literal types" — you'll need both. This is advanced!

---

## Self-Assessment Checklist

After completing these exercises, you should be able to check off:

**Fundamentals**
- [ ] Annotate variables, function params, and return types
- [ ] Use `unknown` instead of `any` and narrow it safely
- [ ] Define and extend interfaces
- [ ] Use union and intersection types correctly
- [ ] Work with arrays and tuples

**Intermediate**
- [ ] Write generic functions, interfaces, and classes
- [ ] Use all common utility types (Partial, Omit, Pick, Record, etc.)
- [ ] Narrow union types with typeof, instanceof, in, and custom guards
- [ ] Use discriminated unions with exhaustive switch statements
- [ ] Type async functions and handle errors properly

**Applied**
- [ ] Type React component props, state, refs, and event handlers
- [ ] Type Express route handlers, middleware, and request bodies
- [ ] Extend 3rd-party types using module augmentation
- [ ] Use `as const` and `satisfies` appropriately
- [ ] Model complex domain types cleanly and reusably

---

*Keep building. The more TypeScript you write, the more intuitive it becomes. When in doubt, let the compiler guide you — that's what it's there for!*
