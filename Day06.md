## Classes

Classes in TypeScript is a template for creating objects. The class defines the data (fields or properties) and the operations (methods) that we can perform on that data. We can create many objects using a single class.

**Creating Classes in TypeScript**

```javascript
class Person {
}
```

**Adding Fields to Class**
> The fields (properties) hold the data of the class. Adding a field is similar to declaring the variables. But without the use of let, var & const keyword.

> In this example, we have added two fields firstName & lastName. Both the properties are of type string.

```javascript
class Person {
  firstName:string=""
  lastName:string=""
}  
```

**Creating objects from Class**

> The class acts as a template for creating objects. We can create multiple objects using the same class. To create a new object use the new keyword followed by the name of the class and then brackets ( ).

```javascript
class Person {
  firstName:string=""
  lastName:string=""
}
 
let p1 = new Person();
p1.firstName="Jon"
p1.lastName="Snow"
 
console.log(p1)   //Person: {  "firstName": "Jon",   "lastName": "Snow" } 
 
let p2 = new Person();
p2.firstName="Samwell"
p2.lastName="Tarly"
 
console.log(p2)   //Person: {  "firstName": "Samwell",   "lastName": "Tarly" }

```

**Providing initial value to Properties**

```javascript
class Person {
  firstName:string="Jon"
  lastName:string="Snow"
 }
 
let p1= new Person() 
let p2= new Person() 
 
console.log(p1)   //Person: {  "firstName": "Jon",   "lastName": "Snow" } 
console.log(p2)   //Person: {  "firstName": "Jon",   "lastName": "Snow" } 

```

The preferred way is to use the constructor function, which allows us to pass different values when we create an object from it.

**Constructor function**

>A constructor is a special function of the class that is automatically invoked when we create an instance of the class. We use it to create & initialize the instance of the class.
>
>The constructor method in a class must have the name constructor. A class can have only one implementation of the constructor method. 
```javascript
class Person {
  firstName:string;
  lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
} 

let p1= new Person("Jon","Snow")
let p2= new Person("Samwell","Tarly")
 
console.log(p1)   //Person: {  "firstName": "Jon",   "lastName": "Snow" } 
console.log(p2)   //Person: {  "firstName": "Samwell",   "lastName": "Tarly" } 
```

>The constructor method creates the instance of the object with the properties defined in the class. We can access that instance by using the this inside the constructor. We use that to initialize the properties of the current object. Once finished constructor function returns the new object.
>

**Methods**

> A function declared in a class is called a method. The methods represent the behavior of the class.

```javascript
class Person {
  firstName:string;
  lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
  // Example of method
  getName() : string {
    return this.firstName + " "+ this.lastName
  }
} 
 
let p= new Person("Jon","Snow")
 
console.log(p.getName())      //Jon Snow

```

**Class declarations are not hoisted**

```javascript
let p= new Person("Jon","Snow")   // ❌Class 'Person' used before its declaration.
 
 
class Person {
  firstName:string;
  lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
} 
```

## Public, Private & Protected Access Modifiers

Private, Public & Protected are the Access Modifiers that we can use in Typescript to control whether certain methods or properties are visible to code outside the class.

**Public**

> Public access modifier allows the class properties and method freely accessible anywhere in the code. The public is the default access modifier if we do not specify the access modifier


```javascript
class Person {
  public firstName:string;
  public lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
  getName() : string {
    return this.firstName + " "+ this.lastName
  }
} 

> The above code works even if we remove the keyword public. Because it is the default access modifier.
 
let p= new Person("Jon","Snow")
 
 
console.log(p.firstName)   //Jon
console.log(p.lastName)    //Snow
console.log(p.getName())      //Jon Snow

```
**Private**

> The Private access modifier restricts access to the class member from within the class only. We cannot access the property or the method from outside the class

```javascript
class Person {
  private firstName:string;
  private lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
  getName() : string {
    return this.firstName + " "+ this.lastName
  }
} 
 
let p= new Person("Jon","Snow")
 
//Compiler Error
console.log(p.firstName)   //Property 'firstName' is private and only accessible within class 'Person'.
console.log(p.lastName)    //Property 'lastName' is private and only accessible within class 'Person'
 
//ok
console.log(p.getName())   //Jon Snow
```
> We **cannot** even access the private property in a derived class.

