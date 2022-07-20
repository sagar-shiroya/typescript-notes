# TypeScript

## What is Typescript?

- Open source programming language from Microsoft
- Superset of JavaScript
- Compile down to plain JavaScript

## Why TypeScript(Why not Dart or CoffeeScript or Plain Old JS)?

- Because of **its relation to JavaScript**(It’s just extended JavaScript). While Dart and CoffeeScript are new languages. You can rename the .js extension to .ts and it will work perfectly fine.
- Optional static typing and type interface. *[JS is a dynamically typed language so it doesn’t know the type until run-time. While TS on other hand identifies the type errors as soon as you type or compile it. Which results in less error-prone code. Specifying type is completely optional.]*
- IDE Support*[Intelesense support, refactoring the code easily. shows error straight away whenever it detects and shows red line underneath]*
- Rapid growth and use

## Setup Development Environment

1. Download and install the latest stable release of Node.js(check whether it’s installed or not by entering `node -v` in CLI
2.  Run the command `npm install -g typescript` (It will install TS globally)
3. Install VSCode IDE

---

## Hello World Program

- Create a file with **.ts** extension(`main.ts` in my case)
- Write a simple hello world program

```tsx
let message = 'Hello World';
console.log(message);
```

- Once written, we need to compile it in CLI by writing `tsc main.ts` **or** `tsc main`
- It will transpile your .ts file to a javascript file
- To run the code, we can use a node. Run `node main.js` It will give you **Hello World** as an output.

You have noticed that the message variable here in .ts file has a red line error underneath and if you hover, you will get a message saying **Cannot redeclare block-scoped variable ‘message’**

It’s happening because the file is treated as a script rather than a module. A module has its own scope, but a script has global scope. To get rid of this, we need to add an empty export statement.

```tsx
export {}
let message = 'Hello World';
console.log(message);
```
