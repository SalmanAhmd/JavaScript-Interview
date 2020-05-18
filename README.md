# Interview Preparation

-------------------------------------------------------------------------------
### 1. Explain "hoisting".

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.

Example 01: Variable Hoisting
```
console.log(message); // output : undefined
var message = "The variable Has been hoisted";
```
The above code looks like as below to the interpreter,
```
var message;
console.log(message);
message = "The variable Has been hoisted";
```
Example 02: Function Hoisting
```
function hoist() {
  a = 20;
  var b = 100;
}

hoist();
console.log(a); 
/* 
Accessible as a global variable outside hoist() function
Output: 20
*/

console.log(b); 
/*
Since it was declared, it is confined to the hoist() function scope.
We can't print it out outside the confines of the hoist() function.
Output: ReferenceError: b is not defined
*/
```
All declarations (function, var, let, const and class) are hoisted in JavaScript, while the var declarations are initialized with undefined, but let and const declarations remain uninitialized.
```
console.log(a);
let a = 3;

// Output: ReferenceError: a is not defined
```
They will only get initialized when their lexical binding (assignment) is evaluated during runtime by the JavaScript engine. This means we can’t access the variable before the engine evaluates its value at the place it was declared in the source code. This is what we call Temporal Dead Zone, A time span between variable creation and its initialization where they can’t be accessed.

Note: JavaScript only hoists declarations, not initialisation

--------------------------------------------------------------------------------
### 2. What are the differences between variables created using let, var or const?

Variables declared using the var keyword are scoped to the function in which they are created, or if created outside of any function, to the global object. let and const are block scoped, meaning they are only accessible within the nearest set of curly braces (function, if-else block, or for-loop).
```
function foo() {
  // All variables are accessible within functions.
  var bar = 'bar';
  let baz = 'baz';
  const qux = 'qux';

  console.log(bar); // bar
  console.log(baz); // baz
  console.log(qux); // qux
}

console.log(bar); // ReferenceError: bar is not defined
console.log(baz); // ReferenceError: baz is not defined
console.log(qux); // ReferenceError: qux is not defined
if (true) {
  var bar = 'bar';
  let baz = 'baz';
  const qux = 'qux';
}

// var declared variables are accessible anywhere in the function scope.
console.log(bar); // bar
// let and const defined variables are not accessible outside of the block they were defined in.
console.log(baz); // ReferenceError: baz is not defined
console.log(qux); // ReferenceError: qux is not defined
```
var allows variables to be hoisted, meaning they can be referenced in code before they are declared. let and const will not allow this, instead throwing an error.
```
console.log(foo); // undefined
var foo = 'foo';

console.log(baz); // ReferenceError: can't access lexical declaration 'baz' before initialization
let baz = 'baz';

console.log(bar); // ReferenceError: can't access lexical declaration 'bar' before initialization
const bar = 'bar';
```
Redeclaring a variable with var will not throw an error, but 'let' and 'const' will.
```
var foo = 'foo';
var foo = 'bar';
console.log(foo); // "bar"

let baz = 'baz';
let baz = 'qux'; // Uncaught SyntaxError: Identifier 'baz' has already been declared
```
let and const differ in that let allows reassigning the variable's value while const does not.
```
// This is fine.
let foo = 'foo';
foo = 'bar';

// This causes an exception.
const baz = 'baz';
baz = 'qux';
```
--------------------------------------------------------------------------------
### 3. Can you give an example for destructuring an object or an array?

The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.
```
let a, b, rest;
[a, b] = [10, 20];
console.log(a); // 10
console.log(b); // 20

[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20


// Stage 4(finished) proposal
({a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40});
console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c: 30, d: 40}
```

Destructuring is an expression available in ES6 which enables a succinct and convenient way to extract values of Objects or Arrays and place them into distinct variables.