```javascript
class Person {
  private firstName:string;
  private lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
  getName() : string {
    return this.firstName + " "+ this.lastName
  }
} 
 
 
class Employee extends Person {
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
    super(firstName,lastName)
    this.designation=designation;
  }
 
  changeName(firstName:string, lastName:string): void {
 
    //ERROR 
    
    this.firstName=firstName;  //Property 'firstName' is private and only accessible within class 'Person'.
    this.lastName=lastName;   //Property 'lastName' is private and only accessible within class 'Person'.
  }
 
}
 
 
let p= new Employee("Jon","Snow","Manager")
 
//Compiler Error
console.log(p.firstName)   //Property 'firstName' is private and only accessible within class 'Person'.
console.log(p.lastName)    //Property 'lastName' is private and only accessible within class 'Person'
 
//ok
console.log(p.getName())   //Jon Snow
```

**Protected**

> The Protected modifier allows access to the class member from itself and from any classes that inherit (sub-class) from it.

```javascript
class Person {
  protected firstName:string;
  protected lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
  getName() : string {
    return this.firstName + " "+ this.lastName
  }
} 
 
 
class Employee extends Person {
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
    super(firstName,lastName)
    this.designation=designation;
  }
 
  changeName(firstName:string, lastName:string): void {
 
    //Ok
    this.firstName=firstName;
    this.lastName=lastName;  
  }
 
}
 
 
let p= new Employee("Jon","Snow","Manager")
 
//Compiler Error
console.log(p.firstName)   //Property 'firstName' is private and only accessible within class 'Person'.
console.log(p.lastName)    //Property 'lastName' is private and only accessible within class 'Person'
 
//ok
console.log(p.getName())   //Jon Snow
 
 
let p1= new Person("Jon","Snow")
//Compiler Error
console.log(p.firstName)   //Property 'firstName' is private and only accessible within class 'Person'.
console.log(p.lastName)    //Property 'lastName' is private and only accessible within class 'Person'


```

**Overriding Access Modifier in the Derived Class**

> The derived class can redeclare the property and override the Access modifier. In the example, the derived class Employee re-declares the protected property firstName & lastName. This effectively removes the protected protection from the objects created using the Employee class. But the objects created using the Person class will not be able to access the firstName & lastName

```javascript
class Person {
  protected firstName:string;
  protected lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
  getName() : string {
    return this.firstName + " "+ this.lastName
  }
} 
 
 
class Employee extends Person {
  firstName:string;
  lastName:string;
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
    super(firstName,lastName)
    this.firstName=firstName;
    this.lastName=lastName;    
    this.designation=designation;
  }
 
  changeName(firstName:string, lastName:string): void {
   this.firstName=firstName; 
    this.lastName=lastName;   
  }
 
}
 
//Created from the Employee Class
let e= new Employee("Jon","Snow","Manager")
 
//Ok
console.log(e.firstName)
console.log(e.lastName) 
 
 
//Created from the Person class
let p= new Person("Jon","Snow")
 
//Error
console.log(p.firstName)  //Property 'firstName' is protected and only accessible within class 'Person' and its subclasses.
console.log(p.lastName)   //Property 'lastName' is protected and only accessible within class 'Person' and its subclasses.
 
 


```

## Constructor Method

> A constructor is a special function of the class that is automatically invoked when we create an instance of the class in Typescript. We use it to initialize the properties of the current instance of the class. Using the constructor parameter properties or Parameter shorthand syntax, we can add new properties to the class. We can also create multiple constructors using the technique of constructor method overload.

**Creating a Class Constructor**
✅   the class can have only one implementation of the constructor method.

✅The constructor method is invoked every time we create an instance from the class using the new operator

```javascript
class Person {
 
  constructor() {
    console.log("Constructor is called")
  }
} 
 
let p1= new Person()    //contructor is called
 
let p2= new Person()    //contructor is called
```

The constructor method creates the instance of the object with the property defined in the class. We can access the current instance using the ‘this‘ inside the constructor. Once finished constructor function returns the new object.


**Parameters to the Constructor method**

The constructor function in the following example accepts two arguments. We use the ‘this‘ keyword to get the current instance of the class and initialize its properties using those parameters.

```javascript
class Person {
  firstName:string;
  lastName:string;
 
  constructor(fName:string, lName:string) {
    this.firstName=fName;
    this.lastName=lName;
  }
} 
 
 let p= new Person("Jon","Snow")  
console.log(p)  //Person: {   "firstName": "Jon",   "lastName": "Snow" } 

/* 
The parameter in the constructor is not optional here. This means that when you instantiate the class, you must pass the values of all arguments to the constructor. If you do not pass all parameters, then it will result in a compiler error.
*/

let p= new Person("Jon")   //Expected 2 arguments, but got 1.
```

