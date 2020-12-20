> <br /> **Table of Contents** : 
>
> *[1. Scope vs Context](#scope_vs_context)* <br />
> *[2. The JavaScript `this` Keyword](#this_keyword)* <br />
> *[3. `this` in Event Handlers](#this_in_evhandle)* <br />
> *[4. Object Method Binding](#obj_mtd_bind)* <br />
> *[5. Explicit Function Binding](#ex_fn_bind)* <br />
> *[6. `this` and object conversion](#obj_conv)* <br />
> *[7. The bind method](#bind_mtd)* <br />
> <br />

<br />
<br />

# 1. Scope vs Context <a id="scope_vs_context"></a>

Many developers often confuse **scope** and **context** as if they equally refer to the same concepts. But this is not the case. **Scope** can be define as **accessibility** and **availability** of variables, functions, and objects inside a particular part of your code during runtime. In other words, scope determines the **visibility** of variables and other resources in areas of your code. Where as **Context** is used to refer to the value of `this` in some particular part of your code.

<br />
<br />

# 2. The JavaScript `this` Keyword <a id="this_keyword"></a>

**Remember** : The value of Javascript's `this` keyword refers to the object it belongs to.

It has different values depending on where it is used :

- In a method, `this` refers to the **owner object**.
- Alone, `this` refers to the **global object**.
- In a function, `this` refers to the **global object**.
- In a function, in strict mode, `this` is `undefined`.
- In an event, `this` refers to the **element** that received the **event**.
- Methods like `call()`, and `apply()` can refer `this` to any object.


<br />
<br />

# 3. `this` in Event Handlers <a id="this_in_evhandle"></a>

In **HTML** event handlers, `this` refers to the **HTML element** that received the **event**:

```html
<button onclick="this.style.display='none'">
  Click to Remove Me!
</button>
```

<br />
<br />

# 4. Object Method Binding <a id="obj_mtd_bind"></a>

In these examples, `this` is the person object (The person object is the "owner" of the function):

```javascript
var person = {
    firstName: "John",
    lastName : "Doe",
    id       : 5566,
    fullName : function() {
        return this.firstName + " " + this.lastName;
    }
};
```
In other words: `this.firstName` means the `firstName` property of `this` (person) object.

<br />
<br />

# 5. Explicit Function Binding <a id="ex_fn_bind"></a>

The `call()` and `apply()` methods are predefined JavaScript methods.
They both are used to call a **function** or a **object's method** with another **object** as **argument**.

Example with **function** :

```javascript
// An object can be passed as the first argument to call or apply and this will be bound to it.
var obj = {a: 'Custom'};

// We declare a variable and the variable is assigned to the global window as its property.
var a = 'Global';

function whatsThis() {
  return this.a;  // The value of this is dependent on how the function is called
}

whatsThis();          // it value is 'Global' because `this` in the function isn't set, so it defaults to the global/window object 
whatsThis.call(obj);  // it value is 'Custom' because this in the function is set to obj
whatsThis.apply(obj); // it value is 'Custom' because this in the function is set to obj
```

<br />

Example with **object's method** :

```javascript
// In the example below, when calling person1.fullName with person2 as argument, this will refer to person2, even if it is a method of person1

var person1 = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
var person2 = {
  firstName:"John",
  lastName: "Doe",
}
person1.fullName.call(person2);  // Will return "John Doe"
```

<br />
<br />

# 6. `this` and object conversion <a id="obj_conv"></a>

```javascript
function add(c, d) {
  return this.a + this.b + c + d;
}

var o = {a: 1, b: 3};

// The first parameter is the object to use as
// 'this', subsequent parameters are passed as
// arguments in the function call
add.call(o, 5, 7); // 16

// The first parameter is the object to use as
// 'this', the second is an array whose
// members are used as the arguments in the function call
add.apply(o, [10, 20]); // 34
```

<br />
<br />

# 7. The bind method <a id="bind_mtd"></a>

ECMAScript 5 introduced `Function.prototype.bind()`. Calling `f.bind(someObject)` creates a new function with the same body and scope as `f`, but where `this` occurs in the original function, in the new function it is permanently bound to the first argument of `bind`, regardless of how the function is being used.

```javascript
function f() {
  return this.a;
}

var g = f.bind({a: 'azerty'});
console.log(g()); // azerty

var h = g.bind({a: 'yoo'}); // bind only works once!
console.log(h()); // azerty

var o = {a: 37, f: f, g: g, h: h};
console.log(o.a, o.f(), o.g(), o.h()); // 37,37, azerty, azerty
```

<br />

Another simple example to understand bind :

```javascript
//Use .bind() javascript

var obj = {name:"Saurabh"};

var greeting = function(a,b,c){
    return "welcome "+this.name+" to "+a+" "+b+" in "+c;
};

//creates a bound function that has same body and parameters 
var bound = greeting.bind(obj); 

console.log(bound("Newtown","KOLKATA","WB")); //call the bound function

/* the output will be 
Output using .bind() below
welcome Niladri to Newtown KOLKATA in WB */
```

<br />
<br />



**Ref**: [*w3school*](https://www.w3schools.com/js/js_this.asp) | [*Scope vs Context*](https://scotch.io/tutorials/understanding-scope-in-javascript#toc-context) | [*MDN Web Docs*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) | [*Bind Function*](https://www.codementor.io/@niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp)

---