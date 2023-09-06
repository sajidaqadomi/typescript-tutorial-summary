## Interface

The Interface in TypeScript defines the Shape of an object. i.e. it specifies what properties & methods a given object can have and their corresponding value types. TypeScript interfaces are abstract types. They do not contain any code. An object, function, or class that implements the interface must implement all the properties specified in the interface.

### Creating an interface
The following IProduct interface defines the three properties and a method. Note that the interface doesn’t initialize nor implement the properties. It does not contain any code.

```javascript
interface IProduct { 
   id:number, 
   name:string, 
   price:number,
   calculate:(qty:number)=> number 
}
```

Once you have defined an `interface`, you can use it as a type. In the following example, we annotate the product variable with the `IProduct interface`.

```javascript
let product: IProduct = {
    id : 1,
    name: "Samsung Galaxy",
    price:1000,
    calculate(qty:number): number {
        return this.price*qty;
    }
}
 
console.log(product.calculate(10))      //1000

```

🖐️ If the Product variable does not contain any property or method defined in the `Interface`, then the Typescript compiler immediately `throws an error`.

```javascript
let product: IProduct = {
    id : 1,
    name: "Samsung Galaxy",
    calculate(qty:number): number {
        return this.price*qty;
    }
}
 
//Property 'price' is missing in type '
//{ id: number; name: string; calculate(qty: number): number; }' 
//but required in type 'IProduct'.
 
```
💡 Hence the product object must adhere to an Interface. When it does that, we say that the object implements the interface.
### Optional Properties

In such cases, we can mark the property as optional with a question mark after the name.

> In this example, address is optional. The compiler does not throw any errors.
> 😊

```javascript
interface IEmployee {
    firstName: string;
    lastName: string;
    address?:string
}
 
let employee:IEmployee= {
   firstName: "Allie", 
   lastName: "Grater",
}
 
```
### Read-Only Properties

We can also mark the property as read-only by prefixing the property as readonly. When the property is marked as read-only, we can assign a value to the property only when initializing the object or in the class constructor. Any subsequent assignments will result in a compiler error.

```javascript
interface IEmployee {
    readonly firstName: string;
    readonly lastName: string;
    address:string
}
 
 
let employee:IEmployee= {
   firstName: "Allie", 
   lastName: "Grater",
   address:"Mumbai, India"
}
 
employee.firstName="Bill"       //Compiler Error ❌
employee.address="Mumbai, Maharastra India"     //ok ✅
 
```
### Interface for an array of objects

The following examples show how you can use represent an array of objects using the interface.

The simplest option is to create the interface for the object and use the [] to declare the variable.

```javascript
interface Employee {
  id: number;
  name: string;
}
 
const arrEmployee: Employee[] = [
  { id: 1, name: 'Rebecca' },
  { id: 2, name: 'Akins' },
];
 
```

You can also create another interface to extend the Array interface as shown below.

```javascript 
interface Employee {
  id: number;
  name: string;
}
 
interface EmployeeArray extends Array<Employee> {}
 
 
let arrEmployee: EmployeeArray = [
  { id: 1, name: 'Rebecca' },
  { id: 2, name: 'Akins' },
];
```
### Interfaces for functions

Interfaces are also capable of describing the functions.

```javascript
interface IAdd {
    (arg1:number,arg2:number):number
}
 
let add:IAdd
 
add=function(num1:number,num2:number,num3:number) {
  return num1+num2;
}
 
//Type '(num1: number, num2: number, num3: number) => number' is not assignable to type 'IAdd'.
 
//invoking
add(10,20) //30
```

Typescript compiler throws an error if we try to use more arguments or arguments of incompatible data types to the implementation function.

```javascript
interface IAdd {
    (arg1:number,arg2:number):number
}
 
let add:IAdd
 
add=function(num1:number,num2:number,num3:number) {
  return num1+num2;
}
 
//Type '(num1: number, num2: number, num3: number) => number' is not assignable to type 'IAdd'.
 
//invoking
add(10,20) //30
```

But allows less number of arguments. In this example, arg2 is missing in the implementation function and yet the compiler will not complain.

```javascript
interface IAdd {
    (arg1:number,arg2:number):number
}
 
let add:IAdd
 
add=function(num1:number) {     //No error
  return num1;
}
 
 
//invoking
add(10,20) //30
```

This example shows how you can create an interface for types that contain a function. The signature of the getName function inside the IEmployee type in declared inline.

```javascript
interface IEmployee {
    firstName: string;
    lastName:string
    getName(fName:string,lName:string):string
}
 
 
let emp:IEmployee= {
 
  firstName:"",
  lastName:"",
  getName:function(fName:string,lName:string) {
    return fName+lName
  }
}
```

You can also create a separate interface for the function and use it to annotate the getName function.

```javascript
interface IgetName {(fName:string,lName:string):string}     //function interface
 
interface IEmployee {
    firstName: string;
    lastName:string;
    getName:IgetName;
}
 
 
let emp:IEmployee= {
 
  firstName:"",
  lastName:"",
  getName:function(fName:string,lName:string) {
    return fName+lName
  }
}
```
### Function Overloading

> Function overloading in TypeScript lets you define functions that can be called in multiple ways.

> Using function overloading requires defining the overload signatures: a set of functions with parameter and return types, but without a body. These signatures indicate how the function should be invoked.

⚠️  Typescript does not allow us to same name for multiple functions. It throws a Duplicate function implementation error if we try to do so.

Since Typescript is based on JavaScript, it does not allow us to create Overloaded functions with the same name. Instead, it allows us to **create overload signatures for a regular function**.

To create function overloading first, we need to create a regular function. This function must check the type of the arguments passed to it and call the appropriate code within that function. We call this an **implementation function.**

