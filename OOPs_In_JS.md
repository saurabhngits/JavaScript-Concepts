> <br /> **Table of Contents** : 
>
> *[1. Object, property and method](#obj_prop_mtd)* <br />
> *[2. Class](#class)* <br />
> *[3. Encapsulation](#encapsulation)* <br />
> *[4. Abstraction](#abstraction)* <br />
> *[5. Inheritance](#inheritance)* <br />
> *[6. Polymorphism](#polymorphism)* <br />
> <br />

<br />
<br />

# 1. Object, property and method <a id="obj_prop_mtd"></a>

## **Object literal**

We can create a new object in JavaScript by setting its properties inside curly braces `{}`. Object literals property values can be any data types, like `function` literals, `arrays`, `strings`, `numbers` or `boolean`.

Let’s create an object with a named book, with properties such as *author*, *published year*, *title*, and a *method*

```javascript
const book = {
    title: "Hippie",    
    author: "Paulo Coelho",  
    year: "2018"
}
```

After creating an object you can get the value with dot notation. For example, we can get the value of the `title` with `book.title`. We can also access the properties with square brackets: `book["title"]`.

<br />
<br />

## **Object constructor**

Object constructor is use to create multiple objects with the same properties and methods. Object constructor is the same as a regular function. We can create a object from object constructor using `new` keyword.


```javascript
function Book(title, author, year) { 
   this.title = title; 
   this.author = author; 
   this.year = year;
}
const book1 = new Book ('Hippie', 'Paulo Coelho', '2018');

console.log(book1);

/*
    {
        title: "Hippie", 
        author: "Paulo Coelho", 
        year: "2018"
    }
*/

// if we want to create more than one book just we call function book with new keyword.
const book2 = new Book ('The Alchemist', 'Paulo Coelho', '1988');
```

`book1` and `book2` create an instance of `Book` and assigned it to a variable. To find out whether an object is an instance of another one. We can use `instanceof`.

```javascript
book1 instanceof Book
> true
```

<br />
<br />

## **Object.create()**

`Object.create()` methord is used to create a new object with the specified prototype object and properties. `Object.create()` method returns a new object with the specified prototype object and properties.

**Applications :** `Object.create()` is used for implementing inheritance in javascript.

<br />

**Syntax :**
```javascript
Object.create(prototype[, propertiesObject])
```
<br />

**Parameter Used :**

1. **prototype** : It is the prototype object from which a new object has to be created.
2. **propertiesObject** : It is optional parameter. It specifies the enumerable properties to be added to the newly created object.

<br />

**Return Valued :** `Object.create()` returns a new object with the specified prototype object and properties.

<br />

**Create an object with Object.create with no prototype**

Consider the below example to create a new object in JavaScript

```javascript
var person = Object.create(null);

typeof(person) // Object
console.log(person) // Object with prototype object as null

// Set property to person object
person.name = "Virat";

console.log(person) // Object with name as property and prototype as null
```

Here, we have created a new object `person` using `Object.create` method. As we have passed `null` for the `prototypeObject` . `person` object does not have any prototype object.

Further, we have added `name` as a new property to the `person` object.

Create an object with prototype:

```javascript
prototypeObject = {
	fullName: function(){
		return this.firstName + " " + this.lastName		
	}
}
var person = Object.create(prototypeObject)

console.log(person) // Object with prototype object as prototypeObject and no properties

// Adding properties to the person object
person.firstName = "Virat";
person.lastName = "Kohli";

person.fullName() // Virat Kohli
```

In the above example, we have created a `propertiesObject` with `fullName` function. We created a `person` object with `propertiesObject` as a prototype object of the person’s object using `Object.create`. Further, we added `firstName` and `lastName` properties to the `person` object. Here, we have added `firstName` and `lastName` properties after the object creation. It would have been great if we could add these properties while creating the object. To do that, we will use the 2nd argument of `Object.create` method.


<br />

<br />


# 2. Class <a id="class"></a>

Class is not an object — it is the blueprint of an object. Classes are special functions. You can define functions using function expressions and declarations and you can define classes that way as well. We can create the number of objects using the blueprint.

You can use the class keyword and the name of the class. The syntax is similar to that of Java.

Class syntax is a nice way to use object-oriented programming and managing prototypes:

```javascript
let Book = function(name) { 
   this.name = name
}
let newBook = function(name) {
   Book.call(this, name)
} 
newBook.prototype = Object.create(Book.prototype);
const book1 = new newBook("The Alchemist");
```

This is using ES6 class syntax:

```javascript
class Book {
   constructor(name) {
      this.name = name
   }
}
class newBook extends Book { 
   constructor(name) {
      super(name);
   }
}
const book1 = new newBook("The Alchemist");
```

Class syntax is syntactical sugar — behind the scenes, it still uses a prototype-based model. Classes are functions, and functions are objects in JavaScript. 

```javascript
class Book {
   constructor(title, author){ 
      this.title = title;
      this.author = author;
   } 
   summary() {
      console.log(`${this.title} written by ${this.author}`);
   }
}
const book1 = new Book("", "");
console.log(typeof Book); 
> "function"
console.log(typeof book1);
> "object"
```

<br />
<br />

# 3. Encapsulation <a id="encapsulation"></a>

The process of wrapping properties and functions within a single unit is known as **Encapsulation**. 

```javascript
const Book = function(t, a) {
   let title = t; 
   let author = a; 
   
   return {
      summary : function() { 
        console.log(`${title} written by ${author}.`);
      } 
   }
}
const book1 = new Book('Hippie', 'Paulo Coelho');
book1.summary();
> Hippie written by Paulo Coelho.
```
In the above code the `title` and the `author` are only visible inside the scope of the function `Book` and the method `summary` is visible to the caller of `Book`. So the `title` and the `author` are encapsulated inside `Book`.

<br />
<br />

# 4. Abstraction <a id="abstraction"></a>
It is a way of hiding the implementation details and only showing the essential features to the caller.

```javascript
const Book = function(getTitle, getAuthor) { 
    // Private variables / properties  
    let title = getTitle; 
    let author = getAuthor;
    // Public method 
    this.giveTitle = function() {
       return title;
    }
    
    // Private method
    const summary = function() {
       return `${title} written by ${author}.`
    }
    // Public method that has access to private method.
    this.giveSummary = function() {
       return summary()
    } 
}
const book1 = new Book('Hippie', 'Paulo Coelho');
book1.giveTitle();
> "Hippie"

book1.summary();
> Uncaught TypeError: book1.summary is not a function

book1.giveSummary();
> "Hippie written by Paulo Coelho."
```

<br />
<br />


# 5. Inheritance <a id="inheritance"></a>

It is a concept in which some property and methods of an Object is being used by another Object. Unlike most of the OOP languages where classes inherit classes, JavaScript Object inherits Object i.e. certain features (property and methods) of one object can be reused by other Objects. 

Lets’s understand inheritance with example: 

```javascript
//Inhertiance example 
class person{ 
	constructor(name){ 
		this.name = name; 
	} 
	//method to return the string 
	toString(){ 
		return (`Name of person: ${this.name}`); 
	} 
} 
class student extends person{ 
	constructor(name,id){ 
		//super keyword to for calling above class constructor 
		super(name); 
		this.id = id; 
	} 
	toString(){ 
		return (`${super.toString()},Student ID: ${this.id}`); 
	} 
} 
let student1 = new student('Mukul',22); 
console.log(student1.toString()); 
```

In the above example we define an `Person` Object with certain property and method and then we inherit the `Person` Object in the `Student` Object and use all the property and method of `Person` Object as well define certain property and methods for `Student`. 

**Note**: The `Person` and `Student` object both have same method i.e `toString()`, this is called as Method Overriding. Method Overriding allows method in a child class to have the same name and method signature as that of a `Parent` class. 

In the above code, `super` keyword is used to refer immediate parent class instance variable. 

<br />
<br />

# 6. Polymorphism <a id="polymorphism"></a>

The ability to call the same method on different objects and have each of them respond in their own way is called polymorphism.

```javascript
let book1 = function () {}
book1.prototype.summary = function() {
   return "summary of book1"
}
let book2 = function() {}
book2.prototype = Object.create(book1.prototype);
book2.prototype.summary = function() {                 
   return "summary of book2"
}
let book3 = function() {}
book3.prototype = Object.create(book1.prototype);
book3.prototype.summary = function() {
   return "summary of book3"
}
   
var books = [new book1(), new book2(), new book3()];
books.forEach(function(book){
   console.log(book.summary());
});

> summary of book1
> summary of book2
> summary of book3

```



**Ref** : [*Medium*](https://betterprogramming.pub/object-oriented-programming-in-javascript-b3bda28d3e81) |  [*Abstraction & Inheritance*](https://www.geeksforgeeks.org/introduction-object-oriented-programming-javascript/) 
