# Interview Preparation

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

-------------------------------------------------------------------------------
### 11. What are the benefits of initializing variables?

It is recommended to initialize variables because of the below benefits,

* It gives cleaner code
* It provides a single place to initialize variables
* Avoid undefined values in the code

-------------------------------------------------------------------------------
### 12. What is a spread operator?

```
var firstGroup = ["C", "C++", "Java"];
var secondGroup = ["SQL", "MySQL", "BigData"];
var thirdGroup = ["Android", "Python", "Ruby", firstGroup, secondGroup];
var finalGroup = ["Android", "Python", "Ruby", ...firstGroup, ...secondGroup];

console.log(thirdGroup); 
// ["Android", "Python", "Ruby", ["C", "C++", "Java"], ["SQL", "MySQL", "BigData"]]
console.log(finalGroup); 
// ["Android", "Python", "Ruby", "C", "C++", "Java", "SQL", "MySQL", "BigData"]
```
> Works for **Object** too

> [Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

-------------------------------------------------------------------------------
### 13. What's the difference between a variable that is: null, undefined or undeclared?

**Undeclared** variables are created when you assign a value to an identifier that is not previously created using `var`, `let` or `const`. Undeclared variables will be defined globally, outside of the current scope. In strict mode, a `ReferenceError` will be thrown when you try to assign to an undeclared variable. Undeclared variables are bad just like how global variables are bad. Avoid them at all cost! To check for them, wrap its usage in a `try`/`catch` block.
```javascript
function foo() {
  x = 1; // Throws a ReferenceError in strict mode
}
foo();
console.log(x); // 1
```
A variable that is **`undefined`** is a variable that has been declared, but not assigned a value. It is of type `undefined`. If a function does not return any value as the result of executing it is assigned to a variable, the variable also has the value of `undefined`. To check for it, compare using the strict equality (`===`) operator or `typeof` which will give the `'undefined'` string. Note that you should not be using the abstract equality operator to check, as it will also return `true` if the value is `null`.
```javascript
var foo;
console.log(foo); // undefined
console.log(foo === undefined); // true
console.log(typeof foo === 'undefined'); // true
console.log(foo == null); // true. Wrong, don't use this to check!
function bar() {}
var baz = bar();
console.log(baz); // undefined
```
A variable that is **`null`** will have been explicitly assigned to the `null` value. It represents no value and is different from `undefined` in the sense that it has been explicitly assigned. To check for `null,` simply compare using the strict equality operator. Note that like the above, you should not be using the abstract equality operator (`==`) to check, as it will also return `true` if the value is `undefined`.
```javascript
var foo = null;
console.log(foo === null); // true
console.log(typeof foo === 'object'); // true
console.log(foo == undefined); // true. Wrong, don't use this to check!
```
As a personal habit, I never leave my variables undeclared or unassigned. I will explicitly assign `null` to them after declaring if I don't intend to use it yet. If you use a linter in your workflow, it will usually also be able to check that you are not referencing undeclared variables.

-------------------------------------------------------------------------------
### 14. What is a closure, and how/why would you use one?

A closure is the combination of a function and the lexical environment within which that function was declared. The word "lexical" refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. Closures are functions that have access to the outer (enclosing) function's variables—scope chain even after the outer function has returned.

**Why would you use one?**

* Data privacy / emulating private methods with closures. Commonly used in the [module pattern](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript).
* [Partial applications or currying](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8#.l4b6l1i3x).

> [W3School](https://www.w3schools.com/js/js_function_closures.asp)

---------------------------
### 15. What's a typical use case for anonymous functions?

They can be used in IIFEs to encapsulate some code within a local scope so that variables declared in it do not leak to the global scope.
```javascript
(function() {
  // Some code here.
})();
```
As a callback that is used once and does not need to be used anywhere else. The code will seem more self-contained and readable when handlers are defined right inside the code calling them, rather than having to search elsewhere to find the function body.
```javascript
setTimeout(function() {
  console.log('Hello world!');
}, 1000);
```
Arguments to functional programming constructs or Lodash (similar to callbacks).
```javascript
const arr = [1, 2, 3];
const double = arr.map(function(el) {
  return el * 2;
});
console.log(double); // [2, 4, 6]
```
An anonymous function is a function without a name! Anonymous functions are commonly assigned to a variable name or used as a callback function. The syntax would be as below,
```javascript
function (optionalParameters) {
  //do something
}
const myFunction = function(){ //Anonymous function assigned to a variable
  //do something
};
[1, 2, 3].map(function(element){ //Anonymous function used as a callback function
  //do something
});
```
Let's see the above anonymous function in an example,
```javascript
var x = function (a, b) {return a * b};
var z = x(5, 10);
console.log(z); // 50
```
Anonymous functions basically used in following scenario.

a.) No name is needed if function is only used in one place, then there is no need to add a name to function.
Let's take the example of setTimeout function 
```javascript
setTimeout(function(){
	alert("Hello");
},1000);
```
Here there is no need of using named function when we are sure 	that function which will alert `hello` would use only once in	application.

b.) Anonymous functions are declared inline and inline functions have advantages in the case that they can access variable in the parent scopes.
Let's take a example of event handler. Notify event of particular 	type (such as click) for a given object. 
Let say we have HTML element (button) on which we want to add click event and when user do click on button we would like toexecute some logic.
```html
<button id="myBtn"></button>
```
Add Event Listener 
```javascript
var btn = document.getElementById('myBtn');
btn.addEventListener('click', function () {
  alert('button clicked');
});
```
	
Above example shows used of anonymous function as a callback function in event handler.
	
c.) Passing anonymous function as a parameter to calling function.
	
