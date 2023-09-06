## What is TypeScript? 📃

 > TypeScript is an open source, typed syntactic superset of JavaScript
 
 ✅  Compiles to readable JS
 ✅ Three parts: Language, Language Server and Compiler.
 ✅  It allows you, as a code author, to leave more of your intent “on the page”
 
 This kind of intent is often missing from JS code. For example:
 
 ```javascript
 function add(a, b) {
  return a + b
}
 ```
 
 Is this meant to take numbers as args? strings? both?

What if someone who interpreted a and b as numbers made this “backwards-compatible change?”

```javascript
function add(a, b, c = 0) {
  return a + b + c
}
```

We’re headed for trouble if we decided to pass strings in for a and b!

Types make the author’s intent more clear

```javascript
function add(a: number, b: number): number {
  return a + b
}
add(3, "4") //❌   Argument of type 'string' is not assignable to parameter of type 'number'.

```

💡**It has the potential to move some kinds of errors from runtime to compile time**

---

## Using tsc and compiling TS code into JavaScript

Let’s consider your TypeScript project that consists of only three files:

- package.json   # Package manifest
- tsconfig.json  # TypeScript compiler  settings
- src/index.ts   # "the program"

**package.json (view source)**

{
  "name": "hello-ts",
  "license": "NOLICENSE",
  "devDependencies": {
    "typescript": "^4.3.2"
  },
  "scripts": {
    "dev": "tsc --watch --preserveWatchOutput"
  }
}
Note that…

We just have one dependency in our package.json: typescript.
We have a dev script (this is what runs when you invoke yarn dev-hello-ts from the project root)

It runs the TypeScript compiler in “watch” mode (watches for source changes, and rebuilds automatically).
The following is just about the simplest possible config file for the TS compiler:

**tsconfig.json (view source)**

{
  "compilerOptions": {
    "outDir": "dist", // where to put the TS files
    "target": "ES3" // which level of JS support to target
  },
  "include": ["src"] // which files to compile
}
All of these things could be specified on the command line (e.g., tsc --outDir dist), but particularly as things get increasingly complicated, we’ll benefit a lot from having this config file:

### Running the compiler

`yarn dev`

You should see something in your terminal like:

`12:01:57 PM - Starting compilation in watch mode...`
Note that within the “hello-ts” project

a ./dist folder has appeared,
inside it is an index.js file.

## Statically Typed VS  Dynamically Typed Language

**Statically Types**
- Varibles Are Static, Once You declare it you cannot  change
- variables Types are  known at compile-time instead of at run-time
- Static typing usually results in compiled code that executes more quickly because when the compiler knows the exact data types that are in use, it can produce optimized machine code (i.e. faster and/or using less memory).
- Error Detected Earlier
-  Common examples of statically-typed languages include Java, C, C++,Typescript FORTRAN, Pascal and Scala

In Statically typed languages, once a variable has been declared with a type, it cannot ever be assigned to some other variable of different type and doing so will raise a type error at compile-time(some IDE’s generally shows a Red Cross mark denoting the error).

**Dynamically Typed**

- type of a variable is checked during run-time
-  it is possible to bind the same variables to objects of different types during the execution of the program
- Error can be Detected After Execution
-  Common examples of dynamically-typed languages includes JavaScript, Objective-C, PHP, Python, Ruby, Lisp, and Tcl.
--

## Type Annotations And Data Type 

We can specify the type of the variables, function parameters and object properties. We can specify the type using `:Type` after the name of the variable, parameter or property. There can be a space after the colon. TypeScript includes all the primitive types of JavaScript- number, string and boolean

```typescript
var age: number = 32; // number variable
var name: string = "John";// string variable
var isUpdated: boolean = true;// Boolean variable
```

In the above example, each variable is declared with their data type. These are type annotations. You cannot change the value using a different data type other than the declared data type of a variable. If you try to do so, TypeScript compiler will show an error. This helps in catching JavaScript errors. For example, if you assign a string to a variable age or a number to name in the above example, then it will give an error.

**The following example demonstrates the type annotation of paramters.**

```typescript
function display(id:number, name:string)
{
    console.log("Id = " + id + ", Name = " + name);
}
```

**Declare an object with inline annotations for each of the properties of the object.**

```typescript
let employee : { 
    id: number; 
    name: string; 
}; 

employee = { 
  id: 100, 
  name : "John"
}
```
---

Variables and simple values
Objects and arrays
--- BREAK ---
Categorizing type systems
Set theory, Union and Intersection types
Interfaces and Type Aliases
--- LUNCH ---
Hack: Writing types for JSON values
Functions
Classes in TypeScript
Top and bottom types
User-defined Type guards
--- BREAK ---
Handling nullish values
Generics
Hack: higher-order functions for dictionaries
Wrap up

## Type annotation for arrays 

Type annotation for arrays can be assigned by simply putting a set of square brackets “[ ]” after the element type. Another syntax that can be used is Array<type>. Here are some examples:

```typescript
let nums1: number[] = [1, 2, 3, 4, 5];
let nums2: Array<number> = [6, 7, 8, 9, 10];
```

## Type annotation Multi-Dimensional Arrays

Multi-dimensional arrays, meaning an array of arrays, can be declared by simply adding another set of square brackets “[ ]” to the original syntax.

```javascript
let nums: number[][] = [ [1, 2, 3], [4, 5, 6], [7, 8, 9] ]; 
```

📃**note:**

> The empty array “[ ]” will not cause errors when assigned to any array type.

// No errors for the following:

```javascript
let nums: number[] = [];
let strings: string[] = [];
let booleans: boolean[] = [];
```

## Tuples

Arrays can have multiple data types as elements. A tuple is a data structure with specified length and order of data types for its elements. While there is no default tuple in JavaScript, leave it for TypeScript to “type” it up. Tuple types are annotated with an array of data types in a specific order.

```typescript

/* 
  tuple of length 4 contains a number, string, boolean, and number
  in that order specific order
*/
let tuple: [number, string, boolean, number] = [ 23, 'string', true, 32 ];

```

TypeScript `throws errors` when incorrect data types are assigned in the specified order and when the length is not exact.

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*_yVT6mY3JCWbxcj4bRUp5A.png)

**Limitations**

As of TypeScript 4.3, there’s limited support for enforcing tuple length constraints.

For example, you get the support you’d hope for on assignment:

```javascript
const numPair: [number, number] = [4, 5, 6]
```

> Type '[number, number, number]' is not assignable to type '[number, number]'.
Source has 3 element(s) but target allows only 2.


but **not** around `push` and `pop`:

```javascript
const numPair: [number, number] = [4, 5]
numPair.push(6) // [4, 5, 6]
numPair.pop() // [4, 5]
numPair.pop() // [4]
numPair.pop() // []
````

## Summary 🗒️💁‍♀️

Array types can be declared after variable name with a type followed by square bracket “[ ]”, e.g., string[ ] or Array<string>.

Multi-dimensional array (an array of arrays) types are type annotated with an additional square bracket, e.g., number[ ][ ].

Tuple types have specified length and order of data types for its elements, e.g., [ number, string, boolean ].

Array types can be inferred as well. When an array that contains uniform data type is declared ( e.g, let nums = [1,2,3] ), TypeScript infers that it is an array type — number[ ] as opposed to a tuple type — [number, number, number].

Rest parameter can be annotated as a specific type with an array type syntax. Spread syntax can be used to refactor code for functions that take in a lot of parameters.
