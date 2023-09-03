> <br /> **Table of Contents** : 
>
> *[1. What Is Scope ?](#what_is_scope)* <br />
> *[2. Block Scope](#block_scope)* <br />
> *[3. `var` Is Not Block Scoped](#var_block_scope)* <br />
> *[4. Function Scope](#function_scope)* <br />
> *[5. Module Scope](#module_scope)* <br />
> *[6. Scopes Can Be Nested](#nested_scope)* <br />
> *[7. Global Scope](#global_scope)* <br />
> *[8. Lexical Scope](#lexical_scope)* <br />
> <br />

<br />
<br />

# 1. What Is Scope ? <a id="what_is_scope"></a>

Scope can be define as **accessibility** and **availability** of variables, functions, and objects inside a particular part of your code during runtime. In other words, scope determines the **visibility** of variables and other resources in areas of your code.

Let's understand this by declaring one variable `message`.

<br />

```javascript
const message = 'Hello';
console.log(message); // 'Hello'
```
<br />

Then, you could easily log this variable in the next line after the declaration. No questions here.

Now, let’s move the declaration of `message` inside of an if code block :

<br />

```javascript
if (true) {
  const message = 'Hello';
}
console.log(message); // ReferenceError: message is not defined
```
<br />

This time, when trying to **log** the variable, JavaScript throws `ReferenceError: message is not defined`.

**Why does it happen?**

The `if` code block creates a scope for `message` variable. And `message` variable can be accessed only within this scope.

At a higher level, the **accessibility** of variables is **limited** by the **scope** where they’re created. You are free to **access** the variable defined within its scope. But outside of its scope, the variable is **inaccessible**.

<br />
<br />

# 2. Block Scope <a id="block_scope"></a>

A code block in JavaScript defines a `scope` called `Block Scope` for variables declared using `let` and `const` :

<br />

```javascript
if (true) {
  // "if" block scope
  const message = 'Hello';
  console.log(message); // 'Hello'
}
console.log(message); // throws ReferenceError
```
<br />

The first `console.log(message)` correctly logs the variable because message is accessed from the scope where it is defined.

But the second `console.log(message)` throws a reference error because message variable is accessed outside of its scope: the variable doesn’t exist here.

The code block of `if`, `for`, `while` statements also create a scope.

In JavaScript you can define standalone code blocks. The standalone code blocks also delimit a scope:

<br />

```javascript
{
  // block scope
  const message = 'Hello';
  console.log(message); // 'Hello'
}
console.log(message); // throws ReferenceError
```
<br />
<br />

# 3. `var` Is Not Block Scoped <a id="var_block_scope"></a>

As seen in the previous section, the code block creates a scope for variables declared using `const` and `let`. However, that’s not the case of variables declared using `var`.

The snippet below declares a variable `count` using a `var` keyword:

<br />

```javascript
if (true) {
  // "if" block scope
  var count = 1;
  console.log(count); // 1
}
console.log(count); // 1
```
<br />

`count` variable, as expected, is accessible within the scope of `if` code block. However, `count` variable is also accessible outside!

A *code block does not create a scope* for `var` variables, but a *function body does*. Read the previous sentence again, and try to remember it.

Let’s continue on the function scope in the next section.

<br />
<br />

# 4. Function Scope <a id="function_scope"></a>

A `function` body in JavaScript defines a scope for variables declared using `var`, `let` and `const`.

Let’s declare a `var` variable within a function body :

<br />

```javascript
function run() {
  // "run" function scope
  var message = 'Run, Forrest, Run!';
  console.log(message); // 'Run, Forrest, Run!'
}

run();
console.log(message); // throws ReferenceError
```
<br />

`run()` function body creates a scope. The variable `message` is accessible inside of the function scope, but inaccessible outside.

Same way, a function body creates a scope for `let`, `const` and even `function` declarations.

<br />

```javascript
function run() {
  // "run" function scope
  const two = 2;
  let count = 0;
  function run2() {}

  console.log(two);   // 2
  console.log(count); // 0
  console.log(run2);  // function
}

run();
console.log(two);   // throws ReferenceError
console.log(count); // throws ReferenceError
console.log(run2);  // throws ReferenceError
```

<br />
<br />

# 5. Module Scope <a id="module_scope"></a>

ES2015 module also creates a scope for **variables**, **functions**, **classes**.

The module circle defines a constant `pi` (*for some internal usuage*) :

<br />

```javascript
// "circle" module scope
const pi = 3.14159;

console.log(pi); // 3.14159

// Usage of pi
```

<br />

`pi` variable is declared within the scope of `circle` module. Also, the variable `pi` is not exported from the module.

Then the `circle` module is imported:

<br />

```javascript
import './circle';

console.log(pi); // throws ReferenceError
```

<br />

The variable `pi` is not accessible outside of `circle` module (*unless explicitly exported using export*).

The module scope makes the module **encapsulated**. Every private variable (*that’s not exported*) remains an internal detail of the module, and the module scope **protects** these variables from being accessed outside.

Looking from another angle, the scope is an **encapsulation mechanism** for code **blocks**, **functions**, and **modules**.

<br />
<br />

# 6. Scopes Can Be Nested <a id="nested_scope"></a>

An interesting property of scopes is that they can be nested.

In the following example the function `run()` creates a scope, and inside an `if` condition code block creates another scope :

<br />

```javascript
function run() {
  // "run" function scope
  const message = 'Run, Forrest, Run!';

  if (true) {
    // "if" code block scope
    const friend = 'Bubba';
    console.log(message); // 'Run, Forrest, Run!'
  }

  console.log(friend); // throws ReferenceError
}

run();
```

<br />

`if` code block scope is nested inside the `run()` function scope. Scopes of any type (*code block, function, module*) can be nested.

The scope contained within another scope is named inner scope. In the example, `if` code block scope is an inner scope of `run()` function scope.

The scope that wraps another scope is named outer scope. In the example, `run()` function scope is an outer scope to `if` code block scope.

<br />
<br />

# 7. Global Scope <a id="global_scope"></a>

When you start writing JavaScript in a document, you are already in the Global scope. There is only one Global scope throughout a JavaScript document.

The global scope is the outermost scope. It is accessible from any inner (*aka local*) scope. 
<br />

```javascript
var name = 'Hammad';

console.log(name); // logs 'Hammad'

function logName() {
    console.log(name); // 'name' is accessible here and everywhere else
}

logName(); // logs 'Hammad'
```

<br />

A variable declared inside the global scope is named **global** variable. Global variables can be accessed and altered in any other scope.

The global scope is a mechanism that lets the host of JavaScript (*browser, Node*) supply applications with host-specific functions as global variables.

`window` and `document`, for example, are global variables supplied by the browser. In a Node environment, you can access `process` object as a global variable.


<br />
<br />

# 8. Lexical Scope <a id="lexical_scope"></a>

Lexical Scope means that in a nested group of functions, the inner functions have access to the variables and other resources of their parent scope . This means that the child functions are lexically bound to the execution context of their parents. 

<br />

```javascript
function outerFunc() {
  // the outer scope
  let outerVar = 'I am from outside!';

  function innerFunc() {
    // the inner scope
    console.log(outerVar); // 'I am from outside!'
  }

  return innerFunc;
}

const inner = outerFunc();
inner();
```

<br />

The thing you will notice about lexical scope is that it works forward, meaning `innerFunc()` can be accessed by its children's execution contexts. But it doesn't work backward to its parents, meaning that the variable `outerFunc()` cannot be accessed by its parents. And that's why lexical scope is also referred as static scope.

<br />

> **Remember** : The **static** scope is not defined at runtime, rather it can be accessed at runtime. But **dynamic** scoping uses execution time: it gives you the value that you most recently assigned to a given name.



<br />

**Ref** : [*Scopes In Details*](https://dmitripavlutin.com/javascript-scope/) | [*Lexical Scope*](https://astronautweb.co/javascript-lexical-scope/) | [*Scope Defination*](https://scotch.io/tutorials/understanding-scope-in-javascript#toc-lexical-scope) | [*Static vs Dynamic Scoping*](https://www.cs.cornell.edu/~asampson/blog/scope.html#:~:text=Static%20scoping%20matches%20variable%20references,assigned%20to%20a%20given%20name.)

---