**Constructor Parameter Properties**

>Constructor Parameter Properties (or Property Shorthand syntax) offers a special **shorthand syntax** to convert parameters of constructor function into properties. We can do this by prefixing a constructor parameter with one of the visibility modifiers ( i.e. public, private, protected, or readonly). The resulting field gets those modifier(s)

```javascript
class Person {
  firstName:string;
  lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
} 
```

Instead, we can prefix the constructor parameters with the public modifier. Typescript automatically creates the properties for us😊 👎

```javascript
class Person {
  constructor(public firstName:string, public lastName:string) {
  }
} 
 
let p = new Person("Jon", "Snow");
 
console.log(p)   //Person: { "firstName": "Jon",   "lastName": "Snow" } 

```

**Passing Default Values in the Constructor method**

```javascript
class Point {
  x: number;
  y: number;
 
  constructor(x = 10, y = 20) {
    this.x = x;
    this.y = y;
  }
}
 
//Using default Values
let p1 = new Point();
console.log(p1)  //Point: {   "x": 10,   "y": 20 } 
 
 
let p2 = new Point(100,200);
console.log(p2)  //Point: {   "x": 100,   "y": 200 } 
 
```

**Constructor functions in the derived class**

> The derived class must call the constructor of the parent class (base class). We do this by invoking the `super` method. We must call the super method before we use ‘this‘ variable.

```javascript
class Person {
  firstName:string;
  lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
} 
 
 
class Employee extends Person {
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
 
    super(firstName,lastName)   // call parent class constructor
 
    this.designation=designation;
  }
 
}
 
let e = new Employee("Jon","Snow","Manager")
console.log(e)  //Employee: {   "firstName": "Jon",  "lastName": "Snow",   "designation": "Manager" }

```

**super’ must be called before accessing ‘this’ in the constructor of a derived class**

⚠️⚠️
```javascript

class Employee extends Person {
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
 
     //Both compiler and run time error
    console.log(this)   //❌'super' must be called before accessing 'this' in the constructor of a derived class.
 
    super(firstName,lastName) // call parent class constructor
    
    this.designation=designation;
  }
 
}
```
**Constructors for derived classes must contain a `super` call**

```javascript
class Employee extends Person {
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
 
    this.designation=designation;
  }
 
}
 
 
//Constructors for derived classes must contain a 'super' call.
```

**Class without constructor**

> You can create a class without a constructor method. In such cases, JavaScript (not TypeScript) automatically uses a default constructor.

The default constructor is an empty constructor.

```javascript
constructor() {
}
```

But if the class is a derived class then the default constructor is as shown below

```javascript
constructor(...args) {
  super(...args);
}
```

**Multiple Constructor methods**

> A class can have only one implementation of the constructor method. Having more than one constructor function will result in an error.
>
> But we can take advantage of function overload to create multiple overload signatures of the constructor function.

```typescript
class Person {
 
  name:string;
 
  constructor(name:string);                                       //constructor function signature 1
  constructor(firstName:string,lastName:string);      //constructor function signature  2
 
  constructor(name:string, lastName?:string) {        //actual constructor function
    if (lastName) {
      this.name=name+" "+lastName
    }
    else {
      this.name=name;
    }
  }
} 
 
let p = new Person("Jon", "Snow");
console.log(p)   //Person: { "name": "Jon Snow" } 
 
p = new Person("Samwell Tarly");
console.log(p)   //Person: {  "name": "Samwell Tarly" } 
```
🗒️🖐️  Note that a parameter property is only allowed in a constructor implementation. For example, prefixing the public modifier to the name property in the constructor function signature results in a compiler error.

```javascript


class Person {
 
  constructor(public name:string);                                //Error ❌
  constructor(firstName:string,lastName:string);   
 
  constructor(name:string, lastName?:string) {        
    if (lastName) {
      this.name=name+" "+lastName
    }
    else {
      this.name=name;
    }
  }
} 
 
//<strong>parameter property</strong> is only allowed in a constructor implementation
 
```

You can prefix the public modifier to the name property only in the constructor implementation function.

```javascript
class Person {
 
  constructor(name:string);                              
  constructor(firstName:string,lastName:string);   
 
  constructor(public name:string, lastName?:string) {       //ok
    if (lastName) {
      this.name=name+" "+lastName
    }
    else {
      this.name=name;
    }
  }
}
```

