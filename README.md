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
