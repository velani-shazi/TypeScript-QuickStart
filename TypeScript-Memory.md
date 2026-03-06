# Copy-by-Value vs Copy-by-Reference in TypeScript

Understanding this is one of the most important mental models for debugging and writing predictable code.

**TypeScript does not change JavaScript's runtime behavior** — it only adds types. So this concept comes from **JavaScript memory behavior**.

---

## 1. The Two Ways Values Exist in Memory

In TypeScript there are **two categories of values**:

| Category | Stored As | Example Types |
|----------|-----------|---------------|
| **Primitive values** | Actual value | `number`, `string`, `boolean`, `null`, `undefined`, `symbol`, `bigint` |
| **Objects** | Reference (memory address) | `object`, `array`, `function`, `class`, `Map`, `Set` |

When you assign variables:

- **Primitives → copied by value**
- **Objects → copied by reference**

---

## 2. Copy by Value (Primitives)

Primitives store the **actual data** inside the variable. When you assign them, a **new copy** is created.

```ts
let a = 10
let b = a

b = 20

console.log(a) // 10
console.log(b) // 20
```

What happened in memory:

```
a → 10
b → 10
```

After changing `b`:

```
a → 10
b → 20
```

`a` stays unchanged because **b received a copy**.

---

## 3. Copy by Reference (Objects)

Objects are stored **in heap memory**, and variables store a **reference (pointer)** to that object. When you assign them, you copy the **reference**, not the object.

```ts
let user1 = { name: "Alice" }

let user2 = user1

user2.name = "Bob"

console.log(user1.name) // Bob
console.log(user2.name) // Bob
```

What happened in memory:

```
user1 ──┐
        ├──► { name: "Alice" }
user2 ──┘
```

After mutation:

```
{ name: "Bob" }
```

Both variables point to the **same object**.

---

## 4. The Rule That Confuses Everyone

Even though objects are **reference types**, the **reference itself is copied by value**.

```
variable → reference → object
```

When you assign `let b = a`, you copy the **reference value**, not the object. So the reference now points to the **same memory location**.

---

## 5. Arrays Behave the Same Way

Arrays are **objects**, so they are also reference types.

```ts
let arr1 = [1,2,3]
let arr2 = arr1

arr2.push(4)

console.log(arr1) // [1,2,3,4]
```

Memory:

```
arr1 ──┐
       ├──► [1,2,3]
arr2 ──┘
```

After push:

```
[1,2,3,4]
```

---

## 6. Reassigning vs Mutating

### Mutating an object

```ts
let obj1 = { x: 1 }
let obj2 = obj1

obj2.x = 5
```

Both change — they share the same reference.

### Reassigning a variable

```ts
let obj1 = { x: 1 }
let obj2 = obj1

obj2 = { x: 5 }
```

Memory becomes:

```
obj1 ───► { x: 1 }
obj2 ───► { x: 5 }
```

Because you changed the **reference**, not the object.

---

## 7. Function Arguments

Function parameters follow the **same rule**.

### Primitive example

```ts
function change(x: number) {
  x = 50
}

let a = 10
change(a)

console.log(a) // 10
```

Because primitives are **copied by value**.

### Object example

```ts
function change(user: {name: string}) {
  user.name = "Bob"
}

let user = { name: "Alice" }

change(user)

console.log(user.name) // Bob
```

Because the **reference is copied**, but still points to the same object.

---

## 8. The "Pass-by-Value" Truth

Technically JavaScript is **always pass-by-value**. But:

| What is passed | What gets copied |
|----------------|------------------|
| Primitive | actual value |
| Object | reference value |

So people say primitives are pass-by-value and objects are pass-by-reference — but technically, **everything is pass-by-value**. Objects just pass a **reference value**.

---

## 9. Shallow Copy vs Deep Copy

Sometimes you want a **new object** instead of sharing the reference.

### Shallow copy

```ts
let user1 = { name: "Alice" }
let user2 = { ...user1 }
```

```
user1 ─► { name: "Alice" }
user2 ─► { name: "Alice" }
```

Different objects. But **nested objects still share references**:

```ts
let obj1 = {
  name: "Alice",
  address: { city: "Paris" }
}

let obj2 = { ...obj1 }

obj2.address.city = "London"

console.log(obj1.address.city) // London
```

Because spread does a **shallow copy** only.

---

## 10. Deep Copy

To fully clone an object:

```ts
let clone = structuredClone(obj)
```

Or alternatively:

```ts
let clone = JSON.parse(JSON.stringify(obj))
```

Now all nested objects are completely separate.

---

## 11. The Mental Model That Makes Everything Click

Think of variables like **labels pointing to boxes**.

### Primitives — separate boxes

```
a → 10
b → 10
```

### Objects — same box

```
a → address 0x123 → { name: "Alice" }
b → address 0x123 → { name: "Alice" }
```

---

## 12. Common Bugs Caused By This

### Bug 1: Unexpected mutation

```ts
const defaults = { theme: "dark" }
const settings = defaults

settings.theme = "light"
// defaults.theme is now "light" too
```

### Bug 2: Array mutation

```ts
const original = [1,2,3]
const copy = original

copy.push(4)
// original is now [1,2,3,4] too
```

---

## 13. When You Must Copy

Always copy when:

- updating **React state**
- working with **Redux**
- avoiding side effects
- writing **functional code**

```ts
const newArray = [...oldArray]
const newObject = { ...oldObject }
```

---

## 14. Summary Table

| Type | Copy Behavior |
|------|---------------|
| `number` | value |
| `string` | value |
| `boolean` | value |
| `null` | value |
| `undefined` | value |
| `symbol` | value |
| `bigint` | value |
| `object` | reference |
| `array` | reference |
| `function` | reference |
| `class instance` | reference |

---

## The One Sentence Rule

> **Primitives copy the value. Objects copy the reference.**
