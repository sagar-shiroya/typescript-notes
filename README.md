# TypeScript

## What is Typescript?

- Open source programming language from Microsoft
- Superset of JavaScript
- Compile down to plain JavaScript

## Why TypeScript(Why not Dart or CoffeeScript or Plain Old JS)?

- Because of **its relation to JavaScript**(It’s just extended JavaScript). While Dart and CoffeeScript are new languages. You can rename the .js extension to .ts and it will work perfectly fine.
- Optional static typing and type interface. *[JS is a dynamically typed language so it doesn’t know the type until run-time. While TS on other hand identifies the type errors as soon as you type or compile it. Which results in less error-prone code. Specifying type is completely optional.]*
- IDE Support *[IntelliSense support, refactoring the code easily. shows error straight away whenever it detects and shows red line underneath]*
- Rapid growth and use

## Environment Setup

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

> In order to automatically recompile TS file whenever there’s a change, we can use watch option. `tsc main --watch`
> 

## Variable Declaration

Unlike traditional javascript, TS encourages to use the **let** and **const** keywords. It supports block level scoping.

Javascript has only **global scope** and **function scope**. There’s no block level scope.

It’s not giving an error for redeclaring the same variable using var. But let and const solve this problem. It will give you an error for redeclaration. 

```tsx
let x = 10;
const y = 20;
let x = 30; 
//This will give an error that **Cannot redeclare** **block-scoped variable 'x'**
```

### Difference between let and const

- let declaration can be done without initialization, while const declaration are always initialize with values. Const declaration once assigned, it can never be reassigned different value.

```tsx
let sum;
const title; //Error: const declaration 'title' must be initialized
```

- If you feel variable never change its value over course of program then go with const declaration, if not then go with let declaration. For e.g. in above code block you can see that, sum of two variables can be changes, but title never change.

```tsx
let sum;
const title = "Typescript Notes";
```

## Variable Types(Essence of TypeScript)

Below are the basic types in TS:

- boolean
- number
- string

```tsx
//Variable Declaration with type
let isPassed: boolean = true;
let total: number = 20;
let name: string = 'Sagar';
```

**Template String:** It can be having multiple lines and have embedded expressions.

```tsx
let sentence: string = `My name is ${name}
I am learning TypeScript`;
console.log(sentence);
```

### Usage of variable type

- Static type checking 
*[When we assign string value to boolean type variable, it is straight away give an error and viceversa]*

```tsx
let name: string = 'Sagar';
name = true; //Type 'boolean' is not assignable to type 'string'.
```

- Accurate IntelliSense
*[When you have type string for variable and in IDE if you start typing that variable e.g. name. then you will start get suggestions for all function application to name type]*

![Untitled](TypeScript%200503d8c3ebe44afb94e32cda25111280/Untitled.png)

**Two more types of variable**

- null
- undefined

```tsx
let n: null = null;
let u: undefined = undefined;
```

These are not much of use. That’s why in TS, null and undefined are classified as subtypes of all other types. So you can assign null or undefined to bool, string or number type variable.

```tsx
//Below code works perfectly fine.
let isNew: boolean = null;
let myName: string = undefined;

let isNew: boolean|null = null;
let myName: string|undefined = undefined;
```

### Declaring array type

```tsx
let list1: number[] = [1,2,3];
let list2: Array<number> = [1,2,3];
```

Both the syntax are similar, there’s no advantage of one syntax over another.

**Array of mixed type**

```tsx
let person1:[string,number] = ['Chris',22]
```

Note: order is matter in above type declarations.

## Enum Type

It’s for giving more friendly name to numeric values.

```tsx
enum Color {
	Red,
	Green,
	Blue
}

let c: Color = Color.Green;
console.log(c);
```

### Any Type

If you’re unsure about what variable type would be then use any type.

```tsx
let randomValue: any = 10;
randomValue = "Sagar";
```

Note: It’s helpful whenever we are migrating from JS to TS.

For any type TS doesn’t throw any error while accessing it any way like below:

```tsx
let myVariable: any = 10;
console.log(myVariable.name);
myVariable(); //JS may throw an error as it'll not find any function with this name defined
myVariable.toUpperCase();
```

### Unknown type

To tackle above issue, TS 3.0 has introduced new type as “unknown”. You cannot access any property of unknown type nor you can construct them.

