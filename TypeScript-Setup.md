# TypeScript Playground Setup Guide

This guide shows how to create a **simple TypeScript workspace** where you can write `.ts` files, compile them to JavaScript, and run them with Node.js.
It is ideal for **learning TypeScript, testing snippets, and practicing concepts** like generics, types, and algorithms.

---

## 1. Create the Project Folder

Create a new folder for your TypeScript playground.

```bash
mkdir typescript-playground
cd typescript-playground
```

---

## 2. Initialize a Node.js Project

Initialize the project to generate a `package.json` file.

```bash
npm init -y
```

This file manages project dependencies and scripts.

---

## 3. Install TypeScript

Install TypeScript and Node type definitions as development dependencies.

```bash
npm install -D typescript @types/node
```

Explanation:

- `typescript` → TypeScript compiler
- `@types/node` → Type definitions for Node.js APIs

---

## 4. Create a TypeScript Configuration File

Initialize the TypeScript configuration.

```bash
npx tsc --init
```

Modify the generated `tsconfig.json` to the following simplified configuration:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "rootDir": "./src",
    "outDir": "./dist",
    "strict": true
  }
}
```

Explanation of key options:

| Option | Purpose |
|--------|---------|
| `target` | JavaScript version to compile to |
| `module` | Module system used by Node.js |
| `rootDir` | Location of TypeScript source files |
| `outDir` | Location of compiled JavaScript |
| `strict` | Enables strict type checking |

---

## 5. Create the Source Folder

Create a folder to store TypeScript files.

```bash
mkdir src
touch src/index.ts
```

Your project structure should now look like this:

```
typescript-playground
│
├── src
│   └── index.ts
│
├── dist
├── package.json
└── tsconfig.json
```

---

## 6. Write Your First TypeScript Program

Open `src/index.ts` and add the following code:

```ts
function greet(name: string): string {
  return `Hello ${name}`;
}

console.log(greet("Menzi"));
```

This function:

- Accepts a `string` parameter
- Returns a `string`
- Logs the result to the console

---

## 7. Compile the TypeScript Code

Compile the TypeScript files into JavaScript.

```bash
npx tsc
```

The compiled output will be placed in the `dist` folder:

```
dist/index.js
```

---

## 8. Run the Program

Execute the compiled JavaScript file with Node.js.

```bash
node dist/index.js
```

Expected output:

```
Hello Menzi
```

---

## 9. Faster Development Workflow (Optional)

Instead of compiling manually each time, you can run TypeScript directly using `ts-node`.

Install it:

```bash
npm install -D ts-node
```

Run TypeScript directly:

```bash
npx ts-node src/index.ts
```

This allows you to execute `.ts` files without compiling first.

---

## 10. Add Useful Scripts

You can simplify commands by adding scripts to `package.json`:

```json
"scripts": {
  "build": "tsc",
  "run": "node dist/index.js",
  "dev": "ts-node src/index.ts"
}
```

Now you can run:

```bash
npm run dev
```

This will execute the TypeScript file directly.

---

## Final Project Structure

```
typescript-playground
│
├── src
│   └── index.ts
│
├── dist
│   └── index.js
│
├── package.json
└── tsconfig.json
```

---

## Summary

This setup provides a lightweight TypeScript environment where you can:

- Write TypeScript code
- Compile it to JavaScript
- Run it with Node.js
- Quickly experiment with TypeScript features

It is perfect for learning concepts such as:

- Type annotations
- Interfaces
- Generics
- Utility types
- Algorithms and data structures