**Example:** 
```javascript
// Function which will execute callback function
function processCallback(callback){
	if(typeof callback === 'function'){
		callback();
	}
}
// Call function and pass anonymous function as callback 
processCallback(function(){
	alert("Hi I am anonymous callback function");
});
```
The best way to make a decision for using anonymous function is to ask the following question:
Will the function which I am going to define, be used anywhere else?
If your answer is yes then go and create named function rather anonymous function.
**Advantage of using anonymous function:**
* It can reduce a bit of code, particularly in recursive function and in callback function.
* Avoid needless global namespace pollutions.

---------------------------
### 16. Explain the difference between: function Person(){}, var person = Person(), and var person = new Person()?

This question is pretty vague. My best guess at its intention is that it is asking about constructors in JavaScript. Technically speaking, `function Person(){}` is just a normal function declaration. The convention is to use PascalCase for functions that are intended to be used as constructors.

`var person = Person()` invokes the `Person` as a function, and not as a constructor. Invoking as such is a common mistake if the function is intended to be used as a constructor. Typically, the constructor does not return anything, hence invoking the constructor like a normal function will return `undefined` and that gets assigned to the variable intended as the instance.

`var person = new Person()` creates an instance of the `Person` object using the `new` operator, which inherits from `Person.prototype`. An alternative would be to use `Object.create`, such as: `Object.create(Person.prototype)`.
```javascript
function Person(name) {
  this.name = name;
}
var person = Person('John');
console.log(person); // undefined
console.log(person.name); // Uncaught TypeError: Cannot read property 'name' of undefined
var person = new Person('John');
console.log(person); // Person { name: "John" }
console.log(person.name); // "john"
```

--------------------------
### 17. Explain Function.prototype.bind

The simplest use of bind() is to make a function that, no matter how it is called, is called with a particular this value.
```
x = 9;
var module = {
    x: 81,
    getX: function () {
        return this.x;
    }
};

module.getX(); // 81

var getX = module.getX;
getX(); // 9, because in this case, "this" refers to the global object

// create a new function with 'this' bound to module
var boundGetX = getX.bind(module);
boundGetX(); // 81
```

---------------------------
### 18. Explain the difference between synchronous and asynchronous functions.

Synchronous functions are blocking while asynchronous functions are not. In synchronous functions, statements complete before the next statement is run. In this case, the program is evaluated exactly in order of the statements and execution of the program is paused if one of the statements take a very long time.

Asynchronous functions usually accept a callback as a parameter and execution continue on the next line immediately after the asynchronous function is invoked. The callback is only invoked when the asynchronous operation is complete and the call stack is empty. Heavy duty operations such as loading data from a web server or querying a database should be done asynchronously so that the main thread can continue executing other operations instead of blocking until that long operation to complete (in the case of browsers, the UI will freeze).

---------------------------
### 19. What are the differences between ES6 class and ES5 function constructors?

