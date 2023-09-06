## Type Aliases

The Type Aliases in Typescript allow us to give a custom name to an existing type. This is useful when you wish to reuse an existing type as it provides a reusable definition.

### Creating Type Alias

The syntax starts with the keyword type followed by the name you wish to give to the new type. It is then followed by an assignment operator and then the type to which you want to assign the name.

```javascript
type aliasName = anyType;
```
The following example creates Person type, which is an object with property name & age.

```typescript
type Person = {
  name: string;
  age:number;
}
```

Now, we can use the type Person to create an object as shown below

```typescript 
let person:Person;
```
hovering over the person will show its type as Person. Intellisense shows only two properties age & name.

![](https://raw.githubusercontent.com/sajidaqadomi/images/main/img12.webp)

```javascript
type Person = {
  name: string;
  age:number;
}
 
let person:Person = {
  name:"Sachin",
  age:50
}
 
```

### Type Alias for Functions
We can also create a Type Alias for a function expression. The following Type alias FuncPrintString accepts a string as an argument and returns a void.

 
```javascript
type FuncPrintString = (strToPrint:string) => void
 
// function expression
let printMe:FuncPrintString = function(foo) {
  console.log(foo)
}
 
printMe(1)  //Argument of type 'number' is not assignable to parameter of type 'string'.
printMe("Hello")  //ok
```

**But there is no option to apply a type alias to a function declaration.**🖐️⚠️

```javascript
type FuncPrintString = (strToPrint:string) => void
 
// function declaration. Cannot apply type alias here😢
function printMe(foo) {
  console.log(foo)
}
```

### Literal Types

TypeScript Literal Types restrict the value of a variable to finite valid values. This is in contrast to the variable which allows you to change value (except for TypeScript Constants). The latest version of Typescript supports the String Literal Types, Numeric Literal Types, Boolean Literal Types & Enum Literal Types

>TypeScript also allows us to define our own literal types. The latest version of Typescript supports the following Literal Types

- String Literal Types
- Numeric Literal Types
- Boolean Literal Types
- Enum Literal Types

The following example engineStatus can have only one value i.e. "Active"

```javascript 
let engineStatus:"Active";
```

Defining a variable type as a string literal does not initialize its value. The TypeScript initializes the variable as Undefined.

```javascript
let engineStatus:"Active";
console.log(typeof engineStatus)    //Undefined
console.log(engineStatus)           //Undefined
```

We can only assign the value "Active" to it.

```javascript
let engineStatus:"Active";
engineStatus="Active"                  
console.log(typeof engineStatus)    //String
console.log(engineStatus)           //Active
 
engineStatus="active"             //Type '"active"' is not assignable to type '"Active"'
```

### Enum Literal Types

Enums are used to define named constants in Typescript. It's the typescripts own feature which is not a type level extension of javascript. It is defined using enum keyword.

You can also define Enum as literal type.

 
```javascript
enum Dir1 {
  Up = 1,
  Down,
}
 
enum Dir2 {
  Left=3,
  Right,
}
 
let a:Dir1.Up|Dir2.Left
 
a=Dir1.Up       //ok
a=Dir1.Down     //Type 'Dir1.Down' is not assignable to type 'Dir1.Up | Dir2.Left'
```

Typescript has three types of enums:
1. Numeric Enums
```javascript
enum Numeric {
    First,
    Second,
    Third,
    Fourth
}
console.log(Numeric.Second); // 1
```
A numeric enum's first member is not initialized then it starts from 0 and Second becomes 1.

```javascript
enum Numeric {
    First = 1,
    Second,
    Third,
    Fourth
}
console.log(Numeric.Second); // 2
```

1. String Enums

    An enum which is initialized with string literal is called String enum.
    
    ```javascript
    enum StringEnum {
        A = "a",
        B = "b",
        C = "c",
        D = "d",
    }
    ```

1. Heterogeneous Enums

    Mix of numeric and string enums.

    ```javascript
    enum HeterogeneousEnum {
        No = 0,
        Yes = 'YES'
    }
    ```
    
🗒️💡**Notes**

- Enum without initializers need to be first.
    ```javascript
    function getConstantValue() {
        return 1;
    }
    
    enum Numeric {
        first,
        second = getConstantValue(),
    }
       // first & second shouldn't be upside down.

    ```
- Enums without initializers should come after initialized enums with numeric constants or other enum constants.like below:

    ```javascript
    enum Numeric {
        first = 2,
        second = A,
        third
    }
    ``` 

    But not like below.👎❌
    
    ```javascript
    enum Numeric {
         first = 2,
         second = getConstantValue(), 
         third
     }
    ```
- Computed values are not permitted in an enum with string valued members.
like below:

    ```javascript
    enum constNComputeEnum {
         first = 1,
         second = 'second',
         third = constNComputeEnum.first, // not allowed ❌
     }
    ```
