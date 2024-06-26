# Pursuit Style Guide

Pursuit JavaScript Style Guide

# Table of Contents
- [Pursuit Style Guide](#pursuit-style-guide)
- [Table of Contents](#table-of-contents)
	- [Types](#types)
		- [Primitive Data Types](#primitive-data-types)
		- [Non-Primitive Data Types](#non-primitive-data-types)
	- [Understanding Scope](#understanding-scope)
	- [Const Over Let](#const-over-let)
	- [Avoid Using Var](#avoid-using-var)
	- [Group all your consts and then group all your lets](#group-all-your-consts-and-then-group-all-your-lets)
	- [Assign variables when you need them](#assign-variables-when-you-need-them)
- [Comparison Operators \& Equality](#comparison-operators--equality)
	- [Proper Indentation and Spacing](#proper-indentation-and-spacing)
	- [Use of Semicolons](#use-of-semicolons)
- [Naming Conventions](#naming-conventions)
	- [Avoid single letter names](#avoid-single-letter-names)
	- [Use Descriptive Function and Variable Names](#use-descriptive-function-and-variable-names)
	- [Exporting](#exporting)
	- [Acronyms and Initialisms](#acronyms-and-initialisms)
	- [Functions Should Start With Verbs](#functions-should-start-with-verbs)
	- [Variables Should Start with Adjectives or Nouns](#variables-should-start-with-adjectives-or-nouns)
	- [Avoid Using Keywords in Variables and Function Names](#avoid-using-keywords-in-variables-and-function-names)
	- [When Using a Type in the Name use an Abbreviation](#when-using-a-type-in-the-name-use-an-abbreviation)
- [Double Loop](#double-loop)
- [Objects](#objects)
- [Arrays](#arrays)
	- [Destructuring](#destructuring)
- [Strings](#strings)
- [Functions](#functions)
	- [Arrow Functions](#arrow-functions)
	- [Classes \& Constructors](#classes--constructors)
- [Modules](#modules)
	- [Properties](#properties)
- [Comments](#comments)
	- [Prefixing your comments](#prefixing-your-comments)
- [Whitespace](#whitespace)
	- [No Trailing Whitespace](#no-trailing-whitespace)
- [Commas](#commas)
	- [Trailing commas](#trailing-commas)
- [Type Casting \& Coercion](#type-casting--coercion)
	- [Strings](#strings-1)
	- [Numbers](#numbers)
	- [Booleans](#booleans)
	- [Testing](#testing)
	- [Resources](#resources)

## Types

### Primitive Data Types
A primitive (primitive value, primitive data type) is data that is not an object and has no methods or properties.

All primitives are immutable; that is, they cannot be altered.

JavaScript has 7 primitive data types.

1. string
2. number
3. bigint
4. boolean
5. undefined
6. symbol
7. null

The `string` data type in JavaScript represents a sequence of characters that are surrounded by single or double quotes.

The `number` data type in javaScript can be used to hold decimal values as well as values without decimals.

`bigInt` data type can represent numbers greater than 2<sup>53</sup>-1 which helps to perform operations on large numbers. The number is specified by writing ‘n’ at the end of the value.

The `boolean` type represents a logical entity and can accept only two values: `true` and `false`.

`undefined` means that a variable has been declared but has not been assigned a value, or it has been explicitly set to the value `undefined`.

The `symbol` data type is used to create objects which will always be unique. these objects can be created using Symbol constructor.

The Null type is inhabited by exactly one value: `null`.

### Non-Primitive Data Types
1. An object
2. An array

An `object` in Javascript is an entity having properties and methods. Everything is an object in javascript.

An `array` can store more than one element under a single name.

> **Note:** JavaScript does not have a `function` data type. When we find the data type of a function using the typeof operator, we find that it returns a function. This is because a function is an object in JavaScript. Ideally the data type of a function should return an object but instead, it returns a function.
> ```js
>function pets() {
>    return "dog, cat, fish";
>}
>console.log(typeof pets) // 'function'
>```

## Understanding Scope
JavaScript has the following kinds of scopes:
* **Global scope**: The default scope for all code running in script mode.
* **Module scope**: The scope for code running in module mode.
* **Function scope**: The scope created with a function.

Variables declared with `let` or `const` can belong to an additional scope:
* **Block scope**: The scope created with a pair of curly braces (a block).

## Const Over Let
Variables in JavaScript are either `const` or `let`. 

Always use `const` or `let` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace.

It's good practice to use `const` over `let` whenever possible, as it makes your code more predictable and less prone to bugs.

If you must reassign references, use `let` instead of `var`.

Both `let` and `const` are block-scoped, whereas `var` is function-scoped.

```js
// block-scoped, can be reassigned
let countOfFellows = 20;
countOfFellows = 21; 	    

// block-scoped, cannot reassign
const animals = ["bear", "turtle", "quokka"];	

// function-scoped
var plants = ["cactus", "sunflower", "hydrangea"]; 
```

## Avoid Using Var
What is `var`, and why should we avoid using it?

The keywords `let` and `var` both declare new variables in JavaScript. The difference between `let` and `var`  is in the scope of the variables they create:

* Variables declared by `let` are only available inside the block where they’re defined.
* Variables declared by `var` are available throughout the function in which they’re declared.

Avoid using `var` because of function scope. Using `let` or `const` uses block scope, which is less error-prone.Additionally, ECMAScript6 (ES6 / JavaScript 2015) encourages you to declare variables with `let` not `var`.

## Group all your consts and then group all your lets
Group all your `const`s and then group all your `let`s. This is helpful when later on you might need to assign a variable depending on one of the previously assigned variables.
```js
// bad
let i, len, dragonball,
	items = getItems(),
	goSportsTeam = true;

// bad
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;
let len;

// good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;
```

## Assign variables when you need them
Assign variables where you need them, but place them in a reasonable place. This is because `let` and `const` are block scoped and not function scoped.
```js
// bad - unnecessary function call
function checkName(hasName) {
	const name = getName();

	if (hasName === "test") {
		return false;
	}

	if (name === "test") {
		this.setName("");
		return false;
	}

	return name;
}

// good
function checkName(hasName) {
	if (hasName === "test") {
		return false;
	}

	const name = getName();

	if (name === "test") {
		this.setName("");
		return false;
	}

	return name;
}
```

Don’t chain variable assignments. Chaining variable assignments creates implicit global variables.
```js
// bad
(function example() {
	// JavaScript interprets this as
	// let a = ( b = ( c = 1 ) );
	// The let keyword only applies to variable a; variables b and c become
	// global variables.
	let a = (b = c = 1);
})();

console.log(a); // throws ReferenceError
console.log(b); // 1
console.log(c); // 1

// good
(function example() {
	let a = 1;
	let b = a;
	let c = a;
})();

console.log(a); // throws ReferenceError
console.log(b); // throws ReferenceError
console.log(c); // throws ReferenceError

// the same applies for `const`
```
Avoid using unary increments and decrements (++, --). Per the eslint documentation, unary increment and decrement statements are subject to automatic semicolon insertion and can cause silent errors with incrementing or decrementing values within an application. It is also more expressive to mutate your values with statements like num += 1 instead of num++ or num ++. Disallowing unary increment and decrement statements also prevents you from pre-incrementing/pre-decrementing values unintentionally which can also cause unexpected behavior in your programs.
```js
// bad

const array = [1, 2, 3];
let num = 1;
num++;
--num;

let sum = 0;
let truthyCount = 0;
for (let i = 0; i < array.length; i++) {
	let value = array[i];
	sum += value;
	if (value) {
		truthyCount++;
	}
}

// good

const array = [1, 2, 3];
let num = 1;
num += 1;
num -= 1;

const sum = array.reduce((a, b) => a + b, 0);
const truthyCount = array.filter(Boolean).length;
```

Avoid linebreaks before or after = in an assignment. If your assignment violates max-len, surround the value in parens. 
```js
// bad
const foo =
	superLongLongLongLongLongLongLongLongFunctionName();

// bad
const foo
	 = 'superLongLongLongLongLongLongLongLongString';

// good
const foo = (
	superLongLongLongLongLongLongLongLongFunctionName()
);

// good
const foo = 'superLongLongLongLongLongLongLongLongString';
```

Disallow unused variables. Variables that are declared and not used anywhere in the code are most likely an error due to incomplete refactoring. Such variables take up space in the code and can lead to confusion by readers.

```js
// bad

const some_unused_var = 42;

// Write-only variables are not considered as used.
let y = 10;
y = 5;

// A read for a modification of itself is not considered as used.
let z = 0;
z = z + 1;

// Unused function arguments.
function getX(x, y) {
	return x;
}

// good

function getXPlusY(x, y) {
	return x + y;
}

const x = 1;
const y = a + 2;

alert(getXPlusY(x, y));

// 'type' is ignored even if unused because it has a rest property sibling.
// This is a form of extracting an object that omits the specified keys.
const { type, ...coords } = data;
// 'coords' is now the 'data' object without its 'type' property.
```

# Comparison Operators & Equality
Use `===` and `!==` over `==` and `!=`.

Conditional statements such as the if statement evaluate their expression using coercion with the ToBoolean abstract method and always follow these simple rules:

* Objects evaluate to true
* Undefined evaluates to false
* Null evaluates to false
* Booleans evaluate to the value of the boolean
* Numbers evaluate to false if +0, -0, or NaN, otherwise true
* Strings evaluate to false if an empty string '', otherwise true

```js
if ([0] && []) {
	// true
	// an array (even an empty one) is an object, objects will evaluate to true
}
```

Use shortcuts for booleans, but explicit comparisons for strings and numbers.
```js
// bad
if (isValid === true) {
	// ...
}

// good
if (isValid) {
	// ...
}

// bad
if (name) {
	// ...
}

// good
if (name !== "") {
	// ...
}

// bad
if (collection.length) {
	// ...
}

// good
if (collection.length > 0) {
	// ...
}
```

## Proper Indentation and Spacing

Proper indentation and spacing should be consistent throughout your code. Many developers choose to use 4-space or 2-space indentation. To be more readable, always use 4 spaces for indentation of code blocks.

JavaScript will not throw an error for improper indentation. As a developer, you need to make sure your code is readable.

```js
// bad
function properIndentation() {
const numbers = [1, 2, 3, 4];
let count = 0;
    
    for (const number of numbers){
    if (typeof number === "number"){
            count += 1;
  }
    }
return `I still need to indent my code ${count} spaces.`;
}

// good
function properIndentation() {
	const numbers = [1, 2, 3, 4];
	let count = 0;

	for (const number of numbers) {
		if (typeof number === "number") {
			count += 1;
		}
	}
	return `I have indented my code ${count} spaces.`;
}
```

Avoid spaces between functions and their invocations.
```js
// bad
func ();

func
();

// good
func();
```

## Use of Semicolons
Most JavaScript statements and declarations must end with a semicolon. While semicolons are not always required, it is good practice to include them to avoid unexpected behaviors.

How does JavaScript interpret line breaks?

For code without a semicolon, JavaScript uses a set of rules called `Automatic Semicolon Insertion`  to determine whether it should regard that line break as the end of a statement, and may place a semicolon into your code before the line break. You can also configure your linter to catch any missing semicolons.

```js
// good
let i = 0; i++    // <-- semicolon obligatory
        				// (but optional before newline)
let i = 0           // <-- semicolon optional
	i++               // <-- semicolon optional
```
An important quirk: inside the `()` of a for loop, semicolons only go after the first and second statement, never after the third:
*/

// ```js
// for (let i=0; i < 10; i++)  {/*actions*/}       // correct
// for (let i=0; i < 10; i++;) {/*actions*/}       // SyntaxError
// ```

# Naming Conventions
## Avoid single letter names
Avoid single letter names. Be descriptive with your naming.
```js
// bad
function q() {
	// ...
}

// good
function query() {
	// ...
}
```

Use camelCase when naming objects, functions, and instances.

## Use Descriptive Function and Variable Names
Use descriptive function and variable names whenever possible. Avoid single letter variable names. Variable names should be written using `camelCase`.

> What is `camel case`?

Use `camelCase` when naming objects, functions, and instances.
```js
// Camel case
const thisIsCamelCase = true;
```

> What is `pascal case`?
Use PascalCase only when naming constructors or classes.

```js
// Pascal case
class NumberOfDonuts {
	constructor(options) {
		this.count = options.count;
	}
}
const donuts = new NumberOfDonuts({
  count: 45,
});
```

```js
// Snake case
const this_is_snake_case = true;
```
```css
/* kebab case */
.home-page {
	background-color: red;
}
```

Do not use trailing or leading underscores.
```js
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';

// good
this.firstName = 'Panda';

// good, in environments where WeakMaps are available
// see https://compat-table.github.io/compat-table/es6/#test-WeakMap
const firstNames = new WeakMap();
firstNames.set(this, 'Panda');
```

## Exporting
Use camelCase when you export-default a function. Your filename should be identical to your function’s name.
```js
function makeStyleGuide() {
	// ...
}

export default makeStyleGuide;
```
Use PascalCase when you export a constructor / class / singleton / function library / bare object.
```js
const AirbnbStyleGuide = {
	es6: {
	},
};

export default AirbnbStyleGuide;
```

## Acronyms and Initialisms
Acronyms and initialisms should always be all uppercased, or all lowercased.
```js
// bad
import SmsContainer from "./containers/SmsContainer";

// bad
const HttpRequests = [
	// ...
];

// good
import SMSContainer from "./containers/SMSContainer";

// good
const HTTPRequests = [
	// ...
];

// also good
const httpRequests = [
	// ...
];

// best
import TextMessageContainer from "./containers/TextMessageContainer";

// best
const requests = [
	// ...
];
```


## Functions Should Start With Verbs
JavaScript function names should be in camel case and use descriptive nouns and verbs as prefixes. This makes it clear what the function does and what kind of value it returns.

What are verbs?

> verb • /vərb/
>
> **GRAMMAR**
>
> _noun_
> plural noun: **verbs**
>
> a word used to describe an action, state, or occurrence, and forming the main part of the predicate of a sentence, such as hear, become, happen.
> 
> Verbs are words that show an action (sing), occurrence (develop), or state of being (exist). Almost every sentence requires a verb. The basic form of a verb is known as its infinitive. The forms call, love, break, and go are all infinitives.

Examples:

```js
// bad
function cheerfulHero() {			// adjective: cheerful
	// ...
}
function goodDirectory() { 		// adjective: good
	// ...
}

// good
function createHero() {				// verb: create
	// ...
}
function makeStyleGuide() {	  // verb: make
	// ...
}
function insideDirectory() {	// noun: inside
	// ...
}
function fortyTwo() { 		 	 	  // noun: forty
	// ...
}
```

## Variables Should Start with Adjectives or Nouns
What are adjectives?
> ad·jec·tive • /ˈajəktiv/
>
> **GRAMMAR**
>
> _noun_
> plural noun: **adjectives**
>
> a word or phrase naming an attribute, added to or grammatically related to a noun to modify or describe it.

What are nouns?
> noun • /noun/
>
> **GRAMMAR**
>
> _noun_
> plural noun: **nouns**
> 
> a word (other than a pronoun) used to identify any of a class of people, places, or things (common noun), or to name a particular one of these (proper noun).
> 
> A noun is a word that refers to a thing (book), a person (Noah Webster), an animal (cat), a place (Omaha), a quality (softness), an idea (justice), or an action (yodeling). It's usually a single word, but not always: cake, shoes, school bus, and time and a half are all nouns.

Examples:
```js
// good nouns
const dog = "Clifford";		 // noun: dog
const schoolBus = "";		 // noun: school bus
const yodeling = true;		  // noun: yodeling
```

```js
// Bad
const kidsInTheClass = 20;
const lettersByValue = null;
let result = '';
const myFunc() {};
let solution = '';

//Good
const countKidsInTheClass = 0;
const sortLettersByValue = ['a', 'b', 'c'];
let numsBetween20And30 = [];

// Bad
const findAllNumsAboveTen = [];
const checkForDog = 'Clifford';

// Good
const allNumsAboveTen = [12, 45, 76];
const redDog = 'Clifford';
```

## Avoid Using Keywords in Variables and Function Names

What are keywords?
Keywords are reserved words that are part of the syntax in the programming language.
Keywords cannot be used to name identifiers.

List of Keywords in JavaScript:
```md
await • break • case • catch • class • const • continue • debugger • default • delete • do • else • enum • export • extends • false • finally • for • function • if • implements • import • in • instanceof • interface • let • new • null • package • private • protected • public • return • super • switch • static • this • throw • try • true • typeof • var • void • while • with • yield	 
```

Examples: 

```js
// Bad
const returnAllNumsAboveTen = () => ...
let newBus = 'red bus';

// Good
const getAllNumsAboutTen;
let bus = 'yellow bus';
```

## When Using a Type in the Name use an Abbreviation
What are the abbreviations for [types](#types)?
In JavaScript there are 5 different data types that can contain values:

Examples
| type     | abbreviation |
|----------|--------------|
| string   | str          |
| number   | num          |
| array    | arr          |
| object   | obj          |
| function | func         |

```js
// Bad
const childrenArray = [];
let lettersString = "";
let scoresObject = {};

// Good
const childrenArr = [];
let lettersStr = "";
let scoresObj = {};
```

# Double Loop
Inside a `for loop`, there can be another loop nested inside it.

Declaring variables inside a double loop will make it more readable. For example, inside the outer loop you can declare a variable called `const word = words[i]`. Then in the inner loop, you can iterate over `word` instead of `words[i]`.

```js
const words = ["red", "popeye", "spinach"];

// double loop
// BAD
for (let i = 0; i < words.length; i++) {
	for (let j = 0; j < words[i].length; j++) {
		console.log(words[i][j]);
	}
}

// BETTER
for (let i = 0; i < words.length; i++) {
	const word = words[i];

	for (let j = 0; j < word.length; j++) {
		const letter = word[j];

		console.log(letter);
	}
}
```

**Even better**

Variables such as `words[i]` and `words[i][j]` can become unreadable.

Both `for...in` and `for...of` statements iterate over something. The main difference between them is in what they iterate over.

```js
// EVEN BETTER
for (const word of words) {
	const letters = word.split("");
	for (const letter of letters) {
		console.log(letter);
	}
}

for (const word in words) {
	for (const idx in word) {
		const letter = word[idx];
		if (idx % 2 === 0) {
			console.log(letter);
		}
	}
}

// PRETTY GOOD :)
words.forEach((word) => {
	word.split("").forEach((letter, idx) => {
		if (idx % 2 === 0) {
			console.log(letter);
		}
	});
});
```

# Objects
Use the literal syntax for object creation.
```js
// bad
const students = new Object();

// good
const students = {};
```

# Arrays
Use the literal syntax for array creation.
```js
// bad
const nums = new Array();

// good
const nums = [];
```

## Destructuring
What is destructuring?
Destructuring is a JavaScript expression that allows us to extract data from arrays, objects, and maps and set them into new, distinct variables. Destructuring allows us to extract multiple properties, or items, from an array​ at a time.

Use object destructuring when accessing and using multiple properties of an object.

```js
// bad
function getFullName(user) {
	const firstName = user.firstName;
	const lastName = user.lastName;

	return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
	const { firstName, lastName } = user;
	return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
	return `${firstName} ${lastName}`;
}
```

Use array destructuring.

```js
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

Use object destructuring for multiple return values, not array destructuring.
```js
// good
function processInput(input) {
	// then a miracle occurs
	return { left, right, top, bottom };
}

// the caller selects only the data they need
const { left, top } = processInput(input);
```

# Strings
Use single quotes `''` for strings.
```js
// bad
const name = "Capt. Jack Sparrow";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Jack Sparrow`;

// good
const name = 'Capt. Jack Sparrow';
```

Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.
```js
// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// bad
const errorMessage = 'This is a super long error that was thrown because ' +
'of Batman. When you stop to think about how Batman had anything to do ' +
'with this, you would get nowhere fast.';

// good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

When programmatically building up strings, use template strings instead of concatenation.
```js
// bad
function sayHi(name) {
	return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
	return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
	return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
	return `How are you, ${name}?`;
}
```
Do not unnecessarily escape characters in strings. 
```js
// bad
const foo = '\'this\' \i\s \"quoted\"';

// good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

Never use `eval()` on a string; it opens too many vulnerabilities and is an enormous security risk.

# Functions
Use named function expressions instead of function declarations.
```js
// bad
function foo() {
	// ...
}

// bad
const foo = function () {
	// ...
};

// good
// lexical name distinguished from the variable-referenced invocation(s)
const short = function longUniqueMoreDescriptiveLexicalFoo() {
	// ...
};
```

## Arrow Functions
When you must use an anonymous function (as when passing an inline callback), use arrow function notation.
```js
// bad
[1, 2, 3].map(function (x) {
	const y = x + 1;
	return x * y;
});

// good
[1, 2, 3].map((x) => {
	const y = x + 1;
	return x * y;
});
```

## Classes & Constructors
Always use `class`. Avoid manipulating `prototype` directly.

```js
// bad
function Queue(contents = []) {
	this.queue = [...contents];
}
Queue.prototype.pop = function () {
	const value = this.queue[0];
	this.queue.splice(0, 1);
	return value;
};

// good
class Queue {
	constructor(contents = []) {
    	this.queue = [...contents];
	}
  	pop() {
		const value = this.queue[0];
		this.queue.splice(0, 1);
		return value;
	}
}
```

Use `extends` for inheritance.

```js
// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
	Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
	return this.queue[0];
};

// good
class PeekableQueue extends Queue {
	peek() {
		return this.queue[0];
	}
}
```

Methods can return `this` to help with method chaining.

```js
// bad
Jedi.prototype.jump = function () {
	this.jumping = true;
	return true;
};

Jedi.prototype.setHeight = function (height) {
	this.height = height;
};

const luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
class Jedi {
	jump() {
		this.jumping = true;
		return this;
	}

	setHeight(height) {
		this.height = height;
		return this;
	}
}

const luke = new Jedi();

luke.jump().setHeight(20);
```

It’s okay to write a custom `toString()` method, just make sure it works successfully and causes no side effects.
```js
class Jedi {
	constructor(options = {}) {
		this.name = options.name || "no name";
	}

	getName() {
		return this.name;
	}

	toString() {
		return `Jedi - ${this.getName()}`;
	}
}

```

Classes have a default constructor if one is not specified. An empty constructor function or one that just delegates to a parent class is unnecessary. 
```js
// bad
class Jedi {
	constructor() {}

	getName() {
		return this.name;
	}
}

// bad
class Rey extends Jedi {
	constructor(...args) {
		super(...args);
	}
}

// good
class Rey extends Jedi {
	constructor(...args) {
		super(...args);
		this.name = "Rey";
	}
}

```

Avoid duplicate class members. Duplicate class member declarations will silently prefer the last one - having duplicates is almost certainly a bug.
```js
// bad
class Foo {
	bar() {
		return 1;
	}
	bar() {
		return 2;
	}
}

// good
class Foo {
	bar() {
		return 1;
	}
}

// good
class Foo {
	bar() {
		return 2;
	}
}
```

Class methods should use `this` or be made into a static method unless an external library or framework requires using specific non-static methods. Being an instance method should indicate that it behaves differently based on properties of the receiver

```js
// bad
class Foo {
	bar() {
		console.log("bar");
	}
}

// good - this is used
class Foo {
	bar() {
		console.log(this.bar);
	}
}

// good - constructor is exempt
class Foo {
	constructor() {
		// ...
	}
}

// good - static methods aren't expected to use this
class Foo {
	static bar() {
		console.log("bar");
	}
}
```

# Modules
Always use modules (import/export) over a non-standard module system. You can always transpile to your preferred module system.
Modules are the future, let’s start using the future now.
```js
// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
module.exports = AirbnbStyleGuide.es6;

// ok
import AirbnbStyleGuide from './AirbnbStyleGuide';
export default AirbnbStyleGuide.es6;

// best
import { es6 } from './AirbnbStyleGuide';
export default es6;
```

Do not use wildcard imports. This makes sure you have a single default export.
```js
// bad
import * as AirbnbStyleGuide from './AirbnbStyleGuide';

// good
import AirbnbStyleGuide from './AirbnbStyleGuide';
```

And do not export directly from an import. Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.
```js
// bad
// filename es6.js
export { es6 as default } from './AirbnbStyleGuide';

// good
// filename es6.js
import { es6 } from './AirbnbStyleGuide';
export default es6;
```

Only import from a path in one place.
```js
// bad
import foo from 'foo';
// … some other imports … //
import { named1, named2 } from 'foo';

// good
import foo, { named1, named2 } from 'foo';

// good
import foo, {
    named1,
    named2,
} from 'foo';
```

Do not export mutable bindings.
```js
// bad
let foo = 3;
export { foo };

// good
const foo = 3;
export { foo };
```

In modules with a single export, prefer default export over named export.
```js
// bad
export function foo() {}

// good
export default function foo() {}
```

Put all imports above non-import statements.
```js
// bad
import foo from 'foo';
foo.init();

import bar from 'bar';

// good
import foo from 'foo';
import bar from 'bar';

foo.init();
```

Multiline imports should be indented just like multiline array and object literals.
```js
// bad
import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

// good
import {
    longNameA,
    longNameB,
    longNameC,
    longNameD,
    longNameE,
} from 'path';
```

Disallow Webpack loader syntax in module import statements.
```js
// bad
import fooSass from 'css!sass!foo.scss';
import barCss from 'style!css!bar.css';

// good
import fooSass from 'foo.scss';
import barCss from 'bar.css';
```

Do not include JavaScript filename extensions.
```js
// bad
import foo from './foo.js';
import bar from './bar.jsx';
import baz from './baz/index.jsx';

// good
import foo from './foo';
import bar from './bar';
import baz from './baz';
```

## Properties
Use dot notation when accessing properties.
```js
const luke = {
	jedi: true,
	age: 28,
};

// bad
const isJedi = luke['jedi'];

// good
const isJedi = luke.jedi;
```

Use bracket notation [] when accessing properties with a variable.
```js
const luke = {
	jedi: true,
	age: 28,
};

function getProp(prop) {
	return luke[prop];
}

const isJedi = getProp('jedi');
```

Use exponentiation operator `**` when calculating exponentiations.
```js
// bad
const binary = Math.pow(2, 10);

// good
const binary = 2 ** 10;
```


# Comments
Use `/** ... */` for multiline comments.

Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it’s on the first line of a block.

Start all comments with a space to make it easier to read. 

## Prefixing your comments
Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you’re pointing out a problem that needs to be revisited, or if you’re suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME: -- need to figure this out` or `TODO: -- need to implement`.

Use `// FIXME:` to annotate problems.
Use `// TODO:` to annotate solutions to problems.

# Whitespace
Whitespace refers to characters which are used to provide horizontal or vertical space between other characters. Whitespace is often used to separate tokens in HTML, CSS, JavaScript, and other computer languages.

## No Trailing Whitespace
Be sure to clean up any trailing whitespace in your JS files.

# Commas
Avoid leading commas.
```js
// ARRAYS
// bad
const story = [
    once
    , upon
    , aTime
];

// good
const story = [
    once,
    upon,
    aTime,
];

// OBJECTS
// bad
const hero = {
    firstName: 'Ada'
    , lastName: 'Lovelace'
    , birthYear: 1815
    , superPower: 'computers'
};

// good
const hero = {
    firstName: 'Ada',
    lastName: 'Lovelace',
    birthYear: 1815,
    superPower: 'computers',
};
```

## Trailing commas
JavaScript has allowed trailing commas in array literals since the beginning.

JavaScript allows trailing commas wherever a comma-separated list of values is accepted and more values may be expected after the last item.

Trailing commas are also allowed in:
* array literals
* object literals
* parameter definitions
* function calls
* named imports
* named exports
* array and object destructuring

In all these cases, the trailing comma is entirely optional and doesn't change the program's semantics in any way.

`JSON`, however, disallows all trailing commas.

```js
// OBJECTS
// bad
const hero = {
    firstName: 'Dana',
    lastName: 'Scully'
};

// good
const hero = {
    firstName: 'Dana',
    lastName: 'Scully',
};

// ARRAYS
// bad
const heroes = [
    'Batman',
    'Superman'
];

// good
const heroes = [
    'Batman',
    'Superman',
];

// FUNCTIONS
// bad
function createHero(
    firstName,
    lastName,
    inventorOf
) {
    // does nothing
}

// good
function createHero(
    firstName,
    lastName,
    inventorOf,
) {
    // does nothing
}

// FUNCTION WITH REST ELEMENT
// good (note that a comma must not appear after a "rest" element)
function createHero(
    firstName,
    lastName,
    inventorOf,
    ...heroArgs
) {
    // does nothing
}

// FUNCTION CALLS
// bad
createHero(
    firstName,
    lastName,
    inventorOf
);

// good
createHero(
    firstName,
    lastName,
    inventorOf,
);

// good (note that a comma must not appear after a "rest" element)
createHero(
    firstName,
    lastName,
    inventorOf,
    ...heroArgs
);
```

# Type Casting & Coercion
Perform type coercion at the beginning of the statement.

## Strings
Disallow `new` operators with the `String`, `Number`, and `Boolean` objects.
```js
// => this.reviewScore = 9;

// bad
const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

// bad
const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

// bad
const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string

// good
const totalScore = String(this.reviewScore);
```

## Numbers
Use `Number` for type casting and parseInt always with a radix for parsing strings.
```js
const inputValue = '4';

// bad
const val = new Number(inputValue);

// bad
const val = +inputValue;

// bad
const val = inputValue >> 0;

// bad
const val = parseInt(inputValue);

// good
const val = Number(inputValue);

// good
const val = parseInt(inputValue, 10);
```

## Booleans
Disallow `new` operators with `Boolean` objects.

```js
const age = 0;

// bad
const hasAge = new Boolean(age);

// good
const hasAge = Boolean(age);

// best
const hasAge = !!age;
```

## Testing
Whichever testing framework you use, you should be writing tests!

## Resources
[Resources](https://github.com/airbnb/javascript?tab=readme-ov-file#resources)