## Inheritance
> Inheritance refers to the ability of an object to reuse the properties and methods of other objects.


**Creating Inheritance in TypeScript**

> to create inheritance we use the extends keyword

```javascript
class Person {
  firstName:string="";
  lastName:string="";
 
  getName() :string {
    return this.firstName+ " "+this.lastName
  }
} 
 
 
class Employee extends Person{
  designation:string="";
}
 
//extend class gets all the properties and methods of the Parent Class
let e= new Employee();
e.firstName="Jon"
e.lastName="Snow"
e.designation="Lead Cast"
console.log(e.getName())  //"Jon Snow"
console.log(e)  // Employee: {  "firstName": "Jon",  "lastName": "Snow",  "designation": "Lead Cast"}  
```
**Invoking Parent class constructor**

In the above example, we used the simple class without a constructor

If the parent class has a constructor, then the child class must invoke the parent class constructor in its constructor. We do that by using a special method super.

In the example below, the Person class has a constructor method that accepts two arguments. firstName & lastName.

```javascript
class Person {
  firstName:string;
  lastName:string;
 
  constructor(firstName:string, lastName:string) {
    this.firstName=firstName;
    this.lastName=lastName;
  }
 
} 

class Employee extends Person {
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
 
    super(firstName,lastName)   // call parent class constructor
 
    this.designation=designation;
  }
 
}
 
```

🖐️ The call to `super` **must** be made before the use of ‘this’ keyword.

🖐️ If we do not call the super method, then the compiler flag this as an **(“Constructors for derived classes must contain a ‘super’ call“)** `error`.

```javascript
class Employee extends Person {
  designation:string;
 
  constructor(firstName:string, lastName:string, designation:string) {
  }
 
}
 
// Constructors for derived classes must contain a 'super' call.
```

If the child class does not need a constructor, then you can omit to call super method. The compiler will not flag this as an error.

```javascript
class Employee extends Person {
  designation:string="";
}
```
But the Typescript automatically creates a constructor method with a super call in the generated JavaScript. The above results in the following JavaScript code.

```javascript
class Employee extends Person {
    constructor() {
        super(...arguments);
        this.designation = "";
    }
}
``` 

🤔🤔**Remember that**🤔🤔

- The call to super must be made before the use of ‘this’ keyword.

- If the derived class has a constructor method, then calling super is compulsory.

- In case the parent class does not have a constructor method, then invoke super without any parameter

- If both parent and child do not need a constructor method, then you do not have to create one. JavaScript will automatically create an empty constructor for both.
 

**Method Overriding**

> You can override the Methods & Properties of the Parent class in the child class.
>
> In method overriding the types of the parameters and the return type of the method have to be compatible with that of the parent class.
>
> While in Property overriding the data type of the Property have to be compatible with that of the parent class

```javascript
class Person {
  greet(name:string) :void {
    console.log("Hello from Parent "+ name)
  }
} 
 
class Employee extends Person{
  greet(name:string) :void {
    super.greet(name)     //invoke parent class method
    console.log("Hello from Child "+ name)
  }
}
 
let e = new Employee()
e.greet("Jon Snow")  //Hello from Parent Jon Snow 
                                 //Hello from Child Jon Snow
 
```

in the upper  example, The Employee class overrides the greet method of the parent class.

we use the super to invoke the parent class method. In this example super.greet() method invokes the greet method from the parent class.

