# TypeScript Fundamentals for Full-Stack Development

### A Guide for JavaScript Developers

* * *

## Table of Contents

1.  [What is TypeScript & Why Use It?](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#1-what-is-typescript--why-use-it)
2.  [Setup & Configuration](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#2-setup--configuration)
3.  [Type Basics](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#3-type-basics)
4.  [Functions](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#4-functions)
5.  [Objects & Interfaces](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#5-objects--interfaces)
6.  [Type Aliases & Union Types](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#6-type-aliases--union-types)
7.  [Arrays & Tuples](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#7-arrays--tuples)
8.  [Enums](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#8-enums)
9.  [Generics](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#9-generics)
10. [Classes & OOP](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#10-classes--oop)
11. [Type Narrowing & Type Guards](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#11-type-narrowing--type-guards)
12. [Utility Types](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#12-utility-types)
13. [Modules & Namespaces](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#13-modules--namespaces)
14. [Working with APIs & Async TypeScript](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#14-working-with-apis--async-typescript)
15. [TypeScript with React (Frontend)](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#15-typescript-with-react-frontend)
16. [TypeScript with Node.js & Express (Backend)](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#16-typescript-with-nodejs--express-backend)
17. [Common Patterns & Best Practices](https://claude.ai/chat/ec705fe9-030a-4372-a1c8-01d1a44910b1#17-common-patterns--best-practices)

* * *

## 1\. What is TypeScript & Why Use It?

### The Big Idea

TypeScript is a **superset of JavaScript** — every valid JS file is also valid TypeScript. Think of it as JavaScript with a built-in spell-checker for your data.

It adds **optional static typing**, meaning you can declare what type of data a variable holds, and the TypeScript compiler will catch type errors before your code even runs.

> 🧠 **Mental Model:** JavaScript is like writing with autocorrect off. TypeScript turns autocorrect on — it catches your mistakes as you type, not after you hit Send.

### The Core Problem TypeScript Solves

In JavaScript, this bug only appears at runtime — after you've already shipped it to users:

```js
// JavaScript — no error until you run this
function greet(user) {
  return `Hello, ${user.naem}`; // typo: should be user.name
}
greet({ name: "Alice" }); // returns "Hello, undefined" — silent bug!
```

TypeScript catches it immediately, before the code ever runs:

```ts
// TypeScript — error at compile time
function greet(user: { name: string }) {
  return `Hello, ${user.naem}`; // ❌ Error: Property 'naem' does not exist
}
```

The red squiggly appears in your editor the moment you type it. Bug squashed before it ever reaches production.

### Key Benefits for Full-Stack Development

- **Autocomplete & IntelliSense** — your editor knows the shape of every object, so it can suggest properties and methods as you type
- **Refactoring safety** — rename a property and TypeScript tells you every single place that breaks, across your entire codebase
- **Self-documenting code** — type signatures act as inline documentation that never goes out of date
- **Fewer runtime bugs** — entire categories of errors (wrong property names, passing the wrong type of argument) are caught at compile time
- **Industry standard** — most modern React, Next.js, Node, and NestJS codebases use TypeScript; it's expected on the job

* * *

## 2\. Setup & Configuration

### Installation

```bash
npm install -g typescript          # global install (use tsc anywhere)
npm install --save-dev typescript  # or as a dev dependency in a project
```

### Compiling TypeScript

TypeScript files use the `.ts` extension. The compiler (`tsc`) converts them to plain `.js` files:

```bash
tsc hello.ts          # compiles hello.ts → hello.js
tsc --watch           # watch mode: recompiles automatically on file change
```

> 🧠 **Mental Model:** Think of `tsc` like a translator. You write in TypeScript, it translates to JavaScript that the browser or Node.js can understand.

### tsconfig.json

This file tells the TypeScript compiler how to behave. Generate one with:

```bash
tsc --init
```

Key options you should know:

```json
{
  "compilerOptions": {
    "target": "ES2020",           // what JS version to compile to
    "module": "commonjs",         // module system (commonjs for Node, ESNext for browser)
    "outDir": "./dist",           // where compiled JS goes
    "rootDir": "./src",           // where your TS source lives
    "strict": true,               // enables ALL strict checks — always use this
    "esModuleInterop": true,      // better default imports from CommonJS modules
    "skipLibCheck": true,         // skip type checking of .d.ts files
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

> ⚠️ **Always enable `"strict": true`.** It activates strict null checks, implicit `any` checks, and more. It feels stricter at first but saves you from a whole class of bugs. Think of it as turning on all the safety features at once.

### Running TypeScript Directly (for development)

During development, you don't want to manually compile every time. Use `ts-node` to run TypeScript directly:

```bash
npm install --save-dev ts-node nodemon
npx ts-node src/index.ts     # run TS without compiling first
```

* * *

## 3\. Type Basics

### Primitive Types

These mirror JavaScript's primitives — the same building blocks, just with explicit labels:

```ts
let username: string = "Alice";
let age: number = 30;
let isAdmin: boolean = false;
let nothing: null = null;
let missing: undefined = undefined;
let id: bigint = 9007199254740991n;
let sym: symbol = Symbol("unique");
```

The syntax is: `variableName: TypeName`. The colon means "is of type".

### Type Inference — TypeScript is Smart

You don't always have to write the type. If you assign a value immediately, TypeScript **infers** the type automatically:

```ts
let name = "Alice";   // TS infers: string
let count = 0;        // TS infers: number
let active = true;    // TS infers: boolean
```

> 🧠 **Mental Model:** TypeScript watches what you put in the box and labels the box for you. If you put a string in, it knows it's a string box.

**Rule of thumb:** Only add explicit type annotations when TypeScript can't infer the type, or when you want to be extra clear for the next developer (including future you).

### `any`, `unknown`, and `never`

These are special types you'll encounter often:

```ts
// any — opts OUT of type checking entirely. Avoid it.
let data: any = "hello";
data = 42;            // no error — type checking is off
data.foo.bar.baz;     // no error — but this will crash at runtime!
```

```ts
// unknown — the SAFE version of any. You must verify the type before using it.
let input: unknown = getUserInput();
if (typeof input === "string") {
  console.log(input.toUpperCase()); // ✅ safe — TypeScript knows it's a string here
}
```

```ts
// never — represents a value that can NEVER exist (unreachable code)
function throwError(msg: string): never {
  throw new Error(msg); // this function never returns normally
}
```

> 🧠 **Mental Model:**
> 
> - `any` = "I give up, don't check anything" (dangerous)
> - `unknown` = "I don't know yet, but I'll check before I use it" (safe)
> - `never` = "this can never happen" (useful for exhaustive checks)

**Golden Rule: Never use `any`. If you don't know the type, use `unknown` and narrow it.**

### `void`

Used for functions that don't return a value — they do something (like log to the console) but give nothing back:

```ts
function logMessage(msg: string): void {
  console.log(msg);
  // no return statement needed
}
```

* * *

## 4\. Functions

### Parameter & Return Type Annotations

You annotate parameters and return values with `: Type`:

```ts
// Basic function — takes two numbers, returns a number
function add(a: number, b: number): number {
  return a + b;
}

// Arrow function — same idea
const multiply = (a: number, b: number): number => a * b;

// TypeScript can infer the return type, but being explicit is good practice
const subtract = (a: number, b: number) => a - b; // return type inferred as number
```

> 🧠 **Mental Model:** Think of the return type as a promise to whoever calls the function. "I promise this function will hand you back a number." TypeScript enforces that promise.

### Optional & Default Parameters

Sometimes a parameter might not be provided. Use `?` to mark it optional:

```ts
// Optional parameter — use ? — must come AFTER required params
function greet(name: string, greeting?: string): string {
  return `${greeting ?? "Hello"}, ${name}!`;
  //                   ^^ if greeting is undefined, use "Hello"
}

greet("Alice");           // "Hello, Alice!"
greet("Alice", "Hi");     // "Hi, Alice!"
```

Default parameters work exactly like JavaScript:

```ts
function createUser(name: string, role: string = "user") {
  return { name, role };
}
```

### Rest Parameters

When a function can accept any number of arguments:

```ts
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, n) => acc + n, 0);
}

sum(1, 2, 3, 4); // 10
```

The `...numbers: number[]` says: "collect all remaining arguments into an array of numbers."

### Function Types

You can describe the *shape* of a function as a type — what arguments it takes and what it returns:

```ts
// Inline type annotation
let calculate: (a: number, b: number) => number;

calculate = (x, y) => x + y;   // ✅ matches the shape
calculate = (x, y) => "hello"; // ❌ Error: string not assignable to number

// Using a type alias (cleaner for reuse)
type MathOperation = (a: number, b: number) => number;
const divide: MathOperation = (a, b) => a / b;
```

### Overloads

When a function behaves differently depending on what type it receives, you can declare multiple "signatures":

```ts
// Declare what's possible
function formatInput(input: string): string;
function formatInput(input: number): string;

// Then implement the full logic
function formatInput(input: string | number): string {
  if (typeof input === "string") return input.trim();
  return input.toFixed(2);
}
```

> 🧠 **Mental Model:** Overloads are like a menu for your function. You list all the valid "orders" up top, then write one kitchen that handles them all.

* * *

## 5\. Objects & Interfaces

### Inline Object Types

For one-off object types, you can describe the shape inline:

```ts
function printUser(user: { name: string; age: number; email?: string }) {
  console.log(user.name, user.age);
}
```

This works, but if you use the same shape in multiple places, it gets repetitive. That's where interfaces come in.

### Interfaces

An interface is a **reusable, named description of an object's shape**. It's the preferred way to type objects in TypeScript:

```ts
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;             // optional — may or may not exist
  readonly createdAt: Date; // read-only — can be set once, never changed
}

const alice: User = {
  id: 1,
  name: "Alice",
  email: "alice@example.com",
  createdAt: new Date(),
};

alice.name = "Bob";           // ✅ fine
alice.createdAt = new Date(); // ❌ Error: cannot assign to read-only property
```

> 🧠 **Mental Model:** An interface is a contract. It says "any object claiming to be a `User` must have at least these properties." TypeScript enforces the contract everywhere.

### Extending Interfaces

Interfaces can inherit from other interfaces, so you can build up complex shapes from simpler ones:

```ts
interface Animal {
  name: string;
  age: number;
}

interface Dog extends Animal {
  breed: string;
  bark(): void;
}

const myDog: Dog = {
  name: "Rex",
  age: 3,
  breed: "Labrador",
  bark: () => console.log("Woof!"),
};
```

`Dog` automatically has everything from `Animal` plus its own properties.

### Index Signatures

When you don't know all the property names ahead of time — like a dictionary or a map:

```ts
interface StringMap {
  [key: string]: string;
}

const headers: StringMap = {
  "Content-Type": "application/json",
  Authorization: "Bearer abc123",
  // can add any string key → string value pair
};
```

> 🧠 **Mental Model:** An index signature says "I don't know the exact keys, but whatever the key is, the value will always be this type."

* * *

## 6\. Type Aliases & Union Types

### Type Aliases (Giving a Type a Nickname)

A type alias is just a name you give to a type so you don't have to repeat it everywhere. Think of it like a nickname.

```ts
type ID = string | number;
```

Instead of writing `string | number` everywhere, you just write `ID`.

More examples:

```ts
type Point = { x: number; y: number };
```

Now whenever you need a point:

```ts
let p: Point = { x: 10, y: 20 };
```

A function type alias:

```ts
type Callback = (err: Error | null, result?: string) => void;
```

This says: the function takes an error (or `null`) and an optional result, and returns nothing (`void`).

**Why this matters:**

- ✅ Makes code easier to read
- ✅ Avoids repeating complicated types
- ✅ Lets you change the type in one place

### `interface` vs `type` — What's the Difference?

Both can describe objects. The practical differences:

| Feature | `interface` | `type` |
| --- | --- | --- |
| Describe objects | ✅   | ✅   |
| Can be extended | `extends` keyword | `&` (intersection) |
| Can merge declarations | ✅   | ❌   |
| Can represent unions & primitives | ❌   | ✅   |

**Rule of thumb (easy to remember):**

- ✅ Use `interface` for objects and classes
- ✅ Use `type` for everything else (unions, primitives, function types)

```ts
// Use interface for objects
interface User {
  name: string;
  age: number;
}

// Use type for unions and other things
type ID = string | number;
```

### Union Types (This OR That)

A union type means a value can be **one of several types**. Think of it as choices:

```ts
type ID = string | number;
```

This means: `ID` can be a string OR a number.

```ts
let userId: ID = "abc-123"; // ✅
userId = 42;                // ✅ also valid
```

**Union with exact values — very common in real projects:**

```ts
type Status = "active" | "inactive" | "pending";
```

Only these exact strings are allowed:

```ts
function setStatus(status: Status) {
  console.log(status);
}

setStatus("active");   // ✅
setStatus("deleted");  // ❌ Error: "deleted" is not assignable to Status
```

This is great for preventing bugs, especially with UI states, API responses, and dropdown values.

### Intersection Types (This AND That)

An intersection type **combines multiple types into one**. The object must satisfy ALL of them.

Think:

- Union (`|`) = OR (one of these)
- Intersection (`&`) = AND (all of these)

```ts
interface WithTimestamps {
  createdAt: Date;
  updatedAt: Date;
}

interface Post {
  title: string;
  body: string;
}

type PostWithTimestamps = Post & WithTimestamps;
```

Now the combined type requires everything from both:

```ts
const post: PostWithTimestamps = {
  title: "Hello",
  body: "World",
  createdAt: new Date(),
  updatedAt: new Date(),
  // ❌ forget any field and TypeScript complains
};
```

> 🧠 **Real-world use:** Intersection types shine when you have base types (like audit timestamps or ownership) that you want to add on top of your domain types, without modifying the originals.

### Literal Types (Exact Values Only)

A literal type represents **one exact value**, not a category of values:

```ts
type Direction = "north" | "south" | "east" | "west";
```

Only these four strings are allowed — nothing else:

```ts
let facing: Direction = "north"; // ✅
facing = "up";                   // ❌ Error
```

Numeric literals work too:

```ts
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;
```

This prevents impossible values like `7`.

### Mental Model Summary 🧠

| Concept | Think of it as... |
| --- | --- |
| Type Alias | A nickname for a type |
| Union (`\|`) | One of many options (OR) |
| Intersection (`&`) | Must have everything (AND) |
| Literal Types | Exact allowed values only |
| `interface` | Best for objects and classes |
| `type` | Best for unions, primitives, functions |

* * *

## 7\. Arrays & Tuples

### Array Types

Two equivalent syntaxes — pick the one you prefer and be consistent:

```ts
let numbers: number[] = [1, 2, 3];     // preferred style
let names: Array<string> = ["Alice", "Bob"]; // generic style

// Array of objects
let users: User[] = [];

// Readonly arrays — can't be mutated after creation
const ids: readonly number[] = [1, 2, 3];
ids.push(4); // ❌ Error: cannot push to readonly array
```

> 🧠 **Mental Model:** `number[]` means "an array where every slot must be a number." TypeScript will stop you from accidentally putting a string in there.

### Tuples — Fixed-Length, Fixed-Type Arrays

A tuple is an array with a **fixed number of elements where each position has a specific type**. Unlike regular arrays, position matters.

```ts
// A tuple: [name, age, isAdmin]
type UserRecord = [string, number, boolean];

const alice: UserRecord = ["Alice", 30, true];  // ✅
const bad: UserRecord = [30, "Alice", true];     // ❌ Error: wrong order

// Destructuring works perfectly
const [name, age, isAdmin] = alice;
```

Optional tuple elements:

```ts
type Coordinate = [number, number, number?]; // x, y, optional z
```

Labeled tuple elements — great for readability:

```ts
type Range = [start: number, end: number];
```

> 🧠 **Real-world use:** React's `useState` hook returns a tuple: `[value, setter]`. That's why you destructure it as `const [count, setCount] = useState(0)`. TypeScript knows index 0 is the value and index 1 is the setter function.

* * *

## 8\. Enums

Enums let you define a **set of named constants** — a collection of related values with human-readable names.

### Numeric Enums

By default, TypeScript assigns numbers starting from 0:

```ts
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right, // 3
}

let move: Direction = Direction.Up;
console.log(move); // 0
```

> 🧠 **Mental Model:** A numeric enum is like a numbered menu. "Option 1 is Up, option 2 is Down..." The number is what gets stored, but you use the name in code.

### String Enums — Preferred in Most Cases

String enums are more readable in logs and debugging because you see the actual name, not a number:

```ts
enum Status {
  Active = "ACTIVE",
  Inactive = "INACTIVE",
  Pending = "PENDING",
}

let userStatus: Status = Status.Active;
console.log(userStatus); // "ACTIVE" — much clearer than 0
```

### When to Use Enums vs Union Types

```ts
// Enum approach
enum Role { Admin = "ADMIN", User = "USER", Guest = "GUEST" }

// Union type approach — often preferred for simpler cases
type Role = "ADMIN" | "USER" | "GUEST";
```

**When to use enums:**

- You need to iterate over all values
- Values are used heavily in `switch` statements
- You want to group related constants under a named namespace

**When to use union types:**

- Simple sets of string constants
- You prefer lighter syntax
- You don't need to iterate over the values

* * *

## 9\. Generics

Generics are one of TypeScript's most powerful features. They let you write **reusable, type-safe code that works with multiple types** — without sacrificing type safety.

### The Problem Generics Solve

Without generics, you face a dilemma:

```ts
// Option 1: Write a separate function for each type — lots of duplication
function getFirstNumber(arr: number[]): number { return arr[0]; }
function getFirstString(arr: string[]): string { return arr[0]; }

// Option 2: Use any — but you lose all type safety
function getFirst(arr: any[]): any { return arr[0]; }
// Now the return type is any — TypeScript can't help you anymore
```

Generics solve this elegantly.

### Generic Functions

The `<T>` is a **type parameter** — a placeholder that gets filled in when the function is called:

```ts
function identity<T>(value: T): T {
  return value;
}

// TypeScript fills in T based on what you pass
identity<string>("hello");  // T = string, returns string
identity<number>(42);       // T = number, returns number
identity("world");          // T inferred as string automatically
```

> 🧠 **Mental Model:** `T` is like a blank label on a box. When you put something in the box, the label gets filled in with the actual type. Now TypeScript knows what's in the box — and what will come out.

A more useful example:

```ts
function getFirst<T>(arr: T[]): T {
  return arr[0];
}

const firstNumber = getFirst([1, 2, 3]);         // type: number ✅
const firstName = getFirst(["Alice", "Bob"]);    // type: string ✅
```

### Generic Constraints

You can restrict what types `T` can be using `extends`:

```ts
// T must have a length property — so strings and arrays qualify, but numbers don't
function longest<T extends { length: number }>(a: T, b: T): T {
  return a.length >= b.length ? a : b;
}

longest("hello", "hi");       // ✅ strings have .length
longest([1, 2, 3], [1, 2]);  // ✅ arrays have .length
longest(10, 20);              // ❌ Error: numbers don't have .length
```

### Generic Interfaces & Types

Generics shine when used with interfaces — especially for API responses:

```ts
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

// Now every response is precisely typed
type UserResponse = ApiResponse<User>;
type PostsResponse = ApiResponse<Post[]>;

const response: UserResponse = {
  data: { id: 1, name: "Alice", email: "a@a.com", createdAt: new Date() },
  status: 200,
  message: "OK",
};
```

> 🧠 **Real-world use:** This pattern is everywhere in professional codebases. You define one generic API wrapper type, then reuse it for every endpoint. Change the wrapper once, it updates everywhere.

### Generic Classes

```ts
class Stack<T> {
  private items: T[] = [];

  push(item: T): void { this.items.push(item); }
  pop(): T | undefined { return this.items.pop(); }
  peek(): T | undefined { return this.items[this.items.length - 1]; }
}

const numberStack = new Stack<number>();
numberStack.push(1);
numberStack.push("hello"); // ❌ Error: string not assignable to number

const stringStack = new Stack<string>();
stringStack.push("hello"); // ✅
```

### Multiple Type Parameters

Functions and types can have more than one type parameter:

```ts
function pair<K, V>(key: K, value: V): [K, V] {
  return [key, value];
}

const entry = pair("name", "Alice"); // [string, string]
const idPair = pair(1, true);        // [number, boolean]
```

* * *

## 10\. Classes & OOP

TypeScript supercharges JavaScript classes with access modifiers, abstract classes, and more — bringing it closer to languages like Java or C#.

### Access Modifiers

Control who can access what:

```ts
class BankAccount {
  public owner: string;        // accessible anywhere (this is the default)
  private balance: number;     // only accessible inside this class
  protected accountId: string; // accessible in this class AND subclasses

  constructor(owner: string, initialBalance: number) {
    this.owner = owner;
    this.balance = initialBalance;
    this.accountId = Math.random().toString(36);
  }

  public deposit(amount: number): void {
    this.balance += amount;
  }

  public getBalance(): number {
    return this.balance; // controlled access to private data
  }
}

const account = new BankAccount("Alice", 1000);
account.owner;          // ✅ public — fine
account.balance;        // ❌ Error: private — can't access directly
account.getBalance();   // ✅ use the public method instead
```

> 🧠 **Mental Model:** Access modifiers are like doors in a building. `public` = no door, anyone can walk in. `private` = locked room, only the owner. `protected` = staff only (this class and its children).

### Constructor Shorthand

TypeScript has a shortcut to declare and initialize class properties directly in the constructor parameters:

```ts
// Verbose way
class User {
  public name: string;
  private email: string;
  constructor(name: string, email: string) {
    this.name = name;
    this.email = email;
  }
}

// Shorthand — TypeScript handles the rest automatically
class User {
  constructor(
    public name: string,
    private email: string,
    readonly id: number = Math.random()
  ) {}
}
```

Adding `public`, `private`, `protected`, or `readonly` in front of a constructor parameter tells TypeScript to automatically create and assign that property.

### Implementing Interfaces

Classes can "implement" interfaces, which **guarantees** the class has all the required properties and methods:

```ts
interface Serializable {
  serialize(): string;
  deserialize(data: string): void;
}

class UserModel implements Serializable {
  constructor(public name: string, public email: string) {}

  serialize(): string {
    return JSON.stringify({ name: this.name, email: this.email });
  }

  deserialize(data: string): void {
    const parsed = JSON.parse(data);
    this.name = parsed.name;
    this.email = parsed.email;
  }
}
```

> 🧠 **Mental Model:** `implements` is a promise. The class is saying "I promise I will have everything this interface requires." TypeScript holds it to that promise.

### Abstract Classes

Abstract classes **can't be instantiated directly** — they serve as blueprints for other classes:

```ts
abstract class Shape {
  abstract getArea(): number; // subclasses MUST implement this

  describe(): string {
    return `This shape has an area of ${this.getArea()}`;
  }
}

class Circle extends Shape {
  constructor(private radius: number) { super(); }

  getArea(): number {
    return Math.PI * this.radius ** 2;
  }
}

const shape = new Shape();    // ❌ Error: Cannot create an instance of an abstract class
const circle = new Circle(5); // ✅
circle.describe();            // "This shape has an area of 78.53..."
```

> 🧠 **Mental Model:** An abstract class is like a recipe template. You can't eat the template itself, but you can follow it to make a real dish. Each real dish (subclass) fills in the blanks.

### Getters & Setters

Getters and setters let you add logic when reading or writing a property:

```ts
class Temperature {
  private _celsius: number;

  constructor(celsius: number) {
    this._celsius = celsius;
  }

  // Getter — runs when you READ the property
  get fahrenheit(): number {
    return this._celsius * 9 / 5 + 32;
  }

  // Setter — runs when you WRITE the property, with validation
  set celsius(value: number) {
    if (value < -273.15) throw new Error("Below absolute zero!");
    this._celsius = value;
  }
}

const temp = new Temperature(100);
console.log(temp.fahrenheit); // 212 — no () needed, looks like a property
temp.celsius = -300;          // ❌ throws an error
```

* * *

## 11\. Type Narrowing & Type Guards

When a value has a **union type**, TypeScript requires you to narrow it to a specific type before using type-specific methods. TypeScript tracks your `if` statements and gets smarter as you check.

> 🧠 **Mental Model:** Imagine you receive a package labeled "could be a book or a laptop." Before you use it, you open the box and check. That moment of checking is narrowing — and TypeScript watches you do it.

### `typeof` Narrowing

```ts
function processInput(input: string | number) {
  if (typeof input === "string") {
    // ✅ TypeScript knows input is a string inside this block
    return input.toUpperCase();
  }
  // ✅ TypeScript knows input is a number here (the only remaining option)
  return input.toFixed(2);
}
```

### `instanceof` Narrowing

Use `instanceof` to narrow to a specific class:

```ts
function handleError(error: Error | string) {
  if (error instanceof Error) {
    console.log(error.message); // ✅ TypeScript knows it's an Error object
  } else {
    console.log(error);         // ✅ TypeScript knows it's a string
  }
}
```

### `in` Operator Narrowing

Use `in` to check if an object has a specific property:

```ts
interface Cat { meow(): void }
interface Dog { bark(): void }

function makeNoise(animal: Cat | Dog) {
  if ("meow" in animal) {
    animal.meow(); // ✅ TypeScript knows it's a Cat
  } else {
    animal.bark(); // ✅ TypeScript knows it's a Dog
  }
}
```

### Custom Type Guards (User-Defined)

Sometimes the built-in narrowing techniques aren't enough. You can write your own type guard — a function that tells TypeScript "if this returns true, the value is this specific type":

```ts
interface Admin { role: "admin"; permissions: string[] }
interface RegularUser { role: "user" }
type AppUser = Admin | RegularUser;

// The return type "user is Admin" is called a type predicate
function isAdmin(user: AppUser): user is Admin {
  return user.role === "admin";
}

function doSomething(user: AppUser) {
  if (isAdmin(user)) {
    console.log(user.permissions); // ✅ TypeScript knows user is Admin here
  }
}
```

### Discriminated Unions — The Gold Standard

The cleanest pattern for union types: add a shared `status` or `type` property with a **literal type** as a "tag" that uniquely identifies each variant.

```ts
interface LoadingState { status: "loading" }
interface SuccessState { status: "success"; data: User[] }
interface ErrorState   { status: "error"; error: string }

type RequestState = LoadingState | SuccessState | ErrorState;

function render(state: RequestState) {
  switch (state.status) {
    case "loading": return "Loading...";
    case "success": return state.data.map(u => u.name).join(", ");
    //                      ^^^^ TypeScript knows data exists here
    case "error":   return `Error: ${state.error}`;
    //                              ^^^^ TypeScript knows error exists here
  }
}
```

> 🧠 **Real-world use:** This pattern is perfect for API loading states, form states, and anything that goes through multiple stages. It makes impossible states unrepresentable.

* * *

## 12\. Utility Types

TypeScript ships with built-in **generic utility types** that transform existing types. These are used constantly in real projects — they save you from writing the same type transformations over and over.

> 🧠 **Mental Model:** Utility types are like tools in a workshop. You have your raw material (an interface), and these tools let you cut, shape, and combine it into what you need.

### `Partial<T>` — Make All Properties Optional

Useful when updating objects where you only want to change some fields:

```ts
interface User { id: number; name: string; email: string }

function updateUser(id: number, changes: Partial<User>) {
  // changes can have any subset of User's properties
}

updateUser(1, { name: "Bob" }); // ✅ email not required
```

### `Required<T>` — Make All Properties Required

The opposite of `Partial` — forces every property to be present:

```ts
interface Config { apiUrl?: string; timeout?: number }

type StrictConfig = Required<Config>;
// { apiUrl: string; timeout: number } — no more optionals
```

### `Readonly<T>` — Make All Properties Read-Only

Prevents mutation after creation — great for config objects:

```ts
const config: Readonly<{ apiUrl: string }> = { apiUrl: "https://api.example.com" };
config.apiUrl = "other"; // ❌ Error: cannot assign to read-only property
```

### `Pick<T, Keys>` — Keep Only Specific Properties

Cherry-pick just the properties you need from a larger type:

```ts
type UserPreview = Pick<User, "id" | "name">;
// Result: { id: number; name: string }
// email is gone — not needed for a preview
```

### `Omit<T, Keys>` — Remove Specific Properties

The opposite of `Pick` — exclude the properties you don't want:

```ts
type UserWithoutId = Omit<User, "id">;
// Result: { name: string; email: string }

// Very common pattern: create a "DTO" (Data Transfer Object) without auto-generated fields
type CreateUserDto = Omit<User, "id" | "createdAt">;
```

### `Record<Keys, Values>` — Create a Map of Keys to Values

Build an object type where you know the exact keys and their value type:

```ts
type RolePermissions = Record<"admin" | "user" | "guest", string[]>;

const permissions: RolePermissions = {
  admin: ["read", "write", "delete"],
  user:  ["read", "write"],
  guest: ["read"],
};
```

> 🧠 **Mental Model:** `Record` is like building a dictionary with typed entries. You specify exactly what keys are valid and what values they hold.

### `Exclude<T, U>` and `Extract<T, U>`

Filter members in or out of a union type:

```ts
type AllStatus = "active" | "inactive" | "pending" | "banned";

// Remove "banned" from the union
type SafeStatus = Exclude<AllStatus, "banned">;
// Result: "active" | "inactive" | "pending"

// Keep only the ones that match
type ActiveOnly = Extract<AllStatus, "active" | "pending">;
// Result: "active" | "pending"
```

### `NonNullable<T>` — Remove `null` and `undefined`

```ts
type MaybeString = string | null | undefined;
type DefiniteString = NonNullable<MaybeString>;
// Result: string — null and undefined are gone
```

### `ReturnType<T>` and `Parameters<T>`

Infer the types from existing functions — great when you don't control the source:

```ts
function fetchUser(id: number, includeDetails: boolean) {
  return { id, name: "Alice" };
}

type FetchUserReturn = ReturnType<typeof fetchUser>;
// Result: { id: number; name: string }

type FetchUserParams = Parameters<typeof fetchUser>;
// Result: [number, boolean]
```

* * *

## 13\. Modules & Namespaces

TypeScript uses the same ES module syntax as modern JavaScript, with full type support built in.

### Exporting Types

```ts
// types.ts
export interface User {
  id: number;
  name: string;
}

export type ID = string | number;

// Use "export type" to be explicit — this export disappears at runtime
// It's tree-shaking friendly and signals to other tools it's type-only
export type { User };
```

### Importing Types

```ts
// main.ts
import { User } from "./types";
import type { ID } from "./types"; // explicit type-only import (recommended)
```

> 🧠 **Why `import type`?** Regular `import` might include the value in the bundle. `import type` tells the compiler "this is only used for type checking — strip it completely from the output." It's cleaner and more intentional.

### Declaration Files (`.d.ts`)

These files contain **only type information** — no runtime code. You'll encounter them when using JavaScript libraries that don't have built-in TypeScript support:

```bash
npm install @types/express
```

This installs type declarations that tell TypeScript the shape of the Express library. You don't write these yourself — they're provided by the [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) community.

* * *

## 14\. Working with APIs & Async TypeScript

### Typing Promises

The generic `Promise<T>` describes what an async function will eventually return:

```ts
// This function returns a Promise that resolves to a User
async function fetchUser(id: number): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  const data = await response.json(); // data is 'any' by default
  return data as User;                // we assert the type we expect
}
```

### Typing `fetch` Responses

`response.json()` returns `any` — you need to tell TypeScript what shape you expect:

```ts
interface ApiUser {
  id: number;
  name: string;
  username: string;
  email: string;
}

async function getUser(id: number): Promise<ApiUser> {
  const res = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);

  if (!res.ok) {
    throw new Error(`HTTP error: ${res.status}`);
  }

  const data: ApiUser = await res.json(); // tell TS what we expect
  return data;
}
```

> ⚠️ **Important caveat:** The type annotation here is a promise to TypeScript — "trust me, this API returns an `ApiUser`." TypeScript can't verify this at runtime. If the API sends something unexpected, TypeScript won't save you. For real validation, use a library like Zod (see section 17).

### Error Handling with TypeScript

In TypeScript, caught errors are typed as `unknown` — because technically, anything can be thrown:

```ts
async function safelyFetch(url: string) {
  try {
    const res = await fetch(url);
    return await res.json();
  } catch (error: unknown) {
    // Must check before accessing properties
    if (error instanceof Error) {
      console.error(error.message); // ✅ safe
    } else {
      console.error("Unknown error occurred");
    }
  }
}
```

### Type Assertions (`as`)

Sometimes you know more than TypeScript does. Use `as` to tell TypeScript what type to treat a value as:

```ts
// TypeScript only knows this is HTMLElement | null — not specific
// We know it's an input, so we assert
const input = document.getElementById("username") as HTMLInputElement;
input.value; // ✅ now TS knows it has a .value property
```

Use type assertions sparingly — they override TypeScript's safety checks. If you're using them everywhere, it often means the types aren't set up properly upstream.

* * *

## 15\. TypeScript with React (Frontend)

### Component Props

Define an interface for your props, then use it on the component:

```ts
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: "primary" | "secondary" | "danger"; // only these three strings
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({
  label,
  onClick,
  variant = "primary",
  disabled = false,
}) => {
  return (
    <button className={`btn btn-${variant}`} onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
};
```

> 🧠 **Why this matters:** TypeScript will error if you use `<Button>` without the required `label` or `onClick` props, or if you pass `variant="purple"` (not in the union). Your component becomes self-documenting.

### `useState` with Types

TypeScript infers the type from the initial value most of the time:

```ts
const [count, setCount] = useState(0);   // inferred: State<number>
const [name, setName] = useState("");    // inferred: State<string>
```

When the initial value doesn't reveal the type (like `null`), be explicit:

```ts
const [user, setUser] = useState<User | null>(null);
const [items, setItems] = useState<string[]>([]);
```

### `useRef`

For DOM references, pass the element type as a generic:

```ts
const inputRef = useRef<HTMLInputElement>(null);

// Use optional chaining because the ref starts as null
inputRef.current?.focus();
```

### `useReducer`

The discriminated union pattern from section 11 works beautifully here:

```ts
type Action =
  | { type: "increment" }
  | { type: "decrement" }
  | { type: "reset"; payload: number };

function reducer(state: number, action: Action): number {
  switch (action.type) {
    case "increment": return state + 1;
    case "decrement": return state - 1;
    case "reset":     return action.payload;
    // TypeScript will warn you if you add a new action type and forget to handle it!
  }
}

const [count, dispatch] = useReducer(reducer, 0);
dispatch({ type: "increment" });
dispatch({ type: "reset", payload: 10 });
```

### Custom Hooks

Generic custom hooks are powerful — write once, use with any type:

```ts
function useFetch<T>(url: string) {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then((json: T) => setData(json))
      .catch((err: Error) => setError(err.message))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}

// Usage — T is inferred as User[]
const { data, loading } = useFetch<User[]>("/api/users");
```

### Event Handlers

React has specific event types for each interaction:

```ts
// Form submission
const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
  e.preventDefault();
};

// Text input changes
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  setValue(e.target.value);
};

// Button clicks
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {
  e.stopPropagation();
};
```

### Children Props

For components that wrap other content, use `React.ReactNode`:

```ts
interface CardProps {
  title: string;
  children: React.ReactNode; // accepts anything React can render
}

const Card = ({ title, children }: CardProps) => (
  <div className="card">
    <h2>{title}</h2>
    {children}
  </div>
);
```

* * *

## 16\. TypeScript with Node.js & Express (Backend)

### Setup

```bash
npm init -y
npm install express
npm install --save-dev typescript @types/node @types/express ts-node nodemon
```

> 🧠 **What are `@types/...` packages?** Most JavaScript libraries were written before TypeScript existed. The `@types` packages add TypeScript type definitions on top, so you get full autocomplete and type checking.

### Basic Express App

```ts
// src/index.ts
import express, { Request, Response, NextFunction } from "express";

const app = express();
app.use(express.json());

app.get("/", (req: Request, res: Response) => {
  res.json({ message: "Hello, TypeScript!" });
});

app.listen(3000, () => console.log("Server running on port 3000"));
```

### Typing Route Parameters & Body

Express's `Request` type is generic — you can tell TypeScript exactly what to expect:

```ts
// Route params — the :id in the URL
app.get("/users/:id", (req: Request<{ id: string }>, res: Response) => {
  const { id } = req.params; // TypeScript knows id is a string
  res.json({ id });
});

// Request body — what's sent in POST/PUT requests
interface CreateUserBody {
  name: string;
  email: string;
}

// Request<Params, ResBody, ReqBody, Query>
app.post("/users", (req: Request<{}, {}, CreateUserBody>, res: Response) => {
  const { name, email } = req.body; // fully typed!
  res.status(201).json({ name, email });
});
```

### Custom Middleware

Extend the `Request` type to carry custom data through your middleware chain:

```ts
interface AuthenticatedRequest extends Request {
  user?: { id: string; role: string };
}

const authMiddleware = (
  req: AuthenticatedRequest,
  res: Response,
  next: NextFunction
) => {
  const token = req.headers.authorization?.split(" ")[1];

  if (!token) {
    return res.status(401).json({ error: "Unauthorized" });
  }

  // After verifying, attach the user to the request
  req.user = { id: "123", role: "admin" };
  next();
};
```

### Environment Variables

Centralise and type your environment variables to avoid scattered `process.env` checks:

```ts
// config.ts
const config = {
  port: process.env.PORT ? parseInt(process.env.PORT) : 3000,
  dbUrl: process.env.DATABASE_URL ?? "",
  jwtSecret: process.env.JWT_SECRET ?? "default-secret",
  nodeEnv: process.env.NODE_ENV ?? "development",
} as const; // 'as const' locks down the types to their literal values

export default config;
```

* * *

## 17\. Common Patterns & Best Practices

### 1\. Always Use `strict` Mode

Enable all strict options in `tsconfig.json`. The short-term friction is worth the long-term safety — it catches null pointer errors, implicit `any`, and more.

### 2\. Avoid `any` — Use `unknown` Instead

```ts
// ❌ Bad — you lose all type safety
function parse(data: any) { return data.name; }

// ✅ Good — you verify before you use
function parse(data: unknown) {
  if (typeof data === "object" && data !== null && "name" in data) {
    return (data as { name: string }).name;
  }
}
```

### 3\. Use `as const` for Immutable Objects

Without `as const`, TypeScript widens string values to `string`. With it, values are narrowed to their exact literal types:

```ts
const ROUTES = {
  HOME: "/",
  ABOUT: "/about",
  DASHBOARD: "/dashboard",
} as const;

// ROUTES.HOME is typed as "/" (not just string)
// This makes it much safer to use in union comparisons
```

### 4\. The `satisfies` Operator (TypeScript 4.9+)

`satisfies` validates a value matches a type **without widening the type** — you get validation AND keep the precise inferred types:

```ts
type Palette = Record<string, string>;

// With 'as' — validation works, but you lose the specific keys
const colors = { red: "#ff0000", blue: "#0000ff" } as Palette;

// With 'satisfies' — validation works AND specific keys are preserved
const colors = { red: "#ff0000", blue: "#0000ff" } satisfies Palette;
colors.red.toUpperCase(); // ✅ TypeScript knows "red" is a valid key
colors.green;             // ❌ TypeScript knows "green" doesn't exist
```

### 5\. Prefer Discriminated Unions Over Optional Properties

Optional properties allow impossible states. Discriminated unions make impossible states unrepresentable:

```ts
// ❌ Bad — both data and error could be defined simultaneously, or both undefined
interface Result {
  data?: User;
  error?: string;
}

// ✅ Good — only one is possible at a time, and it's always clear which
type Result =
  | { success: true; data: User }
  | { success: false; error: string };
```

### 6\. Use Zod for Runtime Validation

TypeScript types disappear at runtime — they can't protect you from bad API responses or user input. Use a validation library to bridge the gap:

```ts
import { z } from "zod";

// Define the shape AND the validation rules
const UserSchema = z.object({
  name: z.string().min(1),
  email: z.string().email(),
  age: z.number().min(0).optional(),
});

// Derive the TypeScript type from the schema — no duplication!
type User = z.infer<typeof UserSchema>;

// Validate at runtime
const result = UserSchema.safeParse(req.body);
if (!result.success) {
  return res.status(400).json(result.error);
}
const user = result.data; // fully typed as User ✅
```

> 🧠 **Why this matters:** TypeScript protects you at compile time. Zod protects you at runtime. You need both to build reliable applications.

### 7\. Barrel Exports for Clean Imports

Group related exports through an `index.ts` file to keep imports tidy:

```ts
// types/index.ts
export type { User } from "./user";
export type { Post } from "./post";
export type { Comment } from "./comment";

// Elsewhere in your app — one clean import instead of three
import type { User, Post } from "./types";
```

* * *

## Quick Reference Card

```ts
// PRIMITIVES
let s: string, n: number, b: boolean, u: undefined, nl: null;

// SPECIAL
let a: any, uk: unknown, nv: never, v: void;

// FUNCTION
const fn = (x: number): string => String(x);

// OBJECT
interface Obj { key: string; optional?: number; readonly fixed: boolean }

// UNION (OR)
type U = string | number;

// INTERSECTION (AND)
type I = TypeA & TypeB;

// LITERAL TYPES
type Direction = "north" | "south" | "east" | "west";

// GENERIC
function id<T>(x: T): T { return x; }

// UTILITY TYPES
Partial<T>      // all properties optional
Required<T>     // all properties required
Readonly<T>     // all properties read-only
Pick<T, K>      // keep only keys K
Omit<T, K>      // remove keys K
Record<K, V>    // object with keys K, values V
NonNullable<T>  // removes null | undefined
ReturnType<T>   // return type of function T
Parameters<T>   // parameter types of function T

// TYPE NARROWING
typeof x === "string"
x instanceof ClassName
"property" in x

// REACT
useState<T>(initial)
useRef<HTMLInputElement>(null)
React.FC<Props>
React.ReactNode
```

* * *

> Happy coding! The best way to learn TypeScript is to write it every day. Start by adding types to an existing JavaScript project — let the compiler be your guide. Every red squiggly line is TypeScript teaching you something. 🚀
