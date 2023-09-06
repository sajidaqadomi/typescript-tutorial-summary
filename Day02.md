## Function Type Annotations
### Function Documentation

In addition to the JavaScript syntaxes for commenting, such as “// single line” or “/* multi-line */”, TypeScript uses a third type called documentation comments “/** doc comments */”, which written directly before a function. They are primarily used to provide a brief description of what the function does, its parameters (using @param), and its return value (using @return).

```javascript
/**
 * DOCUMENTATION COMMENTS FOR FUNCTION NICKNAME
 * Combines two strings to create a nickname
 * 
 * @param str1 - The first input string
 * @param str2 - The second input string
 * @return String message with nickname
 *
 */
function nickName(str1: string, str2: string): string {
  return `Your nickname is: ${str1 + str2}`;
}
let yourNickName = nickName('Pizza', 'Lover')  
console.log(yourNickName) //-> "Your nickname is: PizzaLover"
```
### Parameter Type Annotations
![](https://raw.githubusercontent.com/sajidaqadomi/images/main/Parameter.webp)
![](https://raw.githubusercontent.com/sajidaqadomi/images/main/ParameterError.webp)

In the example above, the string “five” is not a number so TS will pick up and bar its function call.
### Optional & Default Parameters

**Optional  Parameter**
Sometimes in certain use cases for functions, we do not wish to give an argument but still maintain the parameter type. This can be accomplished by simply putting a “?” after parameter name and before the semicolon (:).

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/DefaultParameters.webp)
![](https://raw.githubusercontent.com/sajidaqadomi/images/main/DefaultParametersResult.webp)

**Default Parameters**
When a parameter is initialized with a default argument (value), TypeScript will do its magic and assign the default value’s type to be the parameter’s type. This is just like the type inferences we saw for variables.

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img5.webp)

Running the code above produces,

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img6.webp)

However, if we input a string, then TS will throw an error.

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img7.webp)
![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img8.webp)
### Return Types

Outside security is not enough. There can be trouble brewing inside as well — TypeScript’s got it covered. Again, TS can infer the return type of a function by simply looking at its return statement.

In this example, the function shouldBeStr() takes in a string argument and returns a string. TS infers that it should return a string. When the variable check is assigned a different data type (e.g., boolean) and tried to set its value to the shouldbeStr(‘yes’), TS throws an error.

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img9.webp)

TypeScript also allows for explicit return types in functions, which can be specified by typing the data type after the “:” trailing the parentheses housing the parameter (red). Explicit return types can also be written using the arrow function syntax (green).

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img10.webp)

The **void return type** is used when a function does not return anything. Even though TS will not throw any error if void is not specified, it is customary to specify a return type for functions. Type any can be used in this case as well.

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img11.webp)

> The return value of a void function is intended to be ignored

**We could type functions as returning undefined, but there are some interesting differences that highlight the reason for void’s existence:** 👎

```javascript
function invokeInFourSeconds(callback: () => undefined) {
  setTimeout(callback, 4000)
}
function invokeInFiveSeconds(callback: () => void) {
  setTimeout(callback, 5000)
}
 
const values: number[] = []
invokeInFourSeconds(() => values.push(4)) //❌Type 'number' is not assignable to type 'undefined'.
invokeInFiveSeconds(() => values.push(4)) //✅
```

It happens that Array.prototype.push returns a number, and our invokeInFourSeconds function above is unhappy about this being returned from the callback.

### Void Data Type

In the following example, `someFunc1` **does not have a return statement**. 

`someFunc2` **does have a return statement** but **does not return anything.**

In such cases, the Typescript infers the type as void.

```javascript
function someFunc1() {    //Inferred return is Void
}
 
 
function someFunc2() {      //Inferred return is Void
    return
}
 
 
// You can also annotate the return type explicitly to void.

function someFunc(): void {
}
 
```

> Nothing is assignable to void `except` for **void, undefined, null, any & never.**  You can assign **null to void** **only** if `strictNullChecks` is set to `false` in `tsconfig.json`

```javascript
let a:void
a=undefined    //No Error
```

You cannot assign any other value to it. It will throw a Type is not assignable to type ‘void’ error.

```javascript
a:void
a="test"       //Type 'string' is not assignable to type 'void'.
```

But you cannot assign void to undefined

```javascript
let a:undefined;
let b:void;
 
b=a;        //ok 
 
a=b;        //Type 'void' is not assignable to type 'undefined'
```

Functions in JavaScript return undefined if they do not return any values.

```javascript
function someFunc() {    
}
 
let a = someFunc()    
console.log(a)    //undefined
```

To assign null, first, make the `strictNullChecks` **false** in `tsconfig.ts`. Remember that making it false is not a recommended practice.
```
{
    "compilerOptions": {
      "strictNullChecks": false
    },
}
```
 
```javascript
let a:void
a=null    //ok
```

**Vs Any**

You can also assign variable of any type to a void variable.

A variable of any type can be assigned to anything. This is because the compiler switches type checking when any is involved.

**Void Vs Never**

The never type looks very similar to void.

We use void when the function does return but does not return a value. The typescript infers the return value as void.

✅In the following example, the arrow function does not return anything. But it does finish and return the control to back to the main program. The Typescript `infers the return type as void`.

```javascript
let z = (a:number, b:number) => {
  let c=a+b;
}
```

The Typescript infers the return type as never if a function expression or arrow function.

1. has no return type annotation
1. has no return statement
1. Or has a return statement which returns never
1. does not have an endpoint

**(for function declarations void is the default return type)**
 
In the following examples, TypeScript infers the return type as never.

```javascript
let z = function infiniteLoop() {
 while (true) {
 }
}


let x1 = function (message):void { 
  throw new (message);
};
```

The void type can have undefined or null as a value whereas never cannot have any value.

**Never Type in Function Declaration**

In the example below, all functions throw errors. The function f & g are function expressions. TypeScript correctly infers the type as never. But the last function h is a function declaration where the type is inferred as void.

 ```javascript
//inferred as never
let f = () => {
    throw new Error("Should never get here");
}
 
//inferred as never
let g = function() { 
    throw new Error("Should never get here");
}
 
//inferred as void
function h() { 
    throw new Error("Should never get here");
}
```

This is because of backward compatibility 🔥🔥

**Note**💁‍♀️
- You can assign Never to every other type.✅
- But you cannot assign any other type to never (except never itself).❌
 
**Void as a function parameter**

You can use void as the function parameter. The only valid values that you can pass are void, undefined & null (strictNullChecks is set to false in tsconfig.json)

```javascript
function someFunc(x:void) {
 
}
 
 
someFunc()              //ok
someFunc(undefined)     //ok
 
someFunc(null)          //ok if strictNullChecks=false
``` 
 
The underlying JavaScript neither has a data type void nor value.

The void data type can hold only one value, i.e., undefined (or null if the strictNullChecks compiler option is off). That is because JavaScript returns a value undefined when the function returns no value.

**[Reference](https://www.tektutorialshub.com/typescript/void-data-type-in-typescript/#void-vs-undefined)**
### 
