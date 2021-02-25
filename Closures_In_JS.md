<br /> **Table of Contents** : 
>
> *[1. What is Lexical Scope](#lexical_scope)* <br />
> *[2. Defination Of Closure](#define_closure)* <br /> 
> *[3. Closure Function Always Remember It's Outer Function's Scope](#closure_remember_scope)* <br />
> *[4. Closure Protect Variable Of Function](#closure_protects)* <br /> 
> *[5. Function Always Creates Closure](#function_always_creates_closure)* <br />
> <br />

<br />
<br />

# 1. What is Lexical Scope <a id="lexical_scope"></a>

Lexical Scope means that in a nested group of functions, the inner functions have access to the variables and other resources of their parent scope . This means that the child functions are lexically bound to the execution context of their parents.

<br />
<br />

# 2. Defination Of Closure <a id="define_closure"></a>
**Simply Remember** : When a function along with it's lexical scope, bundled together forms a closure.

let's understands with example : 

```html
<script>
	function x(){
        let a = 7; 
        let y = function (){
            console.log(a);
        }
        y();
    } 
    x();
</script>
```

In above example function `y()` have access to it's outer scope i.e. scope of function `x()`. So function `y()` can access the variable `a`. Now let's execute this code.

<br />

![closure_example_0.](images/js_closure_0.png "Closure example 1.")

In above code snippet we have put debugger at line no. 5, so when we refresh the page the debugger will pause at `console.log(a)` and we can see that on right hand inside scope section we are getting a **closure** as `a: 7`. So it is that easy to understand and define a closure.

<br />
<br />

# 3. Closure Function Always Remember It's Outer Function's Scope <a id="closure_remember_scope"></a>

let's understand it in more details with the help of another example :

![closure_example_1.](images/js_closure_1.png "Closure example 2.")

In above code snippet function `x()` returning a *'function defination'* of function `y()`. At line no. 10 variable `z` calling and storing the return value of function `x` i.e. defination of function `y`.

Before we move forward we need to keep in mind that all the varaibles are get garbage collected once a function get executed. 

So when we call functon `z` it will return value `7` as output, because of **closure** i.e. function `y` still *remembered* it's lexical scope even after function `x` has been executed and finished. In this case variable `a` will never get garbage collected by JS Engine because JS Engine know thats this variable is going to used in future by function `y`.


<br />
<br />

# 4. Closure Protect Variables Of Function <a id="closure_protects"></a>

With closure it is possible to **protect** the variables which are declared inside a function from accessing that particular variable from outside of it's *function scope*.

<br />

Let's understand with example :

Suppose you want to use a variable for counting something, and you want this counter to be available to all functions.

You could use a global variable, and a function to increase the counter :

```javascript
// Initiate counter
let counter = 0;

// Function to increment counter
function add() {
    counter += 1;
}

// Call add() 3 times
add();  // The counter should be 1
add();  // The counter should be 2
add();  // The counter should be 3

```

There is a problem with the solution above: Any code on the page can change the counter, without calling `add()` function.

The counter should be local to the `add()` function, to prevent other code from changing it.


<br />

So, here we can use closure to solve this problem as follow : 

```javascript
// Function to increment counter
function makeCounter() {
    let counter = 0;

    function plus (){
        counter = counter + 1;
        return counter;
    }

    return plus; //returing defination
}

let add = makeCounter(); // initiated 1st time to create add function

// Call add() 3 times
add();  // The counter should be 1
add();  // The counter should be 2
add();  // The counter should be 3
```

Here we can clearly observe that there is no chance for outer functions to access and change the value of `counter` variable.

<br />
<br />

# 5. Function Always Creates Closure <a id="function_always_creates_closure"></a>

Why it is always said that in JavaScript, closures are created every time a function is created ? 

Let's understand with an example :

```javascript 
var a = 10;

function test() {
  console.log(a); // will output 10
  console.log(b); // will output 6
}

var b = 6;
test();
```

When a JavaScript function is invoked, a new execution context is created. Together with the function arguments and the target object, this execution context also receives a link to the lexical environment of the calling execution context, meaning the variables declared in the outer lexical environment (in the above example, both `a` and `b`) are available from execution.

So, every function creates a closure because every function has a link to its outer lexical environment.

**Note** that variables themselves are visible from within a closure, not copies.

<br />

**Ref** : [*Closure Defination*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) | [*Video To Understand Closure*](https://youtu.be/qikxEIxsXco) | [*Counter Example*](https://www.w3schools.com/js/js_function_closures.asp) | [*Function Always Creates Closure*](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work#:~:text=Every%20function%20creates%20a%20closure,within%20a%20closure%2C%20not%20copies.) 

---