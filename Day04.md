### Union Types

Union Types in Typescript allows a variable to have the ability to store a value of several types. We define union types by using a pipe (|) to separate each of the possible types.


For Example in the following code, the variable a can accept both string & number but not a boolean.

```javascript
let a:number|string
 
a = 1         //ok
a = "hello"   //ok
 
a=true        //Type 'boolean' is not assignable to type 'string | number'
```

The Type Aliases help us to create an alias for a union type and use that alias.

```javascript
type stringOrNumber =  number | string;
type yesNoType = "yes" | "no";
type statusType = "Pending" | "Started" | "Finished"
```

### Intersection types

Intersection types allow us to combine two or more types into one. The resulting type will have all the properties of all the types. This allows us to get a Single type from existing types that has all the properties of both the types

`let a : type1 & type2 & .. & .. & typeN`

```typescript
 
interface Person {
    name: string;
    age: number;
}
 
interface Student {
    studentCode: string;
    division: string
}
 
 
let student: Student & Person= {
    studentCode:"1",
    division:"10",
    name:"Rahul",
    age:20
}
 
```

```javascript
interface Colorful {
  color: string;
}
interface Circle {
  radius: number;
}
 
type ColorfulCircle = Colorful & Circle;
```

🗒**️Note**  that student has all the properties from the both the types. If you leave out of any one of the property as in name in the following code, the compiler will throw an error.

**Interfaces vs. Intersections**
We just looked at two ways to combine types which are similar, but are actually subtly different. With interfaces, we could use **an extends** clause to extend from other types, and we were able to do something similar with intersections and name the result with a type alias. The principal difference between the two is how conflicts are handled, and that difference is typically one of the main reasons why you’d pick one over the other between an interface and a type alias of an intersection type.

## Type assertions

In Typescript, Type assertion is a technique that informs the compiler about the type of a variable. Type assertion is similar to `typecasting` but it doesn’t reconstruct code. You can use type assertion to specify a value’s type and tell the compiler not to deduce it. When we want to change a variable from one type to another such as any to number etc, we use Type assertion

We can either use `< >` angular brackets or `as` keywords to do type assertion. 

```typescript
let str: unknown = "geeksforgeeks";
console.log(str);
  
let len: number = (str as string).length;
console.log(len);
```

```typescript
let num: any = 77;
  
// Conversion from any to number
let num1 = <Number> num;
  
console.log(num1);
console.log(typeof num1);
```

```typescript
interface details {
    first_name: string;
    last_name: string;
}

  
let person_1 = <details>{};
person_1.first_name = "Sarah";
person_1.last_name = "jane";
  
console.log(person_1);
```

[Reference](https://www.typescriptlang.org/docs/handbook/basic-types.html#type-assertions)

## Object Type

✅We can assign the object type to a variable by annotating it with :type after the variable name as shown below

```javascript 
let item : {id:number, name:string}         //Annotating with the type
 
 
item = {  id:1, name: "Samsung Galaxy" }    //Assigning a value
console.log(item.name)      //ok
```

✅You can also assign the object directly, in this case, Typescript infers and automatically assigns the correct type to the variable

```javascript
let item = {  id:1, name: "Samsung Galaxy" } 
 
console.log(item.name)      //ok
 
 
console.log(item.price)   //compiler error   
//Property 'price' does not exist on type '{ id: number; name: string; }'.
 
item = {  id:1, name: "Samsung Galaxy", price:100 }  //compiler error   
//Type '{ id: number; name: string; price: number; }' is not assignable to type '{ id: number; name: string; }'.


```

✅Type Alias

```javascript
type product={   
   id:number;      
   name:string ;
   price:number
}
 
let item :product
 
item = { id:1, name: "Samsung Galaxy", price:100 }  
 
console.log(calculate(10, item));       //1000
 
function calculate(qty:number, item: product):number {
  return qty * item.price;
}
```

✅Interface

```javascript
interface  product {   
   id:number;      
   name:string ;
   price:number
}
 
 
let item :product
 
item = { id:1, name: "Samsung Galaxy", price:100 }  
 
console.log(calculate(10, item));       //1000
 
function calculate(qty:number, item: product):number {
  return qty * item.price;
}
```

✅Class

```javascript
class  Product {   
   id:number;      
   name:string ;
   price:number;
 
    constructor(id:number, name:string,price:number) {
        this.id=id;
        this.name=name;
        this.price=price;
    }
}
 
let item :Product
 
item = new Product(1,"Samsung Galaxy", 100);    //create a new product
 
console.log(calculate(10, item));       //1000
 
function calculate(qty:number, item: Product):number {
  return qty * item.price;
}
 
```
------------------------------
