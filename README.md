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
	- [Proper Indentation and Spacing](#proper-indentation-and-spacing)
	- [Use of Semicolons](#use-of-semicolons)
- [Naming Conventions](#naming-conventions)
	- [Use Descriptive Function and Variable Names](#use-descriptive-function-and-variable-names)
	- [Functions Should Start With Verbs](#functions-should-start-with-verbs)
	- [Variables Should Start with Adjectives or Nouns](#variables-should-start-with-adjectives-or-nouns)
	- [Avoid Using Keywords in Variables and Function Names](#avoid-using-keywords-in-variables-and-function-names)
	- [When Using a Type in the Name use an Abbreviation](#when-using-a-type-in-the-name-use-an-abbreviation)
	- [Double Loop](#double-loop)

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

## Understanding Scope
JavaScript has the following kinds of scopes:
* **Global scope**: The default scope for all code running in script mode.
* **Module scope**: The scope for code running in module mode.
* **Function scope**: The scope created with a function.

Variables declared with `let` or `const` can belong to an additional scope:
* **Block scope**: The scope created with a pair of curly braces (a block).

## Const Over Let
Variables in JavaScript are either `const` or `let`. 

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

## Proper Indentation and Spacing

Proper indentation and spacing should be consistent throughout your code. Many developers choose to use 4-space or 2-space indentation. To be more readable, always use 4 spaces for indentation of code blocks.

JavaScript will not throw an error for improper indentation. As a developer, you need to make sure your code is readable.

```js
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
```

Avoid spaces between functions and their invocations.
```js
// good
func();

// bad
func ();

func
();
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
## Use Descriptive Function and Variable Names

Use descriptive function and variable names whenever possible. Avoid single letter variable names. Variable names should be written using `camelCase`.

> What is `camel case`, `pascal case`, `snake case`, and `kebab case`?

Use `camelCase` when naming objects, functions, and instances.
```js
// Camel case
const thisIsCamelCase = true;
```

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

Descriptive function and variable names:

```js
// good
function query() {
	// ...
}

const id = 2;
const greeting = "hello world";


// bad
function q() {
	// ...
}

const x = 2;
const y = "hello world";
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

// bad
function cheerfulHero() {			// adjective: cheerful
	// ...
}
function goodDirectory() { 		// adjective: good
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
// good adjectives

// bad adjectives

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

## Double Loop
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
