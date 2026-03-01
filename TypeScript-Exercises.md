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

## Section 6: Generics

### Exercise 6.1 — Generic Functions

```ts
// 1. Write a generic function first<T>(arr: T[]): T | undefined
//    that returns the first element of any array

// 2. Write a generic function last<T>(arr: T[]): T | undefined

// 3. Write a generic function filterNull<T>(arr: (T | null | undefined)[]): T[]
//    that removes null/undefined from an array

// 4. Write a generic function groupBy<T, K extends string | number>(
//    items: T[], getKey: (item: T) => K): Record<K, T[]>
//    that groups array items by a key function

// Example usage of groupBy:
// groupBy([{age: 20, name: "Alice"}, {age: 30, name: "Bob"}, {age: 20, name: "Charlie"}], u => u.age)
// Should return: { 20: [{...Alice}, {...Charlie}], 30: [{...Bob}] }
```

---

### Exercise 6.2 — Generic Interfaces

```ts
// 1. Create a generic interface Pair<A, B> with properties first and second
//    Write a function swap<A, B>(pair: Pair<A, B>): Pair<B, A>

// 2. Create a generic interface Repository<T> with methods:
//    - findById(id: number): Promise<T | null>
//    - findAll(): Promise<T[]>
//    - create(data: Omit<T, "id">): Promise<T>
//    - update(id: number, data: Partial<T>): Promise<T | null>
//    - delete(id: number): Promise<boolean>

// 3. Create a generic interface Result<T, E = Error> representing success or failure:
//    - ok: boolean
//    - data?: T
//    - error?: E
//    Write a helper function success<T>(data: T): Result<T>
//    and failure<E>(error: E): Result<never, E>
```

---

### Exercise 6.3 — Generic Constraints

```ts
// 1. Write a function merge<T extends object, U extends object>(a: T, b: U): T & U
//    that merges two objects

// 2. Write a function getProperty<T, K extends keyof T>(obj: T, key: K): T[K]
//    A fully type-safe property accessor

// 3. Write a function clamp<T extends number | bigint>(value: T, min: T, max: T): T
//    that clamps a value between min and max

// 4. Write a function sortBy<T>(items: T[], key: keyof T): T[]
//    that sorts an array of objects by any key
```

---

## Section 7: Classes

### Exercise 7.1 — Build a Class

Build a `Stack<T>` class:

```ts
class Stack<T> {
  // Requirements:
  // - private items array
  // - push(item: T): void
  // - pop(): T — should throw an error if stack is empty
  // - peek(): T — should throw if empty
  // - get size(): number — a getter
  // - get isEmpty(): boolean — a getter
  // - clear(): void
  // - toArray(): T[] — returns a copy (not the original array)
}

// Test your Stack:
const stack = new Stack<number>();
stack.push(1);
stack.push(2);
stack.push(3);
console.log(stack.peek()); // 3
console.log(stack.pop());  // 3
console.log(stack.size);   // 2
```

---

### Exercise 7.2 — Abstract Classes

Create a simple shape hierarchy:

```ts
// Abstract base class Shape:
//   - abstract method area(): number
//   - abstract method perimeter(): number
//   - concrete method describe(): string that uses area() and perimeter()
//   - abstract property name: string

// Implement these concrete classes:
// - Rectangle (width, height)
// - Circle (radius)
// - Triangle (a, b, c — three side lengths; area via Heron's formula)

// Write a function printShapeInfo(shape: Shape): void
// Write a function largestShape(shapes: Shape[]): Shape
```

---

### Exercise 7.3 — Interfaces & Classes

```ts
// 1. Define an interface Comparable<T> with method compareTo(other: T): -1 | 0 | 1
// 2. Define an interface Printable with method toString(): string
// 3. Create a class Temperature that:
//    - Has a private celsius value
//    - Implements Comparable<Temperature>
//    - Implements Printable (returns "X°C / Y°F")
//    - Has static factory methods: fromCelsius(c) and fromFahrenheit(f)
//    - Has getters for celsius and fahrenheit
```

---

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
