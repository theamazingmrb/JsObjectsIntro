# JavaScript Objects



### Objectives

After this lesson, students will be able to:

\- Explain the difference between object properties and methods

\- Create empty objects and objects with multiple properties and methods

\- Add, remove, and compare properties on an existing object using the dot and bracket notations

\- Check properties on an object using keys and helper methods (.hasOwnProperty)

\- Iterate over the keys of an object.



Objects in JavaScript

=====

## Opening



### What is an object?

![Whats that](https://media.giphy.com/media/ybcMkow8xLIrK/giphy.gif)

```javascript
const Person = {
  firstName: "Billie",
  lastName: "Heidelberg",
  age: 30,
  eyeColor: "Brown",
  sayHi: function() {
      return this.firstName + " " + this.lastName
  }
};
```



\*An object is a collection of values, and those values can be many different types.

\* Objects comparable to arrays, as in they store multiple values;  but unlike arrays, objects use named keys rather than indices to order and access those pieces of data

\* Objects in general are made up of two things – properties and methods. Properties are data attached to an object that describe it or are related to it in some way. Methods are just functions, but because they're attached to an object, you can think of them as actions that the object can invoke on itself

\* In JavaScript, an object is a type of key-value store, or a way to group many pairs of keys and values together, so sometimes it's used like a hash (in Ruby) or a dictionary (in other languages)

Aside from the values `null` and `undefined`, *\*everything in JavaScript is an object\.



### Collections of name-value pairs



JavaScript objects work as lists of keys (*\*A property name\) and corresponding values (*\*A property value\).



This way of storing/reading data is widely used across programs and languages because it’s highly customizable and quick to implement.



A key can be either a name, a number or a string, the corresponding value to a key can be any value part of JavaScript, including arrays, `null` or `undefined`and even another object. Objects structures can therefore be nested (objects inside objects) and of any complexity.



## Creating Objects



There are 4 different ways to create an object.



#### Object literal syntax



This is also called an [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer).



```javascript
const myObject = {}
```



#### Object constructor



The [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) constructor creates an object wrapper for the given value.

```
const myObject = new Object();
```



#### Constructor function



It is also possible to use a `function` statement to create an object that serves as a "constructor function."



The first step is to write a function that will define the object. By convention, this function we start the function name with a capital letter. Once the function is defined (in the current scope), you can create a new object by using the keyword `new`.



```javascript
function Person( firstName, lastName, age) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
}

const Billie = new Person("Billie", "Heidelberg", 30, "Brown");

Billie
=> Person {firstName: "Billie", lastName: "Heidelberg", age: 30}

```



#### Object.create



It is possible to use the syntax [`Object.create()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create).



This method can take an object in argument as the prototype, allowing you to create an object without having to use a constructor function.



```javascript
const Car = {
	type: "Honda",
    model: "Civic",
    displayType: function() {
        console.log("Im driving a " + this.type + " " + this.model)
    }
}

const myCar = Object.create(Car);

myCar.displayType();

=> "Im driving a Honda Civic"




```



## Object Properties



Objects in JavaScript *\*always\ have properties associated with them.



Properties help us define our Objects, you can think of them as variables that contain values. Those value types can be anything in JavaScript. The properties of an object can be accessed using "dot notation":



```javascript
const Person = {  
    firstName: "Billie",  
    lastName: "Heidelberg",  
};

Person.firstName
=> "Billie"

Person.firstName = "Jack"
Person.firstName
=> "Jack"
```



## Creating an object with properties

Lets create an object `cup` that contains properties type and isFull.



```javascript
const cup = new Object();

cup.type = "Coffee"
=> "Coffee"

cup.isFull = false;
=> false

cup
=> Object{type: "Coffee", isFull: false}
```

 



#### Bracket notation



There is another way to set and access properties on a JavaScript object.



```javascript
cup["type"] = "Glass"
=> "Glass"

cup["isFull"] = true
=> true

console.log(cup["type"])
=> "Glass"

console.log(cup["isFull"])
=> true

```



For more details see [MDN's Documentation on Property Accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors).





#### Deleting properties



If you want to delete a property of an object (and by extension, the value attached to the property), you need to use the [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete) operator:



```javascript
delete cup.full
=> true

cup
=> {type: "Glass"}
```



## Object methods



As we've said before, the value of a property can be anything in JavaScript, means we can also attach functions to objects properties. When a function is attached to a property, this function becomes a `method`. Methods are defined the exact same way as a function, except that they have to be defined as the property of an object.



```javascript
const car = {
	type: "Honda",
    model: "Civic",
    displayType: function() {
        console.log("Im driving a " + this.type + " " + this.model)
    }
}


```



We call this method by accessing the property name and adding a pair of parentheses to execute:



```javascript
car.displayType();
=> "I am driving a Honda Civic"
```



#### Assigning a previously-defined function



We can attach regular functions to objects as methods, even after they are created.

```javascript
const drive = function() {
	console.log("VROOOOOOOOM!")
}

car.drive = drive;

car.drive()
=> "VROOOOOOOOM!"

```



\## `this` for object references



In JavaScript, `this` is a keyword that refers to the current object. When used in a method on an object, it will always refer to the current object.



```javascript
const myCar = Object.create(car);
=> undefined

myCar.type = "Nissan";
=> "Nissan"

myCar.model = "Skyline";
=> "Skyline"

myCar.displayType();
=> "Im driving a Nissan Skyline"
```



#### Assigning a previously-defined function



\> A getter is a method that gets the value of a specific property. A setter is a method that sets the value of a specific property. You can define getters and setters on any predefined core object or user-defined object that supports the addition of new properties. The syntax for defining getters and setters uses the object literal syntax.



```javascript
var o = {
  a: 7,
  get b() {
    return this.a + 1;
  },
  set c(x) {
      this.a = x / 2
  }
};

console.log(o.a);
=> 7

console.log(o.b);
=> 8

o.c = 50;
console.log(o.a);
=> 25
```



This section from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Creating_new_objects#Defining_getters_and_setters)





#### Enumerating properties of an object



There are three native ways to list the properties of an object:



\* *\*for...in loops\ This method traverses all enumerable properties of an object and its prototype chain

\* *\*Object.keys(o)\ This method returns an array with all the own (not in the prototype chain) enumerable properties' names ("keys") of an object o.

\* *\*Object.getOwnPropertyNames(o)\ This method returns an array containing all own properties' names (enumerable or not) of an object o.





*\*Loop over an objects properties\





You can use the bracket notation with for...in to iterate over all the enumerable properties of an object.



```javascript
var myCar = {make: "Ford", model: "Mustang", year: 1969};

function showProps(obj, objName) {
 var result = "";
 for (var i in obj) {
  if (obj.hasOwnProperty(i)) {
   result += objName + "." + i + " = " + obj[i] + "\n";
  }
 }
 return result;
}

showProps(myCar, "Car");

=> Car.make = Ford

=> Car.model = Mustang

=> Car.year = 1969
```





## Comparing Objects

In JavaScript, if two objects are created separately, they are distinct, even if they are given the same properties.



```javascript
const student = {name: "Jim"};
=> undefined

const student2 = {name: "Jack};
=> undefined

student == student2
=> false

student === student
=> true
```



If you're confused by the difference between `==` and `===` review MDN's notes on [equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Equality_()) and [strict equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Identity_strict_equality_())



## Conclusion



We will use objects in JavaScript every day, and you will have plenty of time to practice creating and using objects in JavaScript. There are a lot of resources available on the web for you to dive deeper, but the most detailed and understandable one is probably MDN



\- [JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)

\- [Intro to Object-Orientated Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)

\- [Objects in Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