```javascript
// ES5 Function Constructor
function Person(name) {
  this.name = name;
}

// ES6 Class
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

For simple constructors, they look pretty similar.

The main difference in the constructor comes when using inheritance. If we want to create a `Student` class that subclasses `Person` and add a `studentId` field, this is what we have to do in addition to the above.

```javascript
// ES5 Function Constructor
function Student(name, studentId) {
  // Call constructor of superclass to initialize superclass-derived members.
  Person.call(this, name);

  // Initialize subclass's own members.
  this.studentId = studentId;
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

// ES6 Class
class Student extends Person {
  constructor(name, studentId) {
    super(name);
    this.studentId = studentId;
  }
}
```

It's much more verbose to use inheritance in ES5 and the ES6 version is easier to understand and remember.

---------------------------
### 20. Can you offer a use case for the new arrow => function syntax? How does this new syntax differ from other functions?
### 21. What advantage is there for using the arrow syntax for a method in a constructor?

> [Medium Post](https://medium.com/tfogo/advantages-and-pitfalls-of-arrow-functions-a16f0835799e)

-------------------------------------------------------------------------
### 22. What is the definition of a higher-order function?

A higher-order function is any function that takes one or more functions as arguments, which it uses to operate on some data, and/or returns a function as a result. Higher-order functions are meant to abstract some operation that is performed repeatedly. The classic example of this is `map`, which takes an array and a function as arguments. `map` then uses this function to transform each item in the array, returning a new array with the transformed data. Other popular examples in JavaScript are `forEach`, `filter`, and `reduce`. A higher-order function doesn't just need to be manipulating arrays as there are many use cases for returning a function from another function. `Function.prototype.bind` is one such example in JavaScript.

**Map**

Let say we have an array of names which we need to transform each string to uppercase.

```javascript
const names = ['irish', 'daisy', 'anna'];
```

The imperative way will be as such:

```javascript
const transformNamesToUppercase = function(names) {
  const results = [];
  for (let i = 0; i < names.length; i++) {
    results.push(names[i].toUpperCase());
  }
  return results;
};
transformNamesToUppercase(names); // ['IRISH', 'DAISY', 'ANNA']
```

Use `.map(transformerFn)` makes the code shorter and more declarative.

```javascript
const transformNamesToUppercase = function(names) {
  return names.map(name => name.toUpperCase());
};
transformNamesToUppercase(names); // ['IRISH', 'DAISY', 'ANNA']
```
> [Resource](https://dev.to/damcosset/higher-order-functions-in-javascript-4j8b)

-------------------------------------------------------------------------
### 23. What happens if you write constructor more than once in a class?

> [StackOverFlow](https://stackoverflow.com/questions/32626524/why-doesnt-javascript-es6-support-multi-constructor-classes/32626901)

-------------------------------------------------------------------------
### 24. How do you get the prototype of an object?

> [StackOverFlow](https://stackoverflow.com/questions/7662147/how-to-access-object-prototype-in-javascript)

-------------------------------------------------------------------------
### 25. Is all objects have prototypes?

> [StackOverFlow](https://stackoverflow.com/questions/12661416/it-is-said-that-all-javascript-objects-have-a-prototype-property-but-i-only-see)

-------------------------------------------------------------------------
### 26. What is prototype chain?

> [Medium](https://medium.com/@toastui/javascripts-prototype-chain-made-easy-adbcd5a76e75)

-------------------------------------------------------------------------
### 27. What are closures?

A closure is the combination of a function and the lexical environment within which that function was declared. i.e, It is an inner function that has access to the outer or enclosing function’s variables. The closure has three scope chains

* Own scope where variables defined between its curly brackets
* Outer function’s variables
* Global variables

```javascript
function Welcome(name) {
  var greetingInfo = function(message) {
    console.log(message+' '+name);
  }
  return greetingInfo;
}
var myFunction = Welcome('John');
myFunction('Welcome '); // Output: Welcome John
myFunction('Hello Mr.'); // output: Hello Mr.John
```
As per the above code, the inner `function greetingInfo()` has access to the variables in the outer `function Welcome()` even after outer function has returned.

> [W3School](https://www.w3schools.com/js/js_function_closures.asp) | 
> [Medium](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)

-------------------------------------------------------------------------
### 28. What language constructions do you use for iterating over object properties and array items?

For objects:

* `for-in` loops - `for (var property in obj) { console.log(property); }`. However, this will also iterate through its inherited properties, and you will add an `obj.hasOwnProperty(property)` check before using it.
* `Object.keys()` - `Object.keys(obj).forEach(function (property) { ... })`. `Object.keys()` is a static method that will lists all enumerable properties of the object that you pass it.
* `Object.getOwnPropertyNames()` - `Object.getOwnPropertyNames(obj).forEach(function (property) { ... })`. `Object.getOwnPropertyNames()` is a static method that will lists all enumerable and non-enumerable properties of the object that you pass it.

For arrays:

* `for` loops - `for (var i = 0; i < arr.length; i++)`. The common pitfall here is that `var` is in the function scope and not the block scope and most of the time you would want block scoped iterator variable. ES2015 introduces `let` which has block scope and it is recommended to use that instead. So this becomes: `for (let i = 0; i < arr.length; i++)`.
* `forEach` - `arr.forEach(function (el, index) { ... })`. This construct can be more convenient at times because you do not have to use the `index` if all you need is the array elements. There are also the `every` and `some` methods which will allow you to terminate the iteration early.
* `for-of` loops - `for (let elem of arr) { ... }`. ES6 introduces a new loop, the `for-of` loop, that allows you to loop over objects that conform to the [iterable protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol) such as `String`, `Array`, `Map`, `Set`, etc. It combines the advantages of the `for` loop and the `forEach()` method. The advantage of the `for` loop is that you can break from it, and the advantage of `forEach()` is that it is more concise than the `for` loop because you don't need a counter variable. With the `for-of` loop, you get both the ability to break from a loop and a more concise syntax.

Most of the time, I would prefer the `.forEach` method, but it really depends on what you are trying to do. Before ES6, we used `for` loops when we needed to prematurely terminate the loop using `break`. But now with ES6, we can do that with `for-of` loops. I would use `for` loops when I need even more flexibility, such as incrementing the iterator more than once per loop.

Also, when using the `for-of` loop, if you need to access both the index and value of each array element, you can do so with the ES6 Array `entries()` method and destructuring:

```javascript
const arr = ['a', 'b', 'c'];

for (let [index, elem] of arr.entries()) {
  console.log(index, ': ', elem);
}
```

-------------------------------------------------------------------------
### 29. Can you describe the main difference between the Array.forEach() loop and Array.map() methods and why you would pick one versus the other?

To understand the differences between the two, let's look at what each function does.

**`forEach`**

* Iterates through the elements in an array.
* Executes a callback for each element.
* Does not return a value.

```javascript
const a = [1, 2, 3];
const doubled = a.forEach((num, index) => {
  // Do something with num and/or index.
});

// doubled = undefined
```

**`map`**

* Iterates through the elements in an array.
* "Maps" each element to a new element by calling the function on each element, creating a new array as a result.

```javascript
const a = [1, 2, 3];
const doubled = a.map(num => {
  return num * 2;
});

// doubled = [2, 4, 6]
```

The main difference between `.forEach` and `.map()` is that `.map()` returns a new array. If you need the result, but do not wish to mutate the original array, `.map()` is the clear choice. If you simply need to iterate over an array, `forEach` is a fine choice.

-------------------------------------------------------------------------
### 30. Can you explain what Function.call and Function.apply do? What's the notable difference between the two?

Both `.call` and `.apply` are used to invoke functions and the first parameter will be used as the value of `this` within the function. However, `.call` takes in comma-separated arguments as the next arguments while `.apply` takes in an array of arguments as the next argument. An easy way to remember this is C for `call` and comma-separated and A for `apply` and an array of arguments.

```javascript
function add(a, b) {
  return a + b;
}

console.log(add.call(null, 1, 2)); // 3
console.log(add.apply(null, [1, 2])); // 3
```
-------------------------------------------------------------------------
### 31. Explain Function.prototype.bind.

Taken word-for-word from [MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind):

> The `bind()` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

In my experience, it is most useful for binding the value of `this` in methods of classes that you want to pass into other functions. This is frequently done in React components.

> [Resource](https://www.codementor.io/@niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp) | [Medium](https://medium.com/@ivansifrim/the-differences-between-call-apply-bind-276724bb825b)

-------------------------------------------------------------------------
### 32. What is the definition of a higher-order function?

A higher-order function is any function that takes one or more functions as arguments, which it uses to operate on some data, and/or returns a function as a result. Higher-order functions are meant to abstract some operation that is performed repeatedly. The classic example of this is `map`, which takes an array and a function as arguments. `map` then uses this function to transform each item in the array, returning a new array with the transformed data. Other popular examples in JavaScript are `forEach`, `filter`, and `reduce`. A higher-order function doesn't just need to be manipulating arrays as there are many use cases for returning a function from another function. `Function.prototype.bind` is one such example in JavaScript.

**Map**

Let say we have an array of names which we need to transform each string to uppercase.

```javascript
const names = ['irish', 'daisy', 'anna'];
```

The imperative way will be as such:

```javascript
const transformNamesToUppercase = function(names) {
  const results = [];
  for (let i = 0; i < names.length; i++) {
    results.push(names[i].toUpperCase());
  }
  return results;
};
transformNamesToUppercase(names); // ['IRISH', 'DAISY', 'ANNA']
```

Use `.map(transformerFn)` makes the code shorter and more declarative.

```javascript
const transformNamesToUppercase = function(names) {
  return names.map(name => name.toUpperCase());
};
transformNamesToUppercase(names); // ['IRISH', 'DAISY', 'ANNA']
```
> Q.22

-------------------------------------------------------------------------
### 33. Can you give an example of a curry function and why this syntax offers an advantage?

Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument. 

```javascript
function volume(length) {
  return function(width) {
    return function(height) {
      return height * width * length;
    }
  }
}

volume(2)(3)(4); // 24
```

Curried functions are great to improve code re-usability and functional composition.

Currying is a pattern where a function with more than one parameter is broken into multiple functions that, when called in series, will accumulate all of the required parameters one at a time. This technique can be useful for making code written in a functional style easier to read and compose. It's important to note that for a function to be curried, it needs to start out as one function, then broken out into a sequence of functions that each accepts one parameter.

```javascript
function curry(fn) {
  if (fn.length === 0) {
    return fn;
  }

  function _curried(depth, args) {
    return function(newArgument) {
      if (depth - 1 === 0) {
        return fn(...args, newArgument);
      }
      return _curried(depth - 1, [...args, newArgument]);
    };
  }

  return _curried(fn.length, []);
}

function add(a, b) {
  return a + b;
}

var curriedAdd = curry(add);
var addFive = curriedAdd(5);

var result = [0, 1, 2, 3, 4, 5].map(addFive); // [5, 6, 7, 8, 9, 10]
```
> [Resource](https://javascript.info/currying-partials)

-------------------------------------------------------------------------
### 34. What is a unary function?

Unary function (i.e. monadic) is a function that accepts exactly one argument. Let us take an example of unary function. It stands for single argument accepted by a function.
```javascript
const unaryFunction = a => console.log (a + 10); //Add 10 to the given argument and display the value
```
-------------------------------------------------------------------------
### 35. What is a pure function?

Pure functions are functions that accept an input and returns a value without modifying any data outside its scope(Side Effects). Its output or return value must depend on the input/arguments and pure functions must return a value.

**Example**
```javascript
function impure(arg) {
    finalR.s = 90
    return arg * finalR.s
}
```
The above function is not a pure function because it modified a state `finalR.s` outside its scope.
```javascript
function pure(arg) {
    return arg * 4
}
```
Here is a pure function. It didn’t side effect any external state and it returns an output based on the input.

A function must pass two tests to be considered “pure”:

1. Same inputs always return same outputs
1. No side-effects 

**1. Same Input => Same Output**  
Compare this:
```javascript
const add = (x, y) => x + y;

add(2, 4); // 6
```
To this
```javascript
let x = 2;

const add = (y) => {
  x += y;
};

add(4); // x === 6 (the first time)
```
**2. Pure Functions = Consistent Results**  
The first example returns a value based on the given parameters, regardless of where/when you call it.

If you pass 2 and 4, you’ll always get 6.

Nothing else affects the output.

**Benefits**  
* One of the major benefits of using pure functions is they are immediately testable. They will always produce the same result if you pass in the same arguments.
* The pure functions are easier to parallelize
* They also makes maintaining and refactoring code much easier.

-------------------------------------------------------------------------
### 36. What is memoization?

Memoization is a programming technique which attempts to increase a function’s performance by caching its previously computed results.  Each time a memoized function is called, its parameters are used to index the cache. If the data is present, then it can be returned, without executing the entire function. Otherwise the function is executed and then the result is added to the cache.

```javascript
// A simple memoized function to Add Number
const memoizedAdd = () => {
  let cache = {};
  return (number) => {
    if (number in cache) {
      console.log('Fetching from cache: ');
      return cache[number];
    }
    else {
      console.log('Calculating result: ');
      let result = number + 10;
      cache[number] = result;   // cache.number = result;
      return result;
    }
  }
}
// returned function from memoizedAdd
const sum = memoizedAdd();
console.log(sum(10)); // Calculating result: 20
console.log(sum(10)); // Fetching from cache: 20
```

-------------------------------------------------------------------------
### 37. Explain event delegation.

-------------------------------------------------------------------------
### 38. What's the difference between host objects and native objects?

Native objects are objects that are part of the JavaScript language defined by the ECMAScript specification, such as `String`, `Math`, `RegExp`, `Object`, `Function`, etc.

Host objects are provided by the runtime environment (browser or Node), such as `window`, `XMLHTTPRequest`, etc.

-------------------------------------------------------------------------
### 39. Describe event bubbling.

Event bubbling is a type of event propagation where the event first triggers on the innermost target element, and then successively triggers on the ancestors (parents) of the target element in the same nesting hierarchy till it reaches the outermost DOM element.

Example: If you click on EM, the handler on DIV runs.  
```html
<div onclick="alert('The handler!')">
  <em>If you click on <code>EM</code>, the handler on <code>DIV</code> runs.</em>
</div>
```
* **Stopping bubbling**  
```html
<body onclick="alert(`the bubbling doesn't reach here`)">
  <button onclick="event.stopPropagation()">Click me</button>
</body>
```
-------------------------------------------------------------------------
### 40. Describe event capturing.

Event capturing is a type of event propagation where the event is first captured by the outermost element and then successively triggers on the descendants (children) of the target element in the same nesting hierarchy till it reaches the inner DOM element.

-------------------------------------------------------------------------
### 41. What is an event flow?

Event flow is the order in which event is received on the web page. When you click an element that is nested in various other elements, before your click actually reaches its destination, or target element, it must trigger the click event each of its parent elements first, starting at the top with the global window object.

There are two ways of event flow
* Top to Bottom(Event Capturing)
* Bottom to Top (Event Bubbling)
 
-------------------------------------------------------------------------
### 42. What is BOM?

The Browser Object Model (BOM) allows JavaScript to "talk to" the browser. It consists of the objects navigator, history, screen, location and document which are children of window. The Browser Object Model is not standardized and can change based on different browsers.

-------------------------------------------------------------------------
### 43. What is the use of stopPropagation method?

The stopPropagation method is used to stop the event from bubbling up the event chain. For example, the below nested divs with stopPropagation method prevents default event propagation when clicking on nested div(Div1)
```html
<p>Click DIV1 Element</p>
<div onclick="secondFunc()">DIV 2
  <div onclick="firstFunc(event)">DIV 1</div>
</div>

<script>
function firstFunc(event) {
  alert("DIV 1");
  event.stopPropagation();
}

function secondFunc() {
  alert("DIV 2");
}
</script>
```
-------------------------------------------------------------------------
### 44. What are the properties used to get size of window?

You can use innerWidth, innerHeight, clientWidth, clientHeight properties of windows, document element and document body objects to find the size of a window. Let's use them combination of these properties to calculate the size of a window or document,
```javascript
var width = window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;

var height = window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;
```
-------------------------------------------------------------------------
### 45. What are the DOM methods available for constraint validation?

-------------------------------------------------------------------------
### 46. How do you perform form validation using javascript?

-------------------------------------------------------------------------
### 47. How do you perform form validation without javascript?

-------------------------------------------------------------------------
### 48. What are the different methods to find HTML elements in DOM?

-------------------------------------------------------------------------
### 49. Explain the same-origin policy with regards to JavaScript.

The same-origin policy prevents JavaScript from making requests across domain boundaries. An origin is defined as a combination of URI scheme, hostname, and port number. This policy prevents a malicious script on one page from obtaining access to sensitive data on another web page through that page's Document Object Model.

-------------------------------------------------------------------------
### 50. What is the difference between document load and DOMContentLoaded events?

The `DOMContentLoaded` event is fired when the initial HTML document has been completely loaded and parsed, without waiting for assets(stylesheets, images, and subframes) to finish loading. Whereas The load event is fired when the whole page has loaded, including all dependent resources(stylesheets, images).

-------------------------------------------------------------------------
### 51. What is same-origin policy?

The same-origin policy is a policy that prevents JavaScript from making requests across domain boundaries. An origin is defined as a combination of URI scheme, hostname, and port number. If you enable this policy then it prevents a malicious script on one page from obtaining access to sensitive data on another web page using Document Object Model(DOM).

-------------------------------------------------------------------------
### 52. How do you make synchronous HTTP request?

Browsers provide an XMLHttpRequest object which can be used to make synchronous HTTP requests from JavaScript
```javascript
function httpGet(theUrl)
{
    var xmlHttpReq = new XMLHttpRequest();
    xmlHttpReq.open( "GET", theUrl, false ); // false for synchronous request
    xmlHttpReq.send( null );
    return xmlHttpReq.responseText;
}
```

-------------------------------------------------------------------------
### 53. How do you make asynchronous HTTP request?

Browsers provide an XMLHttpRequest object which can be used to make asynchronous HTTP requests from JavaScript by passing 3rd parameter as true.
```javascript
function httpGetAsync(theUrl, callback)
{
    var xmlHttpReq = new XMLHttpRequest();
    xmlHttpReq.onreadystatechange = function() {
        if (xmlHttpReq.readyState == 4 && xmlHttpReq.status == 200)
            callback(xmlHttpReq.responseText);
    }
    xmlHttp.open("GET", theUrl, true); // true for asynchronous
    xmlHttp.send(null);
}
```

-------------------------------------------------------------------------
### 54. What are the ways to execute javascript after page load?

You can execute javascript after page load in many different ways,  
**a.) window.onload:**
```javascript
window.onload = function ...
```
**b.) document.onload:**
```javascript
document.onload = function ...
```
**c.) body onload:**
```html
<body onload="script();">
```

-------------------------------------------------------------------------
### 55. What is an HTTP Header?

The HTTP headers are used to pass additional information between the clients and the server through the request and response header.
> [Geek](https://www.geeksforgeeks.org/http-headers/) | [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)

-------------------------------------------------------------------------
### 56. How can you prevent CORS issue?

> [Resource](https://www.pivotpointsecurity.com/blog/cross-origin-resource-sharing-security/) |
[Medium](https://medium.com/@dtkatz/3-ways-to-fix-the-cors-error-and-how-access-control-allow-origin-works-d97d55946d9)

-------------------------------------------------------------------------
### 57. When to use async and defer when loading JS files?

> [Resource](https://flaviocopes.com/javascript-async-defer/)

-------------------------------------------------------------------------
### 58. Describe how Fetch API makes use of Promises.

> [Medium](https://medium.com/@armando_amador/how-to-make-http-requests-using-fetch-api-and-promises-b0ca7370a444)

-------------------------------------------------------------------------
<!--
What are "web workers"?
What is HTML5 Web Storage? Explain localStorage and sessionStorage.
What's the difference between the <svg> and <canvas> elements?
What are custom attributes in HTML5?
What are the drawbacks of cookies?
What is purpose of watchPosition() method of geolocation object of HTML5?
How do you manipulate DOM using service worker?
What is a cookie?
How do you delete a cookie?
What is the main difference between localStorage and sessionStorage?
How do you check web storage browser support?
What is the difference between JavaScript and jQuery?
What is $() in jQuery library?
What are the effects methods used in jQuery?
What is the use of toggle() method in JQuery?
What is the use of html() method in JQuery?
What is the use of css() method in JQuery?
What is the starting point of code execution in jQuery?
What is the difference between find and children methods?
What are the selectors in jQuery? How many types of selectors are there in jQuery?
What is the use of serialize() method in JQuery?
What is the difference between jQuery.get() and jQuery.ajax()?
Explain the difference between the .detach() and .remove() methods in jQuery.
What's the difference between document.ready() and window.onload()?
What's the difference between prop() and attr()?
How do you rate limit requests to an ExpressJS route?
How do you structure an Express REST API application?
How to get GET (query string) variables in Express.js on Node.js?
How to retrieve POST query parameters?
How to get the full url in Express?
What will you do if an Express route throws Error: request entity too large?
How do you call a "local" function within module.exports from another function in module.exports?
How do you serve static files with Express?
What does body-parser module do with express?
What is the use of parameter next used in Express routes?
How to get remote client address in a route in Express?
What is a middleware? How can you create one in ExpressJS?
How to redirect 404 errors to a page in ExpressJS?
What are res and req parameters in Express route functions?
How to get hostname of current request in node.js Express?
What is process.env.PORT in ExpressJS?
NoSQL related questions
What are the features of NoSQL?
Explain the difference between NoSQL v/s Relational database?
When should I use a NoSQL database instead of a relational database?
How to do transactions/locking in MongoDB?
Compare MongoDB with Couchbase and CouchbaseDB.
Why is MongoDB not chosen for a 32-bit system?
What are the key features of MongoDB?
What is CRUD?
What is Aggregation in MongoDB?
What is the use of an Index in MongoDB?
Which command is used to create a database in MongoDB?
Which command is used to drop a database in MongoDB?
Which command is used to create a backup of the database?
What is a Collection in MongoDB?
Which method is used to update documents into a collection?
What is the role of profile in MongoDB?
RDBMS related questions
Why a database is called as relational database model?
What are constraints in database?
What is the difference between primary and foreign key?
What is an index represent in relational database model?
What do you understand by database Normalization?
What is the difference between primary key and unique constraints?
What are the differences between DDL, DML and DCL in SQL?
What is the difference between having and where clause?
What is Join?
What is a transaction? What are ACID properties?
List and explain the different types of JOIN clauses supported in ANSI-standard SQL.
Write a SQL query to find the 10th highest employee salary from an Employee table.
How can you select all the even number records from a table? Similarly, all the odd number records?
What is the difference between IN and EXISTS?
How do you copy data from one table to another table ?
How to start a Postgresql server in a Linux system?
Explain the use of aggregate functions in Postgresql?
What is a JOIN? What are the different JOIN operations supported by ANSI SQL?
ReactJS interview questions
Differentiate between Real DOM and Virtual DOM.
List some of the major advantages of React.
What are the limitations of React?
What is JSX?
Can you explain what is the concept of Virtual DOM?
Why can't browsers use JSX?
How different is React's ES6 syntax when compared to ES5?
How is React different from Angular?
"In React, everything is a component". What does this statement mean?
What is Props?
What is a state in React and how is it used?
Differentiate between states and props.
How can you update the state of a component?
What is arrow function in React? How is it used?
Differentiate between stateful and stateless components.
What are the different phases of React component's lifecycle?
Explain the lifecycle methods of React components in detail.
What are synthetic events in React?
What do you understand by refs in React?
What do you know about controlled and uncontrolled components?
What are Higher Order Components(HOC)?
What are Pure Components?
What is the significance of keys in React?
Why do we need a Router in React?
What happens when you call setState?
What's the difference between an Element and a Component in React?
When would you use a Class Component over a Functional Component?
What are refs in React and why are they important?
In which lifecycle method do you make AJAX requests with a Class component?
What are the most common approaches for styling a React application?
What are the advantages of using Redux than managing the state locally?
How is Redux different from Flux?
What is the significance of Store in Redux?
Explain the role of Reducer in Redux.
How are Actions defined in Redux?
Can you list down the components of Redux?
What do you understand by "Single source of truth" in the world of Redux?
What are the three principles that Redux follows?
What is the typical flow of data in a React + Redux app?
What is store in redux?
Explain Reducers in Redux?
Explain action's in Redux?
What are Pure Functions?
Can Redux only be used with React?
Big O Based
Why is O(n!) considered as one of the worst run time complexities for algorithms?
Which runtime does Bubble sort run?
Which runtime does Binary search run? Why?
Array Based
How to find the missing number in given integer array of 1 to 100?
How to find the largest and smallest number in an unsorted integer array?
How to find all pairs of integer array whose sum is equal to a given number?
How to find the duplicate number on a given integer array?
How to sort an integer array in place using QuickSort algorithm?
How to remove duplicates from an array in place?
How to reverse an array in place in Java?
How to find multiple missing numbers in given integer array with duplicates?
String Based
How to Print duplicate characters from String?
How to check if two Strings are anagrams of each other?
How to print first non repeated character from String?
How to reverse a given String using recursion?
How to check if a String contains only digits? Also, can you convert a string with only numbers to its equivalent number data type?
How to count a number of vowels and consonants in a given String?
How to find all permutations of String?
How to check if two String is a rotation of each other?
How to check if given String is Palindrome?
Linked List Based
How to find the middle element of a singly linked list in one pass?
How to reverse a linked list?
How to reverse a singly linked list without recursion?
How to remove duplicate nodes in an unsorted linked list?
How to find the length of a singly linked list?
How to find the 3rd node from the end in a singly linked list?
How do you find the sum of two linked list using Stack?
Tree Based
Can you write a program to implement a binary search tree?
How do you perform Pre-order traversal in a given binary tree?
Write a Program to traverse a given binary tree in Pre-order without recursion.
How to print all nodes of given binary tree using inorder traversal without recursion?
How to implement Post-order traversal algorithm?
How to traverse a binary tree in Post order traversal without recursion?
How to Print all leaves of a binary search tree?
How to count a number of leaf nodes in a given binary tree?
How to perform a binary search in a given array?
How can you find the depth of a graph?
-->


[Resource](https://github.com/learning-zone/javascript-interview-questions)
<!-- Day 1
Variable Declarations and Hoisting
Template Literals
Destructuring
Sets and Maps
Day 2
Functions
Javascript Classes
Closures
Day 3
Functional Programming in Javascript
Higher Order Functions
Recursion
Currying
Map, Reduce, Some, Sort Filter and Find
Chaining
Function methods - apply, bind and call
Day 4
DOM
DOM Selectors
DOM Tree
Creating the DOM elements
DOM Events
Scripting Forms
Scripting CSS using Javascript
Day 5
Ajax
Web page events
Cross-Origin Requests
HTTP
Web APIs (Mostly HTML5 APIs)
Other DOM/BOM related topics
Day 6
NodeJS
NPM
NodeJS Core Modules
NodeJS Streams
Event Emitter
Promises
Async/Await
JSON Web Tokens
NodeJS Debugging
NodeJS Memory Leaks
NodeJS and the CPU
Popular External Utilities
Day 7
ExpressJS
Middlewares
Templating Engines
Error Handlers
Database Integration
Common ExpressJS Libraries (Modules)
Day 8
Non Relational Databases & MongoDB
Relational Databases & SQL
Day 9
ReactJS Introduction
JSX, Components and Rendering
Component State and Life-cycle
Event Handling in Components
Interacting with AJAX APIs
React Router
Advanced React Concepts
Day 9 - Redux
Introduction
Actions
Reducers
Store
Using Redux with React
Using Redux with React Router
Async actions in Redux
Best Practices
Day 10 - DSA
Complexities
Searching Algorithms
Sorting Algorithms
Linked List
Stacks and Queues
Hash Tables
Heaps
Priority Queue
Trees
Graphs
Math based Algorithms
Day 11 - Computer Science Fundamentals
Number Representation in Computers
CPU Architecture
Operating Systems
Process Management
Networking) -->