Next, we create overload signatures for that function and use those signatures to call the function.

```javascript
class calculator {
 
    result:number;
 
    constructor() {
        this.result=0
    }
 
    //overload signature
    add(num1:number,num2:number):number
    add(numArray:number[]):number
 
 
    //function implementation
    add(arg1:number|number[], arg2?:number):number {
  
        this.result= 0;  //default is zero. 
 
 
        if (Array.isArray(arg1)) {
 
            var sum = arg1.reduce(function(a, b){
                return a + b;
            }, 0);
            this.result= sum;
        }
 
        if (typeof arg1=="number" && typeof arg2=="number") {
            //number
            this.result= arg1 + arg2;
        }
 
        return this.result;
 
    }
 
}
 
let Calc=new calculator();
Calc.add(10,10)         //20
Calc.add([1,2,3,4,5,6]) //21
 
```

**Order of overload signature in Important**

Order of overload signature is important. TypeScript chooses the first matching overload when resolving function calls. Hence we need to put the more specific signatures before the more general signatures

```javascript
function fn(x: unknown): unknown;
function fn(x: number[]): number;
function fn(x:any) {
    return x;
}
 
//call the function with a number array and expect a number back
var x = fn([1,2,3]); //  x is unknown
 
```

**The implementation function should be the last**

The overload signatures must be placed directly above the implementation function. The following code is invalid, because of the let statement placed between the overload signature and the implementation function. Typescript compiler throws the “Function implementation is missing or not immediately following the declaration” error

```javascriot
function odFunc(a:string):string
function odFunc(a:number,b:string):string
 
let a =10
 
function odFunc(a:any,b?:any):string {
    return ""
}
 
 
//Function implementation is missing or not immediately following the declaration.(2391)
 ```
### Class Implementing Interface

The Interfaces can be used with the Classes using the keyword implements.

The following example creates the Employee class which implements the IEmployee interface.

```javascript
interface IEmployee {
    firstName: string;
    lastName: string;
    address:string;
    getName():string
}
 
class Employee implements IEmployee {
 
    firstName: string;
    lastName: string;
    address:string;
 
    constructor(firstName: string, lastName: string, address:string) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.address=address;
    }
 
    getName():string {
        return this.firstName+' '+this.lastName
    }
 
}
```
### Extending Interfaces

We can extend the Interfaces to include other interfaces. This helps us to create a new interface consisting of definitions from the other interfaces

This example IEmployee interface also extends the IAddress interface. The employee object must contain all the properties from both the interface.

```javascript
interface IAddress {
    address: string;
    city:string
    state:string
}
 
interface IEmployee extends IAddress {
    firstName: string;
    lastName: string;
    fullName(): string;
}
 
 
//Compiler error
let employee: IEmployee = {
    firstName : "Emil",
    lastName: "Andersson",
    fullName(): string {
        return this.firstName + " " + this.lastName;
    },
    address:"India",
    city:"Mumbai",
    state:"Maharastra",
}
```

You can extend an interface from several other interfaces.

```javascript
interface IAddress {
    address: string;
    city:string
    state:string
}
 
interface IEmployment {
    designation: string;
}
 
interface IEmployee extends IAddress, IEmployment {
    firstName: string;
    lastName: string;
    fullName(): string;
}
 
 
//Compiler error
let employee: IEmployee = {
    firstName : "Emil",
    lastName: "Andersson",
    fullName(): string {
        return this.firstName + " " + this.lastName;
    },
    address:"India",
    city:"Mumbai",
    state:"Maharastra",
    designation:"CEO"
}
 
```
### Interface Merging

Declaration merging is one of the unique concepts of TypeScript. “declaration merging” means that the compiler merges two or more separate declarations declared with the same name into a single definition.

This example creates two interfaces with the name IEmployee.

```javascript
interface IEmployee {
    firstName: string;
    lastName: string;
    fullName(): string;
}
 
interface IEmployee {
    address: string;
    city:string
    state:string
}
```

The compiler does not complain, but instead, it merges both the interface into one.

```javascript
//merged to
interface IEmployee {
    firstName: string;
    lastName: string;
    fullName(): string;
    address: string;
    city:string
    state:string
}
```

That is why the following code results in a compiler error because the employee object does not implement the address, city and state property.

```javascript
interface IEmployee {
    firstName: string;
    lastName: string;
    fullName(): string;
}
 
interface IEmployee {
    address: string;
    city:string
    state:string
}
 
//Compiler error
let employee: IEmployee = {
    firstName : "Emil",
    lastName: "Andersson",
    fullName(): string {
        return this.firstName + " " + this.lastName;
    }
}
 
 
//Type '{ firstName: string; lastName: string; fullName(): string; }' 
//is missing the following properties 
//from type 'Employee': address, city, state

````
In the case of interface merging, the common properties with the same name and data type are merged. But in the case of functions, if the function signatures do not match, then overload functions are created. This is different from interface extending where it compiler throws an error.
### Generic interfaces

The generics in typescript allow us to work with a variety of types instead of a single one.

>Using generics, we can reduce the number of interfaces into a single one. Here T represents a type. It could be anything string, number or array, etc. Here a single interface handles multiple related functions.

```javascript
interface Iadd<T> {(arg1:T,arg2:T):T}
 
 
let addString1:Iadd<string> = function(arg1:string,arg2:string) {
  return arg1+arg2;
}
let addNum1:Iadd<number> = function(arg1:number,arg2:number) {
  return arg1+arg2;
}
let addArray:Iadd<String[]> = function(arg1:String[],arg2:String[]) {
  return [ ...arg1, ...arg2];
}
 
 
```