**Array Destructuring**
```
// Variable assignment.
const foo = ['one', 'two', 'three'];
const [one, two, three] = foo;

console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"
// Swapping variables
let a = 1;
let b = 3;

[a, b] = [b, a];
console.log(a); // 3
console.log(b); // 1
```
**Object Destructuring**
```
// Variable assignment.
const o = { p: 42, q: true };
const { p, q } = o;

console.log(p); // 42
console.log(q); // true
```
> [Resource](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

--------------------------------------------------------------------------------
### 4. Can you give an example of generating a string with ES6 Template Literals?

Template Literal in ES6 provides new features to create a string that gives more control over dynamic strings. Traditionally, String is created using single quotes (‘) or double quotes (“) quotes. Template literal is created using the backtick (`) character

Multiline Strings: In-order to create a multiline string an escape sequence \n was used to give a new line character. However, Template Literals there is no need to add \n string ends only when it gets backtick (`) character.
```
console.log('Some text that I want \non two lines!');
  
// With template literal
console.log(`Some text that I want
on two lines!`);
```
Expressions: To dynamically add values into new Template Literals expressions are used. The ${} syntax allows an expression in it that produces the value.
```
<script>
let principal = 1000;
let noofyears = 1;
let rateofinterest = 7;
  
let SI = `Simple Interest is ${(principal *
            noofyears * rateofinterest)/100}`;
alert("Simple Interest is" + SI);
</script>
 ```
 
Tagged Templates: One of the features of Template Literals is its ability to create Tagged Template Literals. Tagged Literal is written like a function definition, but the difference is when this literal is called. There is no parenthesis() to a literal call. An array of Strings are passed as a parameter to a literal.
```
function TaggedLiteralEg(strings) {
   console.log(strings)
}
 TaggedLiteralEg `GeeksforGeeks`;
```

Template literals are string literals allowing embedded expressions.

Benefits

* String interpolation
* Embedded expressions
* Multiline strings without hacks
* String formatting
* String tagging for safe HTML escaping, localization and more

-------------------------------------------------------------------------------
### 5. How do you compare Object and Map?

Objects are similar to Maps in that both let you set keys to values, retrieve those values, delete keys, and detect whether something is stored at a key. Due to this reason, Objects have been used as Maps historically. But there are important differences that make using a Map preferable in certain cases.

* The keys of an Object are Strings and Symbols, whereas they can be any value for a Map, including functions, objects, and any primitive.
* The keys in Map are ordered while keys added to object are not. Thus, when iterating over it, a Map object returns keys in order of insertion.
* You can get the size of a Map easily with the size property, while the number of properties in an Object must be determined manually.
* A Map is an iterable and can thus be directly iterated, whereas iterating over an Object requires obtaining its keys in some fashion and iterating over them.
* An Object has a prototype, so there are default keys in the map that could collide with your keys if you're not careful. As of ES5 this can be bypassed by using map = Object.create(null), but this is seldom done.
* A Map may perform better in scenarios involving frequent addition and removal of key pairs.

> [Geeks](https://www.geeksforgeeks.org/map-vs-object-in-javascript/)

-------------------------------------------------------------------------------
### 6. What is scope in javascript?

In JavaScript there are two types of scope:

* Local scope
* Global scope
JavaScript has function scope: Each function creates a new scope.

Scope determines the accessibility (visibility) of these variables.

Variables defined inside a function are not accessible (visible) from outside the function.

# Local JavaScript Variables
Variables declared within a JavaScript function, become **LOCAL** to the function.

Local variables have **Function scope**: They can only be accessed from within the function.
```
// code here can NOT use carName

function myFunction() {
  var carName = "Volvo";

  // code here CAN use carName

}
```
Since local variables are only recognized inside their functions, variables with the same name can be used in different functions.

Local variables are created when a function starts, and deleted when the function is completed.
# Global JavaScript Variables
A variable declared outside a function, becomes **GLOBAL**.

A global variable has **global scope**: All scripts and functions on a web page can access it. 
```
var carName = "Volvo";

// code here can use carName

function myFunction() {

  // code here can also use carName

}
```
# Automatically Global
If you assign a value to a variable that has not been declared, it will automatically become a **GLOBAL** variable.

This code example will declare a global variable ```carName```, even if the value is assigned inside a function.
```
myFunction();

// code here can use carName

function myFunction() {
  carName = "Volvo";
}
```
> In "Strict Mode", undeclared variables are not automatically global.

-------------------------------------------------------------------------------
### 7. What are global variables?

Global variables are those that are available throughout the length of the code without any scope. The var keyword is used to declare a local variable but if you omit it then it will become global variable
```
msg = "Hello" // var is missing, it becomes global variable
```
The problem with global variables is the conflict of variable names of local and global scope. It is also difficult to debug and test the code that relies on global variables.

-------------------------------------------------------------------------------
### 8. What are the differences between undeclared and undefined variables?

Below are the major differences between undeclared and undefined variables,
undeclared | undeclared 
--- | ---
These variables do not exist in a program and are not declared | These variables declared in the program but have not assigned any value
If you try to read the value of an undeclared variable, then a runtime error is encountered | If you try to read the value of an undefined variable, an undefined value is returned.

-------------------------------------------------------------------------------
### 9. How do you assign default values to variables?

You can use the logical or operator || in an assignment expression to provide a default value. The syntax looks like as below,

var a = b || c;
As per the above expression, variable 'a 'will get the value of 'c' only if 'b' is falsy (if is null, false, undefined, 0, empty string, or NaN), otherwise 'a' will get the value of 'b'.

> some time we use nullish ??

-------------------------------------------------------------------------------
### 10. What are the benefits of keeping declarations at the top?

It is recommended to keep all declarations at the top of each script or function. The benefits of doing this are,

* Gives cleaner code
* It provides a single place to look for local variables
* Easy to avoid unwanted global variables
* It reduces the possibility of unwanted re-declarations