[Reference](https://www.tektutorialshub.com/typescript/inheritance-in-typescript/)

**Inheritance & Visibility**

> Typescript does **not allow** us to change the visibility of the properties in the overridden class `except for changing protected to public`.
>
❌Th e following code throws an error because we are changing visibility from public to private

```javascript
class Person {
  public age:number=0
} 
 
 
class Employee extends Person{
  private age:number=0
}
 
 
//Class 'Employee' incorrectly extends base class 'Person'.
//Property 'age' is private in type 'Employee' but not in type 'Person'.

```

✅But changing from protected to public is allowed. You can read more about the Exposure of protected members

```javascript
class Person {
  protected age:number=0
} 
 
 
class Employee extends Person{
  public age:number=0
}
```

**Overriding Readonly & Optional Properties**

> The derived classes can override the `Readonly and Optional` properties of `Public and Protected` Properties. It can either make the property `Readonly` and/or `Optional` or `Remove it`

```javascript
class Product  {
    name:string
    readonly price:number
 
    constructor(name:string, price:number) {
      this.name=name
      this.price=price
    }
}
 
 
class ITProduct extends Product {
    price:number
 
    constructor(name:string, price:number) {
      super(name,price)
      this.price=price
    }
}
 
let p = new ITProduct("Computer",1000)
p.price=2000  //   ok
```

Similarly, the derived class removes the optional from the price property.

```javascript
class Product  {
    name:string
    price?:number
 
    constructor(name:string) {
      this.name=name
    }
}
 
class ITProduct extends Product {
    price:number
 
    constructor(name:string) {
      super(name)
    }
}
 
//Property 'price' has no initializer and is not definitely assigned in the constructor.

```

## Getters & Setters

> The Getters and Setters are known as accessor properties in TypeScript. They look like normal properties but are actually functions mapped to a Property. We use “get” to define a getter method and “set” to define a setter method. The Setter method runs when we assign a value to the Property. The Getter method runs when we access the Property.

```javsscript
var car = { 
 
  //Regular Property 
  //Also known as backing Property to color getter & setter property
  _color: "blue", 
  
  // Accessor Property with the name color
  get color() {                    //getter
      return this._color; 
  }, 
  set color(value) {               //setter
      this._color=value; 
  }    
};
 
//Using the getter method
console.log(car.color);  //blue  
 
 
//Setting color. Runs the setter method
car.color="red";
console.log(car.color);  //red  Accessing the property
 
//You can also access the backing property
console.log(car._color);  //red
```

**Creating Getters TypeScript**

```javascript
let obj = {
  _propName:"",
 
  get propName() {           // getter method
    
    // this code is executed when we access the property using 
    // Example value = obj.propName
    return this._propName
  },
}
 
```

The getter function executes when we read the value of the Property. Note that we **cannot pass an argument to the getter** method. The return value of the getter method becomes the value of the property access expression.

In the following example, color is a getter property, while _color is a regular Property. The color function returns the value of the _color property.

```javascript
var car = { 
 
  _color: "blue", 
 
  // Accessor Property with the name color
  get color() {                    //getter
      return this._color; 
  }, 
 
};
 
console.log(car.color)
 
```

**Creating Setters**

> A ‘set’ accessor must have exactly one parameter

The **setter**  method executes when we assign a value to the property. JavaScript invokes the setter method with the value of the right-hand side of the assignment as the argument. If the setter method returns a value then it is ignored.

In the following example, color is a setter property, while _color is a regular Property. The color function accepts a value and updates the _color property.

```javascript
var car = { 
  _color: "blue", 
  
  set color(value:string) {               //setter method
      this._color=value; 
  }    
};
 
car.color="red";
```

**Getter & Setters in TypeScript Classes**

> In the Typescript Classes, we can use the private access Modifier and mark the backing property as private.

In this example, we use the TypeScript class to create a Car class, with getter and setter methods for the color property. We marked the backing property _color as private

```javascript
class Car { 
 
  //Regular Property 
  //Also known as backing Property to color getter & setter property
  private _color:string="blue"
  
  // Accessor Property with the name color
  get color() {                    //getter
      return this._color; 
  }
 
  set color(value) {               //setter
      this._color=value; 
  }    
};
 
let car = new Car()
 
//Using the getter method
console.log(car.color);  //blue  
 
//Setting color. Runs the setter method
car.color="red";
console.log(car.color);  //red  Accessing the property
 
//Compiler error here
console.log(car._color);  //Property '_color' is private and only accessible within class 'Car'
 
```

**Read-only /Write-only Properties**

> If the property has only a getter method, then it is a read-only property. If it has only a setter method then it is a write-only property

****

In the following example making the color property read-only. 

```javascript
class Car { 
 
  private _color="blue"
  
  get color() {                    
      return this._color; 
  } 
 
};
 
 
let car = new Car();
 
console.log(car.color);  //blue  
 
//Setting color. But it wont work as it is read only. 
car.color="red";
console.log(car.color);   //blue
 
//TypeScript Compiler error
//Cannot assign to 'color' because it is a read-only property.
 
//Runtime error while running the code
//Cannot set property color of #<Object> which has only a getter
```

Similarly, you can create a write-only property

```javascript
class Car { 
 
  private _color= "blue"
  
  set color(value:string) {                    
      this._color=value 
  } 
 
};
 
let car = new Car();
 
//Color is write only. Hnece always returns undefined
console.log(car.color);  //undefined
 
car.color="red";
console.log(car.color);   //undefined
 
//Property '_color' is private and only accessible within class 'Car'. 
console.log(car._color);  //red
```