```tsx
let myVar: unknown = 10;
myVar.toUpperCase();
```

In order to prevent that error in unknown type, you’ve to type cast the variable. So TS assumes we made necessary check.

```tsx
let myVar: unknown = 10;
(myVar as string).toUpperCase();
```

## Type Inference

TypeScript infers types of variables when there is no explicit information available in the form of type annotations.

```tsx
let b = 10;
b = false;
```

First line assign type number to b and when you assign boolean it will give you an error. So if TS is automatically gives type then why to give explicitly?

Because it’s only work when you define it with initialization. For below code, it will not work and not give any error.

```tsx
let b;
b = 10;
b = false;
```

### Multi type Variable

```tsx
let multiType: string | number;
multiType = 'A';
multiType = 20;
```

**What is difference between any type and multi type/union type?**

→ union type restrict to specific type where as any type has no restrictions.

→ There’s no IntelliSense support for any type, but it will be there for union type. 

---

## Functions

```tsx
//Normal JS Function
function add(num1, num2){
	return num1 + num2;
}
add(5,10)
add('a','b');

//TypeScript Function with type parameters
function addNumber(num1: number, num2: number){
	return num1 + num2;
}
addNumber(5,10)
addNumber(5,'A'); //This will give an error

// Function parameter type with return type
function addNum(num1:number, num2:number):number {
	return num1 + num2;
}
```

In TS, all the parameters is assumed to be required by the function. But in plain JS, it will be possible to call add() without parameter. In that case parameter will receive a value as undefined.

**Optional Parameters**

```tsx
// ? here declare num2 as optional parameter
function sub(num1: number, num2?:number) : number{
	if(num2)
		return num1-num2;
	else
		return num1;
}
sub(5); //second paramter will be treated as undefined and return only 5
```

Optional parameters should always be after required parameters.

**Default Parameters**

```tsx
function add(num1:number, num2:number = 10):number{
	return num1 + num2;
}
add(10,20); //30
add(5); //15 
```

---

## Interface

It is possible to specify an object as type in TypeScript.

```tsx
function fullName(person:{firstName:string, lastName:string}){
	console.log(person.firstName + ' ' + person.lastName);
}

let p = {
	firstName: 'Sagar',
	lastName: 'Shiroya' 
};

fullName(p);
```

In above example, imagine a function declaration where object has 5-10 different properties. 

In that case, we will define interface and use that interface as type in function and that can be reusable.

```tsx
interface Person{
	firstName: string,
	lastName: string
}
function fullName(person: Person){
	console.log(`${person.firstName} ${person.lastName}`);
}
```

We can also have optional property in case of interface the same was optional parameter by using `?`

```tsx
interface Person{
	firstName: string,
	lastName?: string
}
```

---

## Class and Access Modifiers

```tsx
class Employee {
	employeeName: string;

	constructor(name: string){
		this.employeeName = name;
	}

	greet(){
		console.log(`Good Morning ${this.employeeName}`);
	}
}

let emp1 = new Employee('Sagar');
console.log(emp1.employeeName);
emp1.greet();
```

Because of classes, it’s possible to have class based inheritance.

```tsx
class Manager extends Employee {
    constructor(managerName:string){
        super(managerName);
    }
    delegateWork(){
        console.log(`Manager delegating tasks`);
    }
}

let m1 = new Manager('Bruce');
m1.greet();
console.log(m1.employeeName);
```

If you can see in IDE, by putting `m1.` then it will give you suggestion of own as well as parent methods.

![Untitled](TypeScript%200503d8c3ebe44afb94e32cda25111280/Untitled%201.png)

### Access Modifiers

Access modifiers are keywords that sets the accessibility of methods and member variables

- public
- protected
- private

By default each class member is public. So we can freely access them throughout the program.

```tsx
class Employee {
	private employeeName: string;

	constructor(name: string){
		this.employeeName = name;
	}

	greet(){
		console.log(`Good Morning ${this.employeeName}`);
	}
}
let m1 = new Manager('Bruce');
console.log(m1.employeeName); //Give an error as employeeName is private

//Private property can't even accessible from derived class
class Manager extends Employee {
    constructor(managerName:string){
        super(managerName);
    }
    delegateWork(){
        console.log(`Manager delegating tasks ${this.employeeName}`); //This will error out, to fix this change private to protected
    }
}
```
