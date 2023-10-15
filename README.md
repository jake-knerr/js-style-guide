# JavaScript Style Guide <!-- omit in toc -->

Welcome to my JavaScript Style Guide. This guide aims to be a comprehensive description of my standards for JavaScript source code.

Although this guide is called a style guide, it focuses on more than simply aesthetic issues like formatting. It also provides design guidance — styling with a purpose.

---

## Copyright <!-- omit in toc -->

Jake Knerr © Ardisia Labs LLC

---

## Table of Contents <a id="toc" name="toc"></a> <!-- omit in toc -->

- [Code Analyzers](#code-analyzers)
  - [Prettier](#prettier)
  - [ESLint](#eslint)
- [Transpilers](#transpilers)
- [File Basics](#file-basics)
  - [Character Encoding](#character-encoding)
  - [Filenames](#filenames)
- [Naming](#naming)
  - [General Naming](#general-naming)
  - [Identifiers](#identifiers)
  - [Naming Data](#naming-data)
  - [Naming Functions](#naming-functions)
  - [Naming Files](#naming-files)
  - [Naming Folders](#naming-folders)
- [Storybook Design, Code Order](#storybook-design-code-order)
- [Code as Documentation](#code-as-documentation)
- [JavaScript Features](#javascript-features)
  - [Whitespace](#whitespace)
  - [Control Statements and Structures](#control-statements-and-structures)
  - [Exceptions](#exceptions)
  - [Operators](#operators)
  - [Primitive Types and Built-Ins](#primitive-types-and-built-ins)
  - [Strings](#strings)
  - [Variables](#variables)
  - [Enums](#enums)
  - [Objects](#objects)
  - [Object Concepts](#object-concepts)
  - [Arrays](#arrays)
  - [Events](#events)
  - [Functions](#functions)
  - [Function Concepts](#function-concepts)
  - [Arrow Functions](#arrow-functions)
  - [Generator Functions](#generator-functions)
  - [Classes, Constructor Functions](#classes-constructor-functions)
  - [Object Factories, Class, Constructor Functions, Prototypes](#object-factories-class-constructor-functions-prototypes)
  - [Modules](#modules)
  - [Module Imports](#module-imports)
  - [Module Exports](#module-exports)
  - [CJS Modules](#cjs-modules)
  - [Module Concepts](#module-concepts)
  - [Restricted JavaScript Features](#restricted-javascript-features)
- [Application Architecture](#application-architecture)
  - [General](#general)
  - [Client-Side](#client-side)
  - [Node](#node)
- [Minification](#minification)
- [Comments and Documentation](#comments-and-documentation)
  - [Commenting Overview](#commenting-overview)
  - [Implementation Comments](#implementation-comments)
  - [Documentation Comments, JSDoc](#documentation-comments-jsdoc)
  - [Documentation Concepts](#documentation-concepts)
- [Globalization](#globalization)
- [Programming Paradigms](#programming-paradigms)
- [Abstraction Concepts](#abstraction-concepts)
- [Resources](#resources)
- [Epilogue](#epilogue)

## Code Analyzers

### Prettier

#### Use Prettier.

This guide does not restate formatting rules that Prettier already enforces.

> Why Prettier? The Prettier website puts it best: "By far the biggest reason for adopting Prettier is to stop all the on-going debates over styles. It is generally accepted that having a common style guide is valuable for a project and team but getting there is a very painful and unrewarding process. People get very emotional around particular ways of writing code and nobody likes spending time writing and receiving nits.<br><br>So why choose the 'Prettier style guide' over any other random style guide? Because Prettier is the only 'style guide' that is fully automatic. Even if Prettier does not format all code 100% the way you'd like, it's worth the "sacrifice" given the unique benefits of Prettier, don't you think?"

#### Use Prettier's default configuration.

> Why? The default configuration is reasonable and the easiest to set up.

### ESLint

#### (Optional) Consider using ESLint to catch code quality warnings and errors. Leave formatting to Prettier.

ESLint can help enforce conventions and consistency. However, if you do decide to use ESLint, don't let it boss you around because sometimes otherwise good conventions should be violated.

> Why ESLint? ESLint is a very mature and extensive Javascript linter.

#### This guide will not explicitly reference linter rules.

> Why? Allowing style/design conventions to vary independently of the linter prevents changes to the linter forcing changes to the style guide. Not referencing linter rules also promotes rules that require independent thinking and not merely copying/pasting linter rules. This guide is the source of truth, not the linter configuration file. Finally, many linter rules do not bear repeating because they are catching bugs.

**[⬆ Table of Contents](#toc)**

---

## Transpilers

#### Prefer configuring transpilers via configuration files instead of adding directives to the source code.

For example, use a `webpack.config.js` file instead of using custom import syntax in the source.

> Why? Avoid coupling source code to a particular transpiler's syntax; otherwise, changes to the transpiler will trigger changes to the source code.

```javascript
// discouraged
import styles from "style-loader!css-loader?modules!./styles.css";

// preferred
import styles from "styles.css";
```

**[⬆ Table of Contents](#toc)**

---

## File Basics

### Character Encoding

#### Use UTF-8 for source files.

> Why? Because it is compatible with ASCII, compact, and fully supports Unicode.

#### Use 7-bit ASCII for identifiers.

> Why? ASCII provides the broadest support and uses the same character set (Latin) that JavaScript uses for keywords.

```javascript
// avoid
let é = 10;

// good
let e = 10;
```

#### Prefer Unicode characters over escape characters.

If a Unicode escape is required, leave a comment describing the character.

> Why? The actual character is much clearer than the escape sequence.

```javascript
// discouraged
const euroSymbol = "\u20AC";

// preferred
const euroSymbol = "€";
```

#### Avoid the byte order mark (BOM).

> Why? The BOM typically does not cause any problems, but it can trigger unexpected issues on older browsers or when parsing string content. Also, the Unicode standard does not recommend using it, "Use of a BOM is neither required nor recommended for UTF-8 ..." Unicode Version 5.0 http://www.unicode.org/versions/Unicode5.0.0/ch02.pdf

**[⬆ Table of Contents](#toc)**

---

### Filenames

#### File extensions are .js.

> Why? .js is the standard convention.

**[⬆ Table of Contents](#toc)**

---

## Naming

### General Naming

#### Naming is hard and very important.

> Why? Imagine reading a novel and being unclear on who many of the characters are. This is the experience of reading code with unclear identifiers for variables, functions, object properties, and everything else. One of the reasons naming is hard is because identifiers' names are purposely concise; thus, regardless of how complex an idea is, it needs to be reflected in a short name.

#### Prefer names that are as short as possible but as long as necessary. Aim for intuitive names that are also descriptive.

Clarity is king when creating names.

> Remember that readers may not be fluent in English. Do not show off your dictionary/thesaurus skills.

> What is an intuitive name? It is a name that other developers will recognize and know its meaning.

> What is a descriptive name? It is a name that provides adequate detail.

```javascript
// discouraged - not intuitive
const Bn;
const pulchritudinousPerson;

// preferred
const Button;
const prettyPerson;

// discouraged - not descriptive
const asset;
const data;

// preferred
const icon;
const personData;
```

#### The default word-separation style for JavaScript identifiers is lowerCamelCase.

Exceptions are clearly stated in this guide.

> Why? lowerCamelCase is the standard convention.

```javascript
// lowerCamelCase
const getColor;
const fooBar;
```

#### Abbreviations, initialisms, and acronyms are acceptable as long as they are familiar to other developers.

```javascript
// acceptable - nearly everyone knows these abbreviations
const usa;
const nasa;
```

#### Habitually making all abbreviations (acronyms and initialisms) uppercase is discouraged. Instead, prefer to apply the same naming techniques to abbreviations that are applied to normal words.

> Why? To be consistent with this guide's naming rules. For example, uppercase has a specific meaning in this guide and contravening this meaning because the name is an abbreviation is confusing.

The only exception is if the abbreviation appears after a word in a compound name, then capitalizing the abbreviation is allowed. E.G. `userID, spaceAgencyNASA` are acceptable.

```javascript
// discouraged
const FBI = {};
const HTTPGet = {};
class NASA {}
const userID = 10;

// preferred
const fbi = {}; // lowercase names for objects
const httpGet = {}; // lowercamelcase for compound names
class Nasa {} // uppercamelcase for constructor functions
const userId = 10; // lowercamelcase

// acceptable
const federalAgencyFBI; // compound name; uppercase abbreviation acceptable
```

#### Prefer positive names.

Use `userOnline` instead of `userOffline`.

> Why? For negative names, signaling `true` requires a double negative: `!userOffline`, which is confusing.

```javascript
// discouraged
let loginFail;

// preferred
let loginSuccess;
```

#### Do not use the terms "model", "view", or "controller" in the names of files, folders, variables, function, or anything else.

Names should be more specific than broad architectural abstractions.

This doesn't mean that one should not use these terms in your code. It means that you should not use these terms in your names.

> Why? These terms are too generic and usually lead to confusion and poor organization.

### Identifiers

#### Identifiers (names) in JavaScript refer to data or functions that act on data.

```javascript
const articles = {
  users: [],
};
class Foo {}
function bar() {}
```

#### Identifiers' referenced data has many different _contexts_.

> What is a context? A context is a category of ideas, problems, or activities that the data could be useful within. Data has many different contexts.

> Example: assume we have data that is a brand of running shoes. The possible values for the data are "nike" | "adidas" | "converse". The number of contexts for this data is infinite: sports, shoes, basketball, winning, losing, football, rubber, stitching, running, performance, brands, shoe companies, etc.

> Example 2: assume we have data that is the value of π. The number of contexts for this data is infinite: math, geometry, artillery, homework, long, memorization, etc.

#### Some contexts are more specific than other contexts.

> What is a more specific context? A sub-context within a broader context. In other words, a context that is a subset of another context.

> Taking the example above using shoe brands, the context of "basketball" is more specific than "sports" because all of the ideas, problems and activities of basketball are also contained within the context of "sports".

Programming Example - the constant `PI` has the context of class `Foo` and the context of method `bar`. The `bar` context is more specific than the `Foo` context because `bar` is contained within `Foo`. Restated, the context of `Foo` contains the context of `bar`, which makes `bar` a sub-context and more specific than `Foo`.

```javascript
// context
class Foo {
  // context
  bar() {
    // data
    const PI = 3.14159;
  }
}
```

#### Some contexts are more relevant than others.

> What is a more relevant context? A relevant context for data is the context that the data is currently useful for. Imagine GPS coordinate data. GPS data has the contexts of dropping bombs and locating endangered baby seals. However, both of these contexts would never be relevant at the same time (I would hope).

**[⬆ Table of Contents](#toc)**

---

### Naming Data

#### When creating a name for a data identifier, consider the relevant contexts for the referenced data. Next, consider the relevant contexts in the order of their specificity. Next, prefer to create a name by listing these contexts from left to right in descending order of specificity.

Contexts are nounal because they are _things_.

#### Avoid including irrelevant contexts in the name.

If you have more than two contexts in the name, consider if the remaining contexts are necessary.

#### Do not include a context in a name that is implicit from the surrounding code.

In other words, the context that surrounds a name can be viewed as part of the name; thus, repeating it is unnecessary.

> Note, even the file system can provide implicit context.

```javascript
// avoid
function createUserProfile() {
  const userProfileId = 10;
}

// good - user profile context is clear - unnecessary
function createUserProfile() {
  const id = 10;
}
```

#### Add prepositions, helping and linking verbs, or adjectives to contexts to provide additional information about a context or how multiple contexts relate to one another.

Common examples are "min", "max", "prev", "next", "had", "will", "is", "does", etc.

```javascript
// allowed - "in" is a preposition relating address and database
const addressInDatabase;

// allowed - "primary" is an adjective for user
const primaryUser;

// allowed - "has" is a helping verb relating salad and ranch
const saladHasRanch;
```

**[⬆ Table of Contents](#toc)**

---

### Naming Functions

#### When naming non-constructor functions, first consider the data that the function acts on. Next, follow the same naming instructions for data identifiers explained above. Next, add an action verb as a prefix to the name. The action verb should describe the function's operation on the data.

This is the only place in identifier names that an action verb appears.

Common examples are: "get", "set", "fetch", "remove", "add", "delete", "handle", etc.

> Why an action verb? Functions are actions and behavior, just like verbs.

```javascript
// discouraged
const isTrue = () => {}; // "is" is not an action verb

// preferred
function getColor() {}
const obj = {
  calcTip() {},
};
const createCar = function () {};
function testUserData() {}
```

#### Prefer to name constructor functions like data. They are nounal and do not start with a verb.

> Why? Constructor functions create data (objects).

```javascript
// discouraged
class foo {}

// preferred
class Foo {}
```

#### Names for methods of an object typically have shorter names than standalone named functions because methods have the object name as context.

Standalone named functions do not get the implicit context from the object name.

On the plus side, standalone named functions are easily minified.

```javascript
export class Car {
  // drive inherits the context of Car
  drive() {}
}

// standalone function name is longer because it lacks the context provided
// by the class name
export function driveCar() {}
```

#### Exported functions are named like standalone functions.

> Why? Exported functions are standalone functions. An argument could be made that an exported function name should carry the context of the module it is exported from. However, this is not necessary because the module path is already provided by the import statement.

```javascript
// avoid
function handleCar() {}

export const handleCarInMyModule = handleCar;

// good
export function handleCar() {}
```

### Naming Files

#### Filenames are nounal.

> Why? Files are nouns, not verbs.

#### Filenames only use lowercase letters and numbers. The first character of a filename is a letter. Use train-case to separate words.

Use descriptive names.

> Why no underscores? Underlined filenames and links can obscure the underscore, making it easy to miss.

```
/* avoid */
pageA.js;
UTILITIES_COLOR.js;
defaultClass.js;
page_b.js;

/* good */
template-page-a.js;
utils-color.js;
class-default.js;
template-page-b.js;
```

#### Strongly prefer named files over _index.\*_ files.

The only exception is `index.html` due to how web servers handle such files.

> Why? It is easier to track named files in an IDE, and named files are more descriptive than _index_. It is easy to get confused with a sea of `index` files in your IDE tabs.

```
/* discouraged */
/utils/math/index.js

/* preferred */
utils/math/math-utils.js;
```

#### A file's purpose should be clear from the filename alone, and a filename should be able to resolve any ambiguity that may arise from files with similar purposes in different folders.

A reader should not have to open the file to determine its purpose.

> Why? Since filenames in IDE tabs do not display the additional context of the folders that contain the file or the code within the file, a filename should allow the reader to easily identify the file's purpose.

```
/* avoid */
/client
  /auth.js
/server
  /auth.js

/* good */
/client
  client-auth.js
/server
  server-auth.js
```

#### It may be helpful to reference the parent folder names when naming a file.

Appending or prepending parent folder names to a filename can help create a purposeful and unambiguous name. Don't blindly add parent folders; only do so when they are necessary to make the file's purpose clear or avoid ambiguity.

When adding parent folder names, be flexible. It is fine to change plural names to singular names and vice-versa.

> Should I prepend or append parent folder names? Do whatever feels more natural. Prepending is more consistent with the folder hierarchy but may feel dissonant.

```
/* avoid - handlers is unclear */
/errors
  /validation
    handlers.js

/*
  good - adding parent folders names make the files purpose clear from the name
  alone and prevents ambiguity
*/
/errors
  /validation
    validation-error-handlers.js OR handlers-validation-errors.js
```

#### A file's extension is a part of the filename and may provide additional context.

For example, a `*.js` file tells the reader the file is a JavaScript file, and adding "js" to the name is unnecessary. `*.js` already carries the context of a "js" file.

```
/* avoid - ejs files are templates */
profile-page-template.ejs

/* good */
profile-page.ejs
```

#### Don't overthink file naming.

Remember that the goal is simple: give files names that make the file's purpose clear and resolve ambiguity without being longer than necessary.

Be flexible. A rigid naming abstraction will always fail.

### Naming Folders

#### Folders can have shorter names than files.

> Why? Because folders are viewed in a tree hierarchy. Tree hierarchies provide additional naming context.

```

/* avoid - no need to prepend `client-` to `db` */
/client
  /client-db/
    db-client.js

/* good */
/client
  /db/
    db-client.js

```

**[⬆ Table of Contents](#toc)**

---

## Storybook Design, Code Order

#### Prefer to write source code using storybook design.

Storybook design is the idea that source code should read as a story. Without pushing the analogy too far, when a reader scans the source code in a file/module, the purpose of the code should be clear and logical: what is the interface, how is the code interacted with, what does it do, why do I care?

The following rules are designed to support this idea. However, thinking beyond rules, keep the idea of storybook design in mind when writing code.

#### Prefer to declare and initialize variables where they are needed. For variables intended for use in a nested block, prefer to declare them above and as close as possible to the nested block where they are used.

> Why? Since `let` and `const` are not hoisted, always declaring variables at the top of the enclosing block is no longer needed. Declaring variables where they are needed minimizes their scope, reduces variable span, and reduces variable live time.

> However, if in one's discretion, burying a variable declaration and initialization deep within complex code is unclear, then trust your judgment and move the declaration and initialization closer to the top of the enclosing scope.

Example - variable intended for use in the same block where defined:

```javascript
// discouraged
function foo(goo) {
  let bar = 10; // bar is not needed yet

  if (goo) return false;
}

// preferred - no need to declare a variable before it is used
function foo(goo) {
  if (goo) return false;

  let bar = 10;
}
```

Example - variable intended for use in a nested block:

```javascript
// discouraged - bar defined below the nested block where it is used
function foo() {
  return bar;
}

const bar = 10;

// preferred - bar defined above and close to the nested block where it is used
const bar = 10;

function foo() {
  return bar;
}
```

#### Prefer to define a function below its call site and as close as possible to its call site.

When a function has multiple call sites, place the function definition as close as possible to the first call site.

This rule applies to functions defined on an object literal, class methods, function expressions, and function declarations across a module.

> Why? When using this technique, function calls are typically encountered in the code before the function is defined. Therefore, the reader may be able to determine the purpose of the function from the name alone. This way, if the reader encounters the function definition below they have the option of skipping peering into the implementation; thus saving time and brainpower.<br><br>When this technique is coupled with declaring module exports where they are defined, the module presents itself in an auto-documenting manner.

```javascript
// preferred
{
  function a() {
    b();
    c();
  }

  // called by a() so goes below a()
  function b() {
    c();
  }

  // called by a() and b() so goes below both
  function c() {}
}

// same idea for methods of an object literal
const obj = {
  a() {
    this.b();
    this.c();
  },
  b() {
    this.c();
  },
  c() {},
};

// same idea for prototype methods
class Foo {
  a() {
    this.b();
    this.c();
  }

  b() {
    this.c();
  }

  c() {}
}

// discouraged
function foo() {
  bar();
}

function goo() {}

function bar() {} // further away than necessary from foo()

// preferred - bar is defined close to foo()
function foo() {
  bar();
}

function bar() {}

function goo() {}
```

Example - module code; notice how a reader can scan and see the exports and their dependencies very clearly; organizes itself very nicely:

```javascript
export function foo() {
  a();
  b();
}

function a() {}

function b() {}

export class Bar {
  constructor() {
    c();
  }
}

function c() {}
```

#### When ordering sets of statements/data, which includes variable declarations, object (including class) methods/properties, values in a destructuring assignment, or any other set of statements/data, prefer to define the order using the following guidelines in descending order of importance:

- **Define dependent members above the members they depend on (if possible).**
- **Keep related API functions like `addEventListener` and `removeEventListener` close together.**
- **Place public members above private members.**

> Why? These rules are intended as a catch-all rule to help resolve how to order your code.

> Why push public members towards the top? Public code should be obvious to a reader.

```javascript
// preferred - place dependent object property above object property depended
// upon
const api = {
  getUser () {
    return this.user;
  },
  user: "Jake"
}

// preferred - group api methods in expected order they would be called
const api = {
  addEventListener() {},
  removeEventListener() {}
}

// preferred - place public object method above private method
const api = {
  getName() {}
  #sortData () {}
}

// preferred - export (public) statement above module private statement
export const PI = 3.14159;
const derivedPi = 22 / 7;
```

#### Do not worry about sorting by alpha or any arbitrary ordering system.

> Why? These ordering systems create a lot of overhead for very little gained.

```javascript
// discouraged - no need to arbitrarily sort by alpha
const a;
const b;
const c;
const d;
const e;
const f;
const g;
```

**[⬆ Table of Contents](#toc)**

---

## Code as Documentation

#### Adding unnecessary code for documentation purposes is discouraged. Use code comments or documentation comments (more later) instead.

Note that clarity and documentation are different concepts. Additional code that substantially improves clarity is generally preferred. Additional code that exists to document how the code works or how the code is used is discouraged.

This is a key rule that will help guide many decisions as to how to write code.

> Why? Unnecessary code for documentation can ultimately result in code that is less clear due to there being more code. Also, unnecessary code hurts performance due to larger package sizes.

```javascript
// discouraged - getA() is doing nothing but documenting obj.a
const obj = {
  a: 10,
  getA() {
    return this.a;
  },
};

// preferred
const obj = {
  /**
   * @readonly
   */
  a: 10,
};

// discouraged - no behavior; just creating references to document they exist
class Data {
  constructor() {
    this.a;
    this.b;
  }
}
```

**[⬆ Table of Contents](#toc)**

---

## JavaScript Features

### Whitespace

#### Prefer placing a blank line above a statement that is a different type or serves a different purpose than the statement that precedes it unless it is on the first line of a block. In other words, prefer logical groupings of statements by using blank lines to separate different groups.

For example, a sequence of simple `let` declarations does not need blank lines because they are the same type of statement and serve the same purpose. However, if they were followed by a `for` loop, a blank line above the loop is advised since the `for` loop is different from a `let` declaration and serves a different purpose.

This is just a general advisory for blank lines, and more specific whitespace rules in this guide may override this general preference. Also, this is a very discretionary rule, and a developer's discretion is paramount.

> Why use blank lines? Think of the blank line as a comma in the English language. A comma provides a slight separation between words, phrases, and clauses; similarly, a blank line in JavaScript can show some additional separation between statements. Often, the application of blank lines is a subtle and vital element of a developer's craft like the comma is to a writer.

```javascript
// preferred
const foo = 1;
const bar = 2;

let x = 1;
let y = 2;

// blank line because a function expression is substantively different than a
// simple let declaration
let fn = () => 5;

if (fn() === 5) throw new Error();

for (;;) {}
```

#### For statements that redirect control flow:

- **Prefer to place an empty line above unless it is on the first line of a block.**
- **Prefer to place an empty line below unless it is on the last line of a block.**

For example, place empty lines above and below statements like `return`, `break`, `continue`, `throw`, and function calls.

> Why? The blank line draws more attention to a statement that is having a consequential effect on the control flow of the program.

```javascript
// discouraged
foo(); // missing blank line below
let x = 1;

function fn() {
  let foo = 1;
  return; // missing blank link above
}
fn();

for (let i = 0; i < 10; i++) {
  let foo;

  if (i == 10) {
    foo = 5;
    break; // missing blank link above
  }
}
bar(); // missing blank link above
throw new Error(); // missing blank link above

// preferred
foo();

let x = 1;

function fn() {
  let foo = 1;

  return;
}

fn();

for (let i = 0; i < 10; i++) {
  let foo;

  if (i == 10) {
    foo = 5;

    break;
  }
}

bar();

throw new Error();
```

**[⬆ Table of Contents](#toc)**

---

### Control Statements and Structures

#### Prefer to drop unnecessary braces for control structures except for conditional statements with more than one condition.

```javascript
// discouraged
if (foo === "bar") {
  console.log();
}

// preferred
if (foo === "bar") console.log();

// discouraged
if (foo === "bar") console.log("bar");
else console.log("not bar");

// preferred - always use braces for multiple conditions
if (foo === "bar") {
  console.log("bar");
} else {
  console.log("not bar");
}
```

#### Prefer `switch` statements to `if` and `else` statements when you have four or more conditions.

```javascript
// discouraged
if (foo === 1) {
} else if (foo === 2) {
} else if (foo === 3) {
} else {
}

// preferred
switch (foo) {
  case 1:
    break;

  case 2:
    break;

  case 3:
    break;

  default:
}
```

#### Prefer `for-of` statements when looping through iterables.

> Why? Since JavaScript allows the creation of custom iterables that can be looped over via `for-of`, it makes sense to prefer `for-of` as a standard looping mechanism.

```javascript
const arr = [1, 2, 3];

// discouraged
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

// preferred
for (const element of arr) {
  console.log(element);
}
```

**[⬆ Table of Contents](#toc)**

---

### Exceptions

#### Throw `Error` — or a derived `Error` type — objects over ad-hoc error handling techniques.

Avoid custom error handling.

> Why? The language provides an error-handling technique that is widely understood by developers. Using custom error handling techniques is unnecessary.

```javascript
// avoid
throw "error";

// good
throw new Error("error");
```

#### Prefer to create errors with a message. The message should use proper grammar.

> Why? The error message helps to quickly understand the error.

```javascript
// discouraged
throw new Error();

// discouraged
throw new Error("no user input");

// preferred
throw new Error("No user input.");
```

#### Prefer to have non-empty catch blocks.

If one believes that an empty catch block is appropriate, leave a comment explaining why.

> Why? Ignoring errors is unusual and requires justification.

```javascript
// discouraged
try {
  errorThrowingCode();
} catch {}
```

#### Prefer to omit the catch error argument if the argument is not used.

> Why? Its omission is allowed by the language and is more concise.

```javascript
// discouraged
try {
} catch (err) {
  log("error");
}

// preferred
try {
} catch {
  log("error");
}
```

**[⬆ Table of Contents](#toc)**

---

### Operators

#### Prefer strict equality operators like `===` and `!==` when performing comparisons.

> Why? If abstract and strict comparison operators are mixed, it can be easy for a conscientious developer to confuse them. Using only strict equality frees one's mind from needing to be careful to catch the difference between `==` and `===`.

```javascript
// discouraged
let foo = bar == 1 ? goo : car;

// preferred
let foo = bar === 1 ? goo : car;
```

#### For conditional statements like `if` comparisons, prefer using shortcut "truthy" checks over explicit comparisons when applicable.

> Why? Truthy checks are concise and consistent. Learning the rules of type coercion to boolean values requires some effort, but it is worthwhile. Especially since it prevents one from being shocked when reading the abundant code out in the wild that uses truthy checks.

```javascript
// discouraged
if (str === "") {
}
if (bool === true) {
}

// preferred
if (str) {
}
if (bool) {
}
```

#### Prefer control structures (`if` statements, etc.) over operators (`|| && ? :`, etc.) when the expression's return value is not used.

> Why? Semantically, operators are intended for expressions, not statements, and should be used sparingly when managing control flow rather than returning values.

```javascript
// discouraged
!isTrue && start();
!isTrue ? start() : null;

// preferred
if (isTrue) start();

// acceptable - expression's return value is used
const foo = !isTrue && start();
const bar = !isTrue ? start() : false;
```

#### Prefer control statements to break up complex expressions.

Be wary of complex nested logical and conditional operators.

> Why? Nested operators can be very difficult to comprehend.

```javascript
// discouraged
let value = isTrue ? (check() ? 10 : isString() ? 5 : 1) : 1;

// preferred
const value = (() => {
  if (isTrue && check()) return 10;

  if (isString()) return 5;

  return 1;
})();
```

#### Prefer the unary arithmetic operators (`++` and `--`) where applicable.

Be certain you understand how prefix versus postfix unary operators differ.

> Why prefer unary arithmetic operators? They are expressive, concise, and fundamental to the language.

```javascript
// discouraged
num += 1;
num -= 1;

// preferred
num++;
num--;
--num;
++num;
```

#### Include parenthesis when applying the `new` operator to a constructor function.

> Why? For consistency and because omitting the parentheses may result in subtle errors.

```javascript
// good
const foo = new Foo();
```

#### If using bitwise operators, leave a comment describing their usage.

> Why? Most mere mortals will not immediately understand bitwise operations.

```javascript
let num = 10;

// avoid - no explanatory comment
(num & 1) === 0;

// good
// true if even
(num & 1) === 0;
```

**[⬆ Table of Contents](#toc)**

---

### Primitive Types and Built-Ins

#### Prefer creating regular expressions via a regular expression literal.

> Why? The literal is faster, clearer, and a bit more concise.

```javascript
// discouraged
let re = new RegExp("ab+c");

// preferred
let re = /ab+c/;
```

#### Never create primitives by using the new operator on primitive object wrappers.

> Why? The created value is not a primitive; it is an object. This is extremely confusing and should be avoided. The objects are also slower than true primitives.

```javascript
// avoid
const num = new Number(0);
const str = new String("");
const bool = new Boolean(false);

console.log(typeof num); // "object"
console.log(typeof str); // "object"
console.log(typeof bool); // "object"

if (num) console.log("yes, I am truthy");
if (str) console.log("yes, I am truthy");
if (bool) console.log("yes, I am truthy");

// preferred
const num = 0;
const str = "";
const bool = false;

console.log(typeof num); // "number"
console.log(typeof str); // "string"
console.log(typeof bool); // "boolean"

if (!num) console.log("no, I am not truthy");
if (!str) console.log("no, I am not truthy");
if (!bool) console.log("no, I am not truthy");
```

#### Prefer to convert data to a primitive type by explicitly passing the data as an argument to an object wrapper function.

Exceptions are clearly stated in this guide.

> Why use object wrapper functions for conversion? This technique is more evident because it uses explicit conversion rather than implicit coercion techniques.

```javascript
// discouraged
const str = 0 + "";

// preferred
const str = String(0);
```

#### Prefer to use two logical NOT operators (`!`) to perform boolean type conversion.

> Why? This technique is concise, clear, and effective.

```javascript
const num = 10;

// discouraged
const bool = new Boolean(num);
const bool = Boolean(num);

// preferred
const bool = !!num;
```

**[⬆ Table of Contents](#toc)**

---

### Strings

#### Prefer to allow string literals to overflow the column width rather than placing them across multiple lines.

> Why? Broken strings are difficult to maintain and can be less obvious to readers.

```javascript
// discouraged
const kennedy =
  "We choose to go to the moon. We choose to go to the moon in this decade \
and do the other things, not because they are easy, but because they are \
hard ...";

const kennedy =
  "We choose to go to the moon. We choose to go to the moon in this decade" +
  " and do the other things, not because they are easy, but because they are" +
  " hard ...";

// preferred
const kennedy =
  "We choose to go to the moon. We choose to go to the moon in this decade and do the other things, not because they are easy, but because they are hard ...";
```

#### Prefer template literals/strings over string concatenation.

> Why? Template strings support convenient features, use a standard syntax, and are easier to make changes to.

```javascript
const foo = "foo";
const bar = "bar";

// discouraged
const str = foo + " " + bar;

// preferred
const str = `${foo} ${bar}`;
```

**[⬆ Table of Contents](#toc)**

---

### Variables

#### Declare variables with `const` or `let`. Use `const` by default. Use `let` only if a variable needs to be reassigned.

> Why? Both declaration types avoid the confusion that stems from functional hoisting.

```javascript
// avoid
var foo = "bar";

// good
const foo = "bar";

// good
let foo = "bar";
```

#### Avoid using `var`.

> Why? `let` can accomplish everything `var` can without hoisting, which can be confusing. `let` also uses block scope, which is more obvious than functional scoping.

#### Use one declaration per variable.

> Why? By decoupling variable declarations, it is easier to add new declarations and to locate variables. Also, one declaration per variable makes it less tempting to define all variables in one place rather than above where they are needed as dictated by storybook design.

```javascript
// avoid
let foo, bar;

const goo = 1,
  car = 2;

// good
let foo;
let bar;

const goo = 1;
const car = 2;
```

#### For a sequence of variable declarations, prefer to group `const` declarations above grouped `let` declarations.

> Why? Consistency. Also, mixed-up declarations are ugly.

```javascript
// avoid
const foo = 1;
let bar;
const goo = 2;
let car;

// good
const foo = 1;
const goo = 2;

let bar;
let car;
```

#### Use UPPERCASE and snake_case for deeply immutable constants.

> Why? This is the standard convention.

> What is deeply immutable? If the value is determined at write-time, it is probably deeply immutable. Conversely, if the value is determined at runtime, or it could change, then it is probably not deeply immutable.

```javascript
// avoid - not deeply immutable; could change later
const FAV_NUMBER = 7;
const LAST_USER_BIRTHDAY = "8.8.2019";
const COLOR = "red";

// good
const PI = 3.14159;
const FELIX_BIRTHDAY = "8.8.2019";
const RED = "red";
```

#### If a value is boolean, prefer to prefix the value's identifier name with _is_.

> Why? This is a simple convention to improve clarity.

```javascript
// discouraged
const valid = true;

// preferred
const isValid = true;
```

#### For references to DOM elements, append a "DOM" to the end of the name.

> Why? It is useful to have a quick convention to spot DOM elements in code.

```javascript
// avoid
const div = document.createElement("div");

// good
const divDOM = document.createElement("div");
```

**[⬆ Table of Contents](#toc)**

---

### Enums

#### Fake the enum data type using these rules:

- **A `const` variable assigned to an object literal.**
- **The variable identifier is named using UpperCamelCase.**
- **Property names are UPPERCASE snake_case.**
- **Give each property a string value that identifies the property.**

> Why? This technique is a reasonable compromise to fake the enum data type in JavaScript. It lacks guards to prevent different properties from having the same value, and it lacks a simple membership test, but it is simple and intuitive to use.

```javascript
const BigCarCompanies = {
  TESLA: "tesla",
  TOYOTA: "toyota",
  VOLKSWAGEN: "volkswagen",
};
```

**[⬆ Table of Contents](#toc)**

---

### Objects

#### Prefer to create objects using literal syntax.

> Why? The literal syntax is concise and fast.

```javascript
// discouraged
let obj = new Object();

// preferred
let obj = {};
```

#### Prefer placing an object literal on a single line if it fits within the column width. However, format the object as a block-like structure if, in one's discretion, clarity is substantively improved.

> Why? Being concise is generally superior as long as clarity is preserved. However, clarity is paramount; trust your judgment.

```javascript
// discouraged
let obj = {
  foo: 1,
  bar: 2,
};

// preferred - assuming the single line version is clear
let obj = { foo: 1, bar: 2 };

// discouraged
const arr = [
  {
    foo: 1,
  },
];

// preferred - assuming the single line version is clear
const arr = [{ foo: 1 }];
```

#### For pure data POJOs, prefer object literals that do not have empty rows.

> Why? The lack of empty rows makes the object look more like a data structure.

```javascript
// discouraged
const foo = {
  name: "Jake",

  sonOne: "Felix",

  sonTwo: "Calvin",

  doggo: "Laika",
};

// preferred
const foo = {
  name: "Jake",
  sonOne: "Felix",
  sonTwo: "Calvin",
  doggo: "Laika",
};
```

#### For objects that have methods, prefer placing empty rows between all properties.

> Why? The empty rows make the object look more like an API.

```javascript
// discouraged
const foo = {
  birthday: "8.8.2019",
  getAge() {},
  getHeight() {},
};

// preferred
const foo = {
  birthday: "8.8.2019",

  getAge() {},

  getHeight() {},
};
```

#### Prefer dot notation `.` to access object properties over bracket notation `[""]`.

> Why? Dot notation avoids adding the noisy quotations required by bracket notation.

```javascript
// discouraged
const foo = obj["foo"];

// preferred
const foo = obj.foo;
```

#### Avoid using special characters in object property names.

> Why? Special characters require bracket notation to access object properties.

```javascript
// avoid
const goo = obj["foo-bar"];

// good
const goo = obj.fooBar;
```

#### Prefer to create all object properties in one place.

This preference includes dynamic property names.

> Why? Grouped properties make it easier to understand the object's purpose.

```javascript
// discouraged
let obj = {};
obj.foo = 1;
obj[getKey("bar")] = 2;

// preferred
let obj = {
  foo: 1,
  [getKey("bar")]: 2,
};
```

#### Prefer object property shorthand.

> Why? Shorthand is descriptive and concise.

```javascript
const foo = "bar";

// discouraged
let obj = {
  addBar: function (value) {
    return value * 2;
  },
  foo: foo,
};

// preferred
let obj = {
  addBar(value) {
    return value * 2;
  },
  foo,
};
```

#### Prefer the spread operator to copy objects.

> Why? The spread operator is concise and avoids additional mutations.

```javascript
let obj = { a: 1, b: 2 };

// discouraged
const newObj = Object.assign(obj);

// preferred
const newObj = { ...obj };
```

#### Prefer destructuring to access object properties.

> Why? Destructuring is concise and clear.

```javascript
let obj = { a: 1, b: 2 };

// discouraged
let a = obj.a;
let b = obj.b;
let val1 = obj.a;
let val2 = obj.b;

// preferred
let { a, b, a: val1, b: val2 } = obj;
```

#### For mixin objects — objects intended for object composition — prefer names using the format: nounal name + "Mixin".

> Why? This nomenclature clearly states the purpose of a mixin and signals that these objects are intended to be used with object composition.

```javascript
// preferred
const eventEmitterMixin = {
  addEvent() {},

  removeEvent() {},
};

class EventEmitterMixin {
  addEvent() {}

  removeEvent() {}
}
```

**[⬆ Table of Contents](#toc)**

---

### Object Concepts

#### Prefer cohesive objects.

If an object has internal state data, the more object methods that use the internal state, the more cohesive the object.

> Why prefer high cohesion? Highly cohesive objects are typically loosely-coupled and adhere to the single responsibility rule.

#### Prefer to think of objects as peers, not as having parent-child relationships.

> Why? This line of thinking fosters object composition, and object composition is generally considered a better technique to add functionality than object hierarchies.

**[⬆ Table of Contents](#toc)**

---

### Arrays

#### Prefer to create arrays using literal syntax.

> Why? Faster creation time, a simpler syntax, and less error-prone due to the variadic nature of the Array constructor.

```javascript
// avoid
let arr = new Array();

// good
let arr = [];
```

#### Prefer the spread operator when applicable.

This preference includes, but not limited to, (1) copying arrays, (2) converting iterables to arrays, and (3) array concatenation.

> Why? The spread operator is very concise.

```javascript
// copying arrays
let foo = [1, 2, 3];
let bar = [...foo]; // preferred over foo.slice()

// converting iterables to arrays
function fn() {
  let foo = [...arguments]; // preferred over Array.prototype.slice.call(arguments)
}

// array concatenation
let foo = [0, 1, 2];
let bar = [3, 4, 5];

foo = [...foo, ...bar]; // preferred over foo.concat(bar)
```

#### Prefer array destructuring.

Omit variables for unused elements.

> Why? Array destructuring is very concise and clear.

```javascript
let arr = [1, 2, 3, 4, 5];

// discouraged
const value1 = arr[0];
const value2 = arr[1];

// preferred
const [value1, value2] = arr[0];

// preferred - omit elements not used
const [value1, , , , value5];
```

**[⬆ Table of Contents](#toc)**

---

### Events

#### Prefer verbal event names. In other words, the name should begin or end with a verb or verb-like word.

> Why? Events represent actions and processes.

```javascript
// discouraged
const event = { type: "enter" };
function triggerEnter() {}

// preferred
const event = { type: "enterDown" };
function triggerEnterDown() {}
```

#### Prefer to name event handler functions _handle_ + the event name. The entire name should use the standard lowerCamelCase convention.

> Why? This technique makes it easy to recognize an event handler. Also, _handle_ signals the lazy nature of the callback function instead of making it appear that the event listener is eagerly triggering the function call.

```javascript
// discouraged
function clickListener(event) {}

// preferred
function handleClick(event) {}
```

#### For events that can be canceled, prefer names that have the present participle `ing` appended to the event name.

> Why? This convention makes it clear that the event is cancellable.

```javascript
addEventListener("loading", event => {
  event.preventDefault();
})

dispatchEvent(new Event("loading");
```

**[⬆ Table of Contents](#toc)**

---

### Functions

#### Prefer function declarations over function expressions.

Default to function declarations, but remember that function expressions are still useful.

> Why prefer declarations? The principal argument against declarations is that they hoist. However, hoisting can be viewed as an advantage for functions because it allows depended-upon functions to be written under the dependent code, and this is useful because it facilitates code that reads in a top-down manner (storybook design). Also, function declarations require a name, which eliminates the hard-to-track-down bugs that unnamed function expressions create. Finally, the keyword `function` appearing on the left side of the declaration provides clarity to the reader. When a reader scans the source code, the functions are clear. When one assigns all of one's functions to `const` variables, the source is less self-documenting.

> Named functions are the only reliable way to get robust stack inspection.

```javascript
// discouraged
const getValue = function anotherName() {};
const getValue = () => {};

// preferred
function getValue() {}
```

#### Place a blank line above function declarations unless the declaration is on the first line of a block.

```javascript
// avoid
function foo() {}
function bar() {}

// good
function foo() {}

function bar() {}
```

#### Avoid declaring functions inside conditional blocks. Use function expressions instead or rewrite the code.

> Why? JS engines handle them differently, especially pre-ECMAScript 2015 engines.

```javascript
// avoid
if (true) {
  function checker() {}
}

// acceptable
if (true) {
  const checker = function () {};
}
```

#### When passing multiple values as a single argument or returning multiple values, prefer object literals over arrays.

> Why? An object literal allows each value to have a different name, which facilitates destructuring the return value. Also, it is easier to add new values to an object because arrays couple a value to its position, which makes it harder to add values without breaking any code that relies on the old order.

```javascript
// avoid
function foo([strValue = "one", numValue = 1] = []) {
  return ["two", 2];
}

// good
function foo({ strValue = "one", numValue = 1 } = {}) {
  return {
    strValue: "two",
    numValue: 2,
  };
}
```

#### Use rest parameter syntax for variadic functions.

Avoid relying on the `arguments` object.

> Why? `...` parameters are a real array, unlike the array-like `arguments`.

```javascript
// avoid
function foo() {
  let args = Array.prototype.slice.call(arguments);
}

// good
function foo(...args) {}
```

#### Never name a parameter `arguments`.

Prefer using the term `args`.

> Why? Because of the confusion from shadowing the array-like arguments object.

```javascript
// avoid
function foo(arguments) {}

// preferred
function foo(args) {}
```

#### When calling a function and a specific value for `this` is not needed, prefer the spread operator over `Function.prototype.apply`.

> Why? The spread operator syntax is concise and prevents the need to provide a dummy `this` value.

```javascript
const arr = [1, 2, 3];

function foo(one, two, three) {}

// discouraged
foo.apply(null, arr);

// preferred
foo(...arr);
```

#### When a function has 4 or more required parameters, prefer consolidating all required parameters into a single object.

> Why? This makes it easier to refactor functions and accommodate change.

```javascript
// discouraged
function foo(a, b, c, d) {}

// preferred
function foo({ a, b, c, d }) {}
```

#### Prefer to place optional parameters after required parameters in the function signature.

Prefer to not mix required and optional properties.

> Why? These conventions make it clear to readers what parameters are optional and which are not. Placing optional parameters at the end of the function signature is the standard convention most developers know and expect, and by supplying optional parameters with values, it is even more apparent which parameters are optional and which are not.

```javascript
// discouraged
function foo(bar = 10, car, goo) {}

// preferred
function foo(goo, bar = 10, car = "") {}
```

#### If there is more than a single optional parameter, prefer consolidating the optional parameters into a single destructured object.

> Why? Otherwise, when calling the function, some optional parameters may have to have dummy values passed to them.

```javascript
// discouraged
function foo(reqA, reqB, optA, optB, optC) {}

// call only wants to pass optC; required to pass dummy values to earlier
// parameters
foo(1, 2, null, null, 3);

// preferred
function foo(reqA, reqB, { optA, optB, optC } = {}) {}

foo(1, 2, { optC: 3 });
```

#### For functions where the number of arguments may change in the future, or when required versus optional arguments varies, prefer a single object parameter.

> Why? Simplicity.

#### Parameters do not use default value initializers that create side effects.

> Why? This creates undesirable coupling between function call sites and functions.

```javascript
// avoid
let val = 1;

// ++val changes state outside the function
function foo(bar = ++val) {}

foo();

// good
let val = 1;

function foo(bar = val) {}

foo(++val);
```

#### When using rest syntax in a destructuring assignment for arguments, prefer to name the rest properties "props" for required properties and "optionalProps" for optional rest properties.

> Why? This convention is clear and frees the developer from having to invent a name.

```javascript
// discouraged
function({ a, b, c, ...args }, { optA, optB, ...options }) {}

// preferred
function({ a, b, c, ...props }, { optA, optB, ...optionalProps }) {}
```

#### For objects with required object parameters, prefer to define the required props before the optional properties in the function signature.

> Why? Consistency with the convention that required parameters are defined before optional parameters.

```javascript
// discouraged
function foo({ optA = "a", req } = {}) {}

// preferred
function foo({ req, optA = "a" } = {}) {}
```

#### Avoid `null` and `undefined` arguments in function calls.

Use an optional parameter instead or change the order of the required parameters.

> Why? They are ugly and noisy.

```javascript
// avoid
function foo(a, b, c) {}
foo(undefined, 1, 2);

// prefer
function foo(b, c, a) {}
foo(1, 2);
```

#### For global calls in a browser, omit `window`.

> Why? If one couples global calls to `window`, then the JavaScript code only works in the browser environment. Also, it is unnecessarily verbose.

```javascript
// avoid
window.addEventListener("click", (event) => {});

// good
addEventListener("click", (event) => {});
```

#### Prefer to name functions that handle asynchronous behavior with the action verb prefix _handle_.

> Why? This nomenclature makes the function's lazy nature clear.

```javascript
// preferred
function handleClick(event) {}
function handleLoad() {}
```

#### For functional mixins — functions intended to add behavior to objects — prefer names using the format: "mix" + a verbal description of what the mixin does.

> Why? This nomenclature clearly states the purpose of the function.

```javascript
// preferred
function mixColor(obj) {
  return Object.assign(obj, {
    getColor() {
      return "red";
    },
  });
}

const obj = {
  blackAndWhite() {
    return true;
  },
};
const colorObj = mixColor(obj);
```

#### For plugins that add functionality to a framework, prefer naming their hook methods by using a leading "register" and a descriptor.

```javascript
// preferred
const plugin {
  registerFunctionality (framework) {}
}

function framework(plugin) {
  plugin.registerFunctionality();
}
```

**[⬆ Table of Contents](#toc)**

---

### Function Concepts

#### Prefer smaller functions over larger functions.

Some tests to determine if a function is getting too large:

- Does the function have more than three parameters?
- Can you break out logic into a new function and give it a name that is not a restatement of the implementation?

> Why prefer smaller functions? In short, easier composition, easier testing, easier reuse, more DRY, clearer control flow, etc. See the single responsibility rule.

> Note, this preference should not be taken to an extreme and make the code hard to comprehend.<br><br>The biggest drawback to small functions is that they can make the code more difficult to understand because the control flow no longer moves in a top-down fashion. Instead, the control flow moves based on function calls, and function calls require the reader to pause their thinking in the main function and jump to a secondary function, comprehend the secondary function, and then jump back to the main function. This can be challenging and is similar to reading a paragraph in a novel that forces you to reference a glossary to comprehend each sentence.<br><br>In short, if breaking up a function is making the code difficult to comprehend, then consider leaving the larger function intact.

#### Prefer to break out reusable logic into helper/utility functions.

> Why? DRY code is preferable to WET code.

#### (Optional) Consider adding explicit block scopes inside of function bodies to improve code clarity and isolate variable declarations.

> Why? Limiting a scope's exposure is an extension of the principle of least privilege. Optional blocks are a form of defensive programming.

```javascript
function foo() {
  let x;

  // adding optional block scope to isolate the code block below
  {
    const y = 10;
    for (let i = 0; i < y; i++) {
      x = i;
    }
  }

  return x;
}
```

**[⬆ Table of Contents](#toc)**

---

### Arrow Functions

#### Prefer arrow function expressions for anonymous functions.

> Why? All things being equal, they offer a more concise syntax.

```javascript
// discouraged
const arr = [1, 2, 3].map(function (x) {
  return x * 2;
});

// preferred
const arr = [1, 2, 3].map((x) => x * 2);

// discouraged
function foo(x, y, z = function () {}) {}

// preferred
function foo(x, y, z = () => {}) {}
```

#### Prefer arrow functions over techniques that use `this` hacks.

In other words, if one needs a lexical `this`, then use arrow functions.

> Why? Arrow functions are an idiomatic way to handle function context.

```javascript
// discouraged
const context = this;
addEventListener("click", function (event) {
  context.onClick();
});

// preferred
addEventListener("click", (event) => {
  this.onClick();
});
```

#### Omit the curly brackets only if the return value is used and there are no side effects.

> Why? Arrow functions are already difficult to read. By requiring brackets and an explicit `return` for more complex functions, confusion is minimized.

```javascript
let foo = 1;
let bar = 2;

// avoid - side effects and the return value is not used
arr.forEach((element) => (foo++, bar++));

// good
forEach((element) => {
  foo++;
  bar++;
});

// avoid - side effects
const newArr = arr.map((element) => (foo++, element * 2));

// good
const newArr = arr.map((element) => {
  foo++;

  return element * 2;
});

// acceptable - return value is used and no side-effects
const newArr = arr.map((element) => element * 2);
```

**[⬆ Table of Contents](#toc)**

---

### Generator Functions

#### Generators are a useful addition to the language. Use them as applicable.

> Why? Generators enable developers to create custom iterables, which is something to be embraced.

```javascript
// good
function* genFunction(start = 0, end = 100, step = 1) {
  let count = 0;

  for (let i = start; i < end; i += step) yield ++count;

  return count;
}
```

**[⬆ Table of Contents](#toc)**

---

### Classes, Constructor Functions

#### Use the `class` syntax over other class (prototype) techniques.

This includes using `extends` for prototypal inheritance.

> Why? `class` syntax is clear and easy to understand. Also, since it is the new standard, it is better understood by other developers than ad-hoc techniques.

```javascript
// avoid
function Kls() {}

Kls.prototype.foo = function () {};

// good
class Kls {
  foo() {}
}

// good
class ExtKls extends Kls() {}
```

#### All constructor functions use UpperCamelCase for their names.

> Why? This technique is the standard convention.

```javascript
// avoid
class klsOne {}
function klsTwo() {}

// good
class KlsOne {}
function KlsTwo() {}
```

#### Avoid manipulating prototypes directly.

> Why? This is essentially a restatement of the preference for `class` syntax.

#### Prefer the following code order inside a class definition.

The order of methods within each section should reflect storybook design as defined earlier in this guide.

> Why? Predictable structure is helpful because it reduces the number of decisions the person writing the code has to make, and it helps the reader navigate to sought-out methods.

1. Static public properties
1. Static private properties
1. Static public setter/getter
1. Static private setter/getter
1. Static public methods
1. Static private methods
1. Public properties
1. Private properties
1. Public setter/getter
1. Private setter/getter
1. Constructor
1. Public methods
1. Private methods

> Note - Even though the preference for public methods is above private ones, storybook design may require private methods to be defined above public methods. Storybook design is dispositive.

```javascript
// preferred
class Foo {
  static a;

  static #b;

  static get c() {}
  static set c(value) {}

  static get #d() {}
  static set #d(value) {}

  static e() {}

  static #f() {}

  g = 10;

  #h = 20;

  get i() {}
  set i(value) {}

  get #j() {}
  set #j(value) {}

  constructor() {}

  k() {}

  #l() {}
}
```

#### Prefer to place a blank line after `super` calls when extending.

> Why? The separation makes methods easier to read.

```javascript
// discouraged
class Foo extends Bar {
  constructor() {
    super();
    this.prop = 1;
  }
}

// preferred
class Foo extends Bar {
  constructor() {
    super();

    this.prop = 1;
  }
}
```

#### Place a blank line between methods, getters, and setters.

> Why? The blank line makes it much easier to distinguish the methods.

```javascript
// avoid
class Kls {
  foo() {}
  bar() {}
  goo() {}
}

// good
class Kls {
  foo() {}

  bar() {}

  goo() {}
}
```

#### Avoid empty constructors.

> Why? Habitually defining constructors is a waste of time and bytes.

```javascript
// avoid
class Kls {
  constructor(...args) {
    super(...args);
  }
}

// good
class Kls {}
```

#### Getters and setters are useful additions to the language. Use them as applicable.

Getter/setter functions are primarily useful in two contexts: (1) using a getter alone to provide read-only access to an object's internal state, and (2) using a getter for read access along with a setter to change internal state.

```javascript
// acceptable
class Kls {
  constructor() {
    this.#foo = 1;
  }

  get() {
    return this.#foo;
  }

  set(value) {
    this.#foo = calcFoo(value);
  }
}
```

#### Define getters before setters.

> Why? Convention.

```javascript
// avoid
set(value) {}

get() {}

// good
get() {}

set(value) {}
```

#### Avoid changing state in getters.

> Why? Changing state in the getter couples call sites to the getter, which is unnecessary and potentially confusing.

```javascript
// avoid
class Kls {
  get count() {
    return ++this._count;
  }
}
```

#### Use idiomatic private properties and methods for classes.

They help document the code and they are easily compressed by minifiers.

```javascript
// good
class Foo {
  #internal = 10;

  #privSetter() {}
}
```

#### Prefer to define bound methods as properties rather than using `bind` on prototype methods.

When creating instance properties that are functions, define them in the functions section of the class definition rather than the properties section.

> Why? This is a much cleaner syntax.

```javascript
// discouraged
class Kls {
  constructor() {
    this.setProp = this.setProp.bind(this);
  }

  setProp(value) {}
}

// preferred
class Kls {
  setProp = (value) => {};
}

// avoid - `setProp` points to a function; should be defined in the methods
// section that is below the constructor
class Kls {
  setProp = (value) => {};

  constructor() {}
}

// good
class Kls {
  constructor() {}

  setProp = (value) => {};
}
```

#### Prefer class methods that use the `this` variable.

If a function does not use `this`, consider moving it to a non-class method.

> Why? This practice promotes cohesive classes that do not violate the single responsibility rule.

```javascript
// discouraged - no `this` is used
class Kls {
  double(value) {
    return value * 2;
  }
}

// preferred - double moved to non-class method
class Kls {}

function double(value) {
  return value * 2;
}
```

**[⬆ Table of Contents](#toc)**

---

### Object Factories, Class, Constructor Functions, Prototypes

#### Object factories are preferred to constructor functions for object creation.

> Why not use class or prototypes? My principle gripe against prototypes is that requiring the `this` keyword makes their use less flexible. I like being able to destructure methods, and pass the methods around without needing to keep in mind the context of the method. In principle, I really like the idea of prototypes and the consistency of the class syntax. But in practice, I find them to be more cumbersome than they are worth.

```javascript
// discouraged
class Person {
  constructor(name) {
    this.name = name;
  }
}

// preferred
function createPerson(name) {
  return {
    name,
  };
}
```

#### For object factories, prefer names using the format: "create" + object name.

> Why? This nomenclature clearly states the purpose of the function.

```javascript
// preferred
function createPerson() {
  return { name: "Calvin" };
}
```

#### Avoid the `this` keyword.

Use closures to capture state instead.

```javascript
// discouraged - using `this`
function createPerson(name) {
  return {
    birthday: "12.8.2022",

    getAge() {
      return this.birthday;
    },
  };
}

// preferred
function createPerson(name) {
  const birthday = "12.8.2022";

  const person = {
    birthday,

    getAge() {
      return birthday;
    },
  };

  return person;
}
```

#### A useful factory pattern is declaring all initialization variables and functions towards the top of the creational function, then create an API object with public properties, and then return the API object.

> Why write out initialization variables and functions towards the top? It is easier to read code that is written in a top-down fashion.

> Why return a named API object? By creating the API object by name, public methods can call other public methods and return itself for method chaining. This technique is self-documenting and makes it easy to add new methods to the API.

```javascript
function createPerson(name) {
  // declare all variables and functions for initialization here towards the top
  const birthday = "12.8.2022";

  let birthdayDateTime = getBirthdayDatetime();

  function getBirthdayDatetime() {
    return parseDate(birthday);
  }

  // create api object
  const api = {
    birthday,

    getBirthdayDatetime,

    // reference api object to access public property
    getAge() {
      return api.birthday;
    },

    calcGeneration() {
      // reference api object to call other public method
      const gen = api.getAge();
    }

    setAge(age) {
      // return api to alow method chaining
      return api;
    },
  };

  return api;
}
```

#### Prefer object composition over prototypal inheritance.

> Why? Object composition is more flexible.

```javascript
// discouraged
class Dog {}

class Golden extends Dog {}

// preferred
function createDog() {
  return {};
}

function createGolden() {
  return Object.assign(createDog(), {});
}
```

#### Useful criteria for when to use constructor functions:

- When they are required.
  - _Examples_:
    - Using the built-in `Error` object.
    - Creating custom elements.
- Large numbers of objects are created, and the performance and/or memory consumption of the object creation is critical.
  - For these use cases, construction can be optimized by moving methods to the reused prototype.
- Inheritance is expected by third-party consumers, which makes an idiomatic technique useful.

> Why? Prototypes have narrowly defined use-cases.

```javascript
// required
class Popup extends HTMLElement {
  constructor() {
    super();
  }
}
customElements.define("popup-info", Popup);

// required
new Error("Error message here.");
```

#### Useful criteria for when prototypal inheritance may be preferable to object composition:

- The entire API of the superclass must be available to consumers of the extended object.
- The types of arguments stay consistent.
  - Typescript flavored JSDoc doesn't allow extensions to change argument types without re-declaring them. I hate writing code to accommodate JSDoc.
- Inheritance is intended to be performed by third parties. Inheritance has the advantage of providing a simple mechanism for other users to conform to your implementation.

Generally, object composition is preferred.

**[⬆ Table of Contents](#toc)**

---

### Modules

#### For greenfield projects, prefer JavaScript modules syntax to import dependencies and export bindings.

If one is using a bundler, prefer this syntax for import/export.

> Why? JavaScript modules are a part of the specification, and browser support is very good.

```javascript
// discouraged
const utility = require("./utilities.js");

module.exports = class Kls {};

// preferred
import { utility } from "./utilities";

export class Kls {}
```

#### Module filenames are not required to rigidly reflect the names of exported identifiers.

Generally, exported identifiers will likely reflect the file's purpose and be reflected in the filename. But, this is not required.

> Why? Naming flexibility is necessary. Also, it is not always possible to reflect the exported identifiers in the filename. For example, a file may export a single default export, but the default export may be a composite object that contains many identifiers.

```javascript
export default class createBtnComponent() {}
```

```
// acceptable
/client-button.js
```

**[⬆ Table of Contents](#toc)**

---

### Module Imports

#### Exclude the file extension in import paths when permissible.

> Why? This convention promotes consistency and allows for future typescript support. It is also more concise.

```javascript
// avoid
import "./code.js";

// good
import "./code";
```

#### Imports go above other code in the module.

> Why? This convention reinforces the fact that import statements are hoisted and available across the module.

```javascript
// avoid
let foo;

import "bar";

// good
import "bar";

let foo;
```

#### Wildcard imports are discouraged.

> Why? Wildcard imports are more difficult to tree-shake and less self-documenting because they do not explicitly list what is imported.

```javascript
// discouraged
import * as fns from "./fns";

// preferred
import { fnA, fnB } from "./fns";
```

#### Prefer to order imports in the following way:

1. **Built-in (native) modules.**
1. **Modules in node_modules.**
1. **Local library modules.**
1. **Local modules.**
1. **Non-JavaScript files.**

**Place a blank line between each section.**

> Why are non-JavaScript files placed at the bottom? This way imported styles are defined after styles defined by dependencies. This allows composite components to override the styling from composed components.

```javascript
// preferred
import fs from "fs"; // node.js module

import lib from "library_in_node_modules";

import { D, d, k } from "google/d"; // local third-party modules

import { F, f, l } from "F"; // local modules

import "./styles/a.css"; // non-js files
```

#### Do not habitually sort imports by alpha.

> Why? It is a lot of effort for very little gain and is a difficult to maintain abstraction.

#### Do not habitually sort destructured bindings.

> Why? It is a lot of effort for very little gain and is a difficult to maintain abstraction.

```javascript
// discouraged
import { A, a, b, g, Z, z } from "./utils";

// acceptable
import { g, Z, b, A, G, a, j } from "./utils";
```

#### (Optional) Consider breaking up a section into sub-sections for clarity.

Separate each sub-section with a newline and order them in any way that makes sense.

```javascript
/*
  acceptable - even though each import is a local module and should be grouped
  together; still breaking them up into sub-sections to highlight naming modules
  versus utility modules
*/
import NameA from "./NameA";
import NameB from "./NameA";
import NameC from "./NameA";

import { utilityA } from "./utilitiesA";
import { utilityB } from "./utilitiesB";
import { utilityB } from "./utilitiesC";
```

#### If importing both a default export and destructured exports from a single module, prefer to use a single import statement. List the default export first.

> Why? This convention minimizes the number of import statements.

```javascript
// discouraged
import Foo from "./Foo";
import { utils } from "./Foo";

// discouraged
import { utils }, Foo from "./Foo";

// preferred - place default export first
import Foo, { utils } from "./Foo";
```

#### Renaming named imports is discouraged.

Only do so to avoid naming collisions.

> Why? Aliasing adds an additional level of indirection.

```javascript
// discouraged
import { foo as bar } from "./foo";

// preferred
import { foo } from "./foo";

// acceptable - avoid name collision
import { addEventListener } from "./foo";
import { addEventListener: addBarEventListener } from "./bar";
```

**[⬆ Table of Contents](#toc)**

---

### Module Exports

#### Prefer named exports over default exports.

> Why prefer named exports? This is a tough one: on the one hand, default exports encourage smaller modules, which fosters cohesive and orthogonal modules. However, since default exports do not have a default import name, this leads to inconsistencies for the import name across modules. It is simpler to avoid default exports.

```javascript
// discouraged
export default class Kls {}

// preferred
export class Kls {}
```

#### Avoid exporting directly from an import in a single statement.

> Why? One line re-exports break the convention on where imports and exports are located in a module. Consistency is more important than conciseness.

```javascript
// avoid
import A from "A";
export { specificName } from "./other";
import B from "B";

// avoid
import A from "A";
import B from "B";

export { specificName } from "./other";

// good - a statement for the import and the export
import A from "A";
import B from "B";
import { specificName } from "./other";

export { specificName };
```

#### Place re-exported imports immediately below all of the other import statements.

> Why? This convention keeps re-exports as close to their corresponding import statement as possible.

```javascript
// avoid
import A from "A";
import B from "B";
import C from "C";

export class Foo {}

export { A };

// good - re-export immediately follows imports
import A from "A";
import B from "B";
import C from "C";

export { A };

export class Foo {}
```

#### Prefer to export values/functions where they are defined.

> Why? This convention makes the module's interface evident to a reader as they scan the code. Also, it encourages storybook design.

```javascript
// discouraged
function foo() {}

const obj = {};

function bar() {}

export { foo, bar };

// preferred - export where defined
export function foo() {}

const obj = {};

export function bar() {}
```

#### Circular dependencies between modules are discouraged.

If circular dependencies are necessary, leave an explanatory comment. Use with caution.

> Why? Circular dependencies are simply confusing and increase coupling between modules.

#### Use constant exports.

Avoid exporting mutable bindings.

> Why? Modules should be able to depend on an exported item without it changing.

```javascript
// avoid
export let foo = 10;

// good
export const foo = 10;
```

#### Place a blank line above and below export statements.

> Why? This convention makes the important keyword `export` more easily noticed by the reader.

```javascript
// avoid
const foo = 1;
export { foo };
for (;;) {}

// good
const foo = 1;

export { foo };

for (;;) {}
```

**[⬆ Table of Contents](#toc)**

---

### CJS Modules

#### If using CJS modules, export inline code using the `exports.*` syntax rather than `module.exports`.

> Why? This is consistent with the the ES modules preference and reduces refactoring time since a change in the name of an exported function does not trigger another change in the `module.exports` object.

```javascript
// avoid
function exportMe() {}

module.exports = {
  exportMe,
};

// good
exports.exportMe = function () {};
```

**[⬆ Table of Contents](#toc)**

---

### Module Concepts

#### When exporting an API and determining whether to export an object factory or standalone data/functions, export an object factory if:

1. Multiple instances (possibly) are required.
1. Initialization data or creation timing is required. Or,
1. A consistent technique across a series of related components is needed.

Otherwise, prefer to export data/functions and manage state directly in the module.

> Why? Module syntax provides great support for inline export of data and functions. Other than the use cases above, there is no need to create an object factory.

```javascript
// discouraged - pure functions do not need multiple instances
export function createPureUtilsFunctions () {
  return {
    foo () {},
    bar () {}
  }
}

// preferred
export foo() {}
export bar() {}
```

#### Prefer highly orthogonal modules.

Minimize how changes in one module force changes in other modules. Try to keep modules independent and decoupled.

#### Prefer to place side-effect causing code that runs when the module is initialized towards the top of the module.

> Why? Since the code will cause a side-effect every time the module is used, it should be obvious to readers.

```javascript
// discouraged
import { modifyDOM } from "utils";

function longFunc () {
  ...
}

modifyDOM();

// preferred - `modifyDOM` moved towards the top of the module
import { addStyleRulesToTheDom } from "utils";

modifyDOM();

function longFunc () {
  ...
}
```

**[⬆ Table of Contents](#toc)**

---

### Restricted JavaScript Features

#### Avoid executing JavaScript in loose mode.

Note, JavaScript modules only run in strict mode.

> Why strict mode? For a multitude of reasons: security, performance, preventing global variables, and standardization, to name a few.

#### Use dynamic code evaluation (`eval`, `new Function`) with extreme caution.

Leave an explanatory comment to justify their use.

> Why? Both features are slow, potentially dangerous, and almost always unnecessary.

#### Avoid non-standard JavaScript features. Only use features that are in the official spec and have broad runtime support.

This proscription includes features that have been removed, in-progress web standards, or features that rely on transpilers for broad support.

```javascript
// avoid - not in spec; requires transpilers
@deco
class Kls {}

function deco(target) {
  deco.annotated = true;
}
```

#### Modify built-ins with extreme caution.

There are legitimate use cases (shims/polyfills) for modifying built-ins, but they are narrowly prescribed.

> Why? Modifying built-ins open up the possibility of collisions with other library code and bugs due to breaking changes in the future.

```javascript
// avoid
Array.prototype.sum = () => {};
```

**[⬆ Table of Contents](#toc)**

---

## Application Architecture

### General

#### Services are modules that export functionality and manage an internal state and/or cause side-effects.

Exported functionality that does not manage an internal state or cause side-effects are simply utilities.

Note, the totality of the exported functions in a module are a singular "service". Each function is not a service, and the module does not export "services". The module exports a "service".

#### Utilities are exported pure (or purish...) functions that are not specific to your application's business logic.

The utilities folder should be a toolbox that you can ideally lift and put in another project with minimal effort.

#### Helpers are modules that export functionality that is intended to be used in another module. When a module API grows large, consider re-exporting helper modules to keep the API clean.

Helpers are a way to pull out code from a module to make it smaller more readable.

Keep helper modules close to the modules that they are used within. Typically, they are stored inside a sub-folder of the folder containing the consumer module.

#### In your project directory structure, prefer to place modules close to the modules that consume them.

> Why? This way, related modules/files will be close to one-another and easily accessible in the file tree.

#### Prefer to co-locate modules by functionality (what they do) rather than their technical category.

In other words, prefer to keep domain-related modules together instead of grouping them by what type of role they satisfy from an architectural perspective.

> Why? This technique makes it easier to determine where to place modules. Sometimes, a module may not cleanly fit into an architectural role, which makes it difficult to determine where to place it (such modules often end up in `/utilities`). By having folders grouped by functionality, it should be easier to locate where modules should be placed.

```
#discouraged
/routes/
  /api.js
  /products.js
  /user.js
/schema/
  /api.js
  /products.js
  /user.js
/testing
  /api.js
  /products.js
  /user.js

#preferred
/api
  /api-routes.js
  /api-schema.js
  /api-tests.js
/products
  /products-routes.js
  /products-schema.js
  /products-tests.js
/user
  /user-routes.js
  /user-schema.js
  /user-tests.js
```

### Client-Side

#### Common src folders:

- `src/components`
- `src/services` - modules that add application functionality for different features of the application.
- `src/utils`
- `src/types` - shared type definitions, enums, classes, and jsdoc definitions that do not fit cleanly into a feature folder.

### Node

#### Divide up apps into feature/domain folders with a file in the root directory named `server` that bootstraps the server.

Optionally, a `.env` file at the root may be useful to store site secrets.

```
#example folders/files
.env
/auth
/cars
/client
/customers
server.js
```

#### Common top-level folders:

- `/client` - the client application.
- `/web` - public website(s).
- `/types` - shared type definitions, enums, classes, and jsdoc definitions that do not fit cleanly into a feature folder.
- `/utils` - shared utils.
- `/validators` - shared validators.
- `/public` - static files accessible by name.

#### Each top-level feature/domain folder prefers these sub-folders:

- `/routes` - Post requests should use CRUD prefixes in the url. E.G. `/create-topic`
- `/handlers` - Controllers. The only function types that can accept `req`, `res`,and `session` objects.
  - Prefer thin controllers and put business logic in the services.
    - HTTP request handlers should just concern themselves with HTTP and data shape validation.
  - Responses prefer a JSON response with the following signature: `{ok: boolean, error: string|string[]}`;
  - Exported functions use `handleXXX` as a naming scheme.
- `/data` - All exported functions use CRUD prefix names like `readData`, `updateData`, etc. Data functions are "dumb" and use simple CRUD functions. The services are smart.
  - Data functions are the gateway to the persistence layer. All SQL/DB code is in these functions.
  - Prefer the following top-down order for exported functions: `read/update/create/delete`.
  - Domain entities are defined in types. E.G. `User`, `Car`, `Customer`.
- `/services` - Domain level exported functions that are the API that each feature uses to communicate with each-other, and they are the gateway to the data model. Services are "smart" and data models are "dumb". They provide the API for features to interact with one-another. They also provide the data that the controllers use.
  - When deciding which service a function belongs to, consider the data. What data is being mutated, created, or read? What service does this data fit into the best?
  - Prefer the following top-down function order: `get/set/add/remove`.
- `/pages` - Templates and static view files.
- `/src` - Source files for any transpiled, compiled, or bundled libraries.
  - Even for multiple discrete bundles, prefer to put them all in a single `/src` folder per feature.
- `/validators` - Validators are middleware used to validate data before it gets to the services.
  - All exported functions use `validateXXX` as a naming scheme. They validate and sanitize data in requests.
  - They validate the shape of data so typically there are no hits to the database or services.
  - For errors, either throw `400`|`500` for tampering, or errors in an array on the `Request` object for handling by controllers.
- `/types` - Enums, classes, and jsdoc definitions that are specific to the feature, and can be used by other features.
- `/utils` - Feature specific utilities.

**[⬆ Table of Contents](#toc)**

---

## Minification

#### Prefer to assign object properties to new variables when it will substantially increase minification.

In other words, if an object property is used many times or has a very long name, assigning the property to a variable can allow a minifier to greatly reduce the code length.

This indirection is only worthwhile if the minification savings are substantial.

> Why? Object properties can not be reliably minified. Variables defined in the local scope can be minified.

> Private class properties are easily minified.

```javascript
// destructuring
function ({someExampleProp: a}) {}

// assignment
const a = this.someExample.prop.view.state.a;
```

**[⬆ Table of Contents](#toc)**

---

## Comments and Documentation

### Commenting Overview

#### Use `//` (end-of-line comments) and single-line `/* ... /*` (asterisks comments) for _implementation comments_. Use `/** ... */` for all _documentation comments_.

> What exactly are implementation comments? Implementation comments are technical comments that describe a particular concrete implementation. They are intended to be consumed by readers of the source and usually directly reference specific code. Implementation comments are not required, and their creation is left up to the developer's discretion. If a comment does not make sense without reference to the source code, it is probably an implementation comment.

> What are documentation comments? Documentation comments describe how to interact with code and should be comprehensible without reference to the source code. Documentation comments are designed to be consumed by developers reading the source and by anyone who is reading external documentation. Documentation comments examples include license, copyright, module description, API methods, export descriptions, JSDoc, etc. If a comment would make sense to readers of an external manual on how to use the source code, then it is probably a documentation comment.

```javascript
/**
 * This class helps with colors. (documentation)
 */
class Color {
  getColor(foo /** string (doc comment) */) {
    // memory leaks can occur here if you are not careful (implementation)
    let fn = function () {
      /* lorem ipsum (impl comment) */
    };
  }
}
```

#### Use technical terms in comments.

Use a vocabulary that is understood by the intended audience.

#### Write comments in a natural language.

> Why? Comments complement code; comments do not restate code. Since code uses a non-natural language, comments should use a natural language to avoid merely repeating the code.

```javascript
// avoid
function fn() {
  // forEach(element => ...)?
  for (let i = 0; i < 10; i++) {}
}

// good
function fn() {
  // foreach may be better
  for (let i = 0; i < 10; i++) {}
}
```

#### Choose a style guide to resolve any natural language style questions.

Also, if one's natural language has different national varieties, pick one to resolve differences between them. For example, if using English, decide to use American English, British English, Canadian English, or any other national variety to resolve differences.

I use Wikipedia's style guide for English located here: [Wikipedia:Manual of Style [English]](https://en.wikipedia.org/wiki/Wikipedia:Manual_of_Style).

> Why Wikipedia? Their guide is thorough, free, searchable, and accessible.

#### Prefer to place comments immediately above the subjects of the comments.

> Why? This convention makes it clear to what code a comment refers.

```javascript
// discouraged

// test database

function testDatabase() {}

function testDatabase() {} // test database

/**
 * This is the test database function.
 */

function testDatabase() {}

// preferred

// test database
function testDatabase() {}

/**
 * This is the test database function.
 */
function testDatabase() {}
```

#### Place an empty line before a comment unless it's on the first line of a block.

> Why? Without a blank line, code becomes cramped.

```javascript
// avoid

const foo = 1;
/**
 * A function.
 */
function fn() {
  let foo = 10;
  // bar is the default
  let bar = -10;
}

// good

const foo = 1;

/**
 * A function.
 */
function fn() {
  let foo = 10;

  // bar is the default
  let bar = -10;
}
```

### Implementation Comments

#### Prefer to make source code self-documenting instead of relying on implementation comments for clarity.

Some code requires comments to make it clear, but most code does not.

> Why? Using a comment to provide clarity couples the comment to the code so that changes in the code triggers changes to the comment. If this coupling is unnecessary, then avoid it.

```javascript
// avoid - comment below is unnecessary
for (let i = 0; i < 10; i++) {
  // retrieve element by index
  const obj = obj[i];
}
```

#### `//` is strongly preferred over `/* */` for implementation comments.

If `/* */` are used for implementation comments, they must be on a single line.

> Why discourage `/* */` style comments? Since this type of comment can be embedded inline within code, they are a distraction that hurts code comprehension. Also, by only using asterisks in documentation comments, the distinction between implementation and documentation comments is stark.

```javascript
// discouraged
function getColor(foo /* always an integer */) {}

// preferred
// foo is always an integer
function getColor(foo) {}
```

#### Write implementation comments:

- **In lowercase only (this includes code in the comment).**
- **Use punctuation only when necessary for clarity.**
- **Sentence fragments are permissible if the meaning of the fragment is clear.**
- **Separate sentences and sentence fragments with semicolons.**

**Otherwise, use formal grammar, e.g., verb conjugation, subject-verb agreement, etc. Focus on clarity.**

This rule only applies if it makes sense with regard to one's natural language. This author intends no English language chauvinism.

> Why simplify grammar? Simplifying grammar frees developers from many grammatical debates and decisions. Also, grammatical simplification means that a developer does not have to drift as far from the coding mindset when writing a comment as one would if formal grammar was required. In other words, thinking about formal grammar can throw one's mind out of a coding groove.

```javascript
// avoid
// The function below calculates the color value and then returns it. Color is
// encoded using R.G.B. values.
const color = fn();

// good
// returns color; color is rgb
const color = fn();
```

#### Start implementation comments with a single space.

> Why? A comment with a space is much easier to read.

```javascript
// avoid
//test database

// good
// test database
```

#### For implementation comments that overflow the line width, break after the last word that fits on the line, and continue with a new comment on the next line.

Why? This technique ensures that the comment is visible regardless of the word-wrapping setting on the reader's text editor.

```javascript
// avoid
// lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure

// good
// lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor
// incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
// nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat
// duis aute irure
```

#### Use a _TODO_ implementation comment to signify follow-up work. Such comments should appear at the top of the file to call attention to them.

> Why? _TODO_ is the most common convention for action comments.

```javascript
// TODO rewrite using new syntax
```

**[⬆ Table of Contents](#toc)**

---

### Documentation Comments, JSDoc

#### All documentation comments are written using JSDoc syntax.

The terms JSDoc and documentation comments can be used interchangeably.

> Why? JSDoc is useful for auto-documentation and is the standard convention for JavaScript.

#### Prefer TypeScript flavored JSDoc.

> Why? TypeScript enabled IDEs will get improved type checking and intellisense support.

```javascript
// discouraged
/** @type {function(string, boolean): number} Closure syntax */

// preferred
/** @type {(s: string, b: boolean) => number} TypeScript syntax */
```

#### Write JSDoc descriptions using formal grammar.

> Why? JSDoc may be used to generate documentation that is read without reference to the code. Therefore, the code can not serve as the implied subject for descriptions, and formal grammar can help provide clarity to the reader.

```javascript
// avoid
/**
 * get ui colors
 *
 * @param {string} type Component type
 */
function getColor(type) {}

// good
/**
 * Retrieves the correct color for UI components.
 *
 * @param {string} type The type of component.
 */
function getColor(type) {}
```

#### Single line annotations are only allowed for @type annotations or type aliases.

> Why? No documentation is necessary since the type is defined elsewhere.

```javascript
// allowed
/** @type {CustomType} */
const foo;

// allowed - type alias
/** @typedef {import("../foo.js").FooType} FooType */
```

#### Place a blank line between the JSDoc description and any block tags. Avoid placing empty lines between block tags.

> Why? The blank line makes it much easier to read the description. Other blank lines are not necessary.

```javascript
// discouraged
/**
 * Description goes here.
 * @param {string} foo
 *
 * @param {string} bar
 *
 * @returns {number} The sum of foo and bar.
 */

// preferred
/**
 * Description goes here.
 *
 * @param {string} foo
 * @param {string} bar
 * @returns {number} The sum of foo and bar.
 */
```

#### For JSDoc descriptions that overflow the line width, break after the last word that fits on the line, and continue on the next line.

Why? This technique ensures that the description is visible regardless of the word-wrapping setting on the reader's text editor.

```javascript
// avoid
/**
 * lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure
 */

// good
/**
 * lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor
 * incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
 * nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat
 * duis aute irure
 */
```

#### Allow inline descriptions for block tags to overflow the line width.

> Why not indent? Continuation lines between block tags are simply ugly.

```javascript
// discouraged
/**
 * @param {string} X The following is a very long comment that does not fit on
 *   one very long line.
 */

// preferred
/**
 * @param {string} X The following is a very long comment that does not fit on one very long line.
 */
```

#### Capitalize all object types, including `Object`.

> Why? Consistency and TypeScript flavored JSDoc sometimes requires it.

```javascript
// avoid
/**
 * @typedef {object} SpecialType Creates a new type named 'SpecialType'.
 */

// good
/**
 * @typedef {Object} SpecialType Creates a new type named 'SpecialType'.
 */
```

#### Spaces around the union character "|" are discouraged.

> Why? Improved conciseness.

```javascript
// discouraged
/**
 * @param {string | boolean} SpecialType
 */

// preferred
/**
 * @param {string|boolean} SpecialType
 */
```

#### Spaces around the equal sign "=" in default values are discouraged.

> Why? Improved conciseness.

```javascript
// discouraged
/**
 * @prop {string} [prop = "a"]
 */

// preferred
/**
 * @prop {string} [prop="a"]
 */
```

#### Prefer to start descriptions with a capital letter.

> Why? It makes the start of the description obvious.

```javascript
// discouraged
/**
 * @typedef {Object} SpecialType creates a new type named 'SpecialType'
 */

// preferred
/**
 * @typedef {Object} SpecialType Creates a new type named 'SpecialType'
 */
```

#### Hyphens before an inline description are discouraged unless it is required for clarity.

> Why? It is more concise to exclude the hyphen and is already clear since IDEs change colors for contrast.

```javascript
// discouraged - inline descriptions have hyphen
/**
 * @typedef {Object} SpecialType - Creates a new type named 'SpecialType'.
 * @property {string} prop1 - A string property of SpecialType.
 * @prop {number} [prop5 = 42] - An optional number property of SpecialType with default.
 */

// preferred
/**
 * @typedef {Object} SpecialType Creates a new type named 'SpecialType'.
 * @property {string} prop1 A string property of SpecialType.
 * @prop {number} [prop5 = 42] An optional number property of SpecialType with default.
 */
```

#### A description is not required if the type already provides an adequate description.

```javascript
// good
/**
 * A type that is a Foo.
 *
 * @typedef {Object} Foo
 * @prop {string} bar
 */

// no description is necessary since the type provides a description
/**
 * @type {Foo}
 */
export const foo;
```

#### Do not worry about sorting @props by alpha or any other arbitrary sorting system.

> Why? This is a hard to maintain abstraction that provides little benefit.

#### Avoid placing JSDoc annotations above `import` statements.

In other words, JSDoc annotations are always below `import` statements.

> Why? Consistency.

```javascript
// avoid - @typedef above import
/**
 * @typedef {Object} Type
 */

import Foo from "bar";

// good
import Foo from "bar";

/**
 * @typedef {Object} Type
 */
```

#### If an imported type is used more than once in a module, prefer to create a top-level alias to the imported type with the same name.

> Why? It is more concise to read an alias type than a full import path.

```javascript
// discouraged
/** @type {import("./types").Foo} */
const foo;

/** @type {import("./types").Foo} */
const anotherFoo

// preferred
/** @typedef {import("./types").Foo} Foo

/** @type {Foo} */
const foo

/** @type {Foo} */
const anotherFoo
```

#### For the anything/everything type, prefer to use `any` instead of `*`.

> Why? Asterisks can be confusing since they are also used for other purposes.

```javascript
// discouraged
/** @type {*} */

// preferred
/** @type {any} */
```

**[⬆ Table of Contents](#toc)**

---

### Documentation Concepts

#### A file/module can, at a developer's discretion, have a top-level JSDoc comment with:

- **An optional description.**
- **An optional `@author` tag.**
- **An optional `@version` tag.**
- **An optional `@license` tag.**

#### Link to license descriptions.

> Why? Large license headers are very noisy, distracting, and force heavy scrolling.

```javascript
// avoid
/**
 * @license Permission is hereby granted, free of charge,...
 */

// good
/**
 * @license MIT - https://en.wikipedia.org/wiki/MIT_License
 */
```

#### Document the interface for a file. For modules, document all exports. Exported functions and data should have intellisense support.

This includes types that are indirectly exported.

> Why? This serves the primary purpose of documentation, which is to illustrate how to use the interface.

```javascript
/**
 * A class named Foo.
 *
 * @extends Bar
 */
export class Foo extends Bar() {
  /**
   * Creates Foo(s).
   *
   * @param {number} x - The first number.
   * @param {number} y - The second number.
   */
  constructor(x, y) {}
}

// indirect export of the bar function
/**
 * @returns {bar}
 */
export function foo() {
  return bar;
}

/**
 * This is the bar function. I am documented because I am indirectly exported.
 */
function bar() {}
```

#### Documenting more than what is necessary is discouraged.

Also, if the name of an API property/method makes its purpose obvious, then there is no need to write a description.

However, always document the parameter types of API properties/methods.

> Why? Dogmatic approaches to documentation are hard to maintain and accomplish little.

```javascript
// discouraged
export class Foo {
  /**
   * This method sets the color of the class.
   *
   * @param {string} color Hex representation of the color.
   */
  setColor(color) {}
}

// good - a description of `setColor` is not needed
export class Foo {
  /**
   * @param {string} color Hex representation of the color.
   */
  setColor(color) {}
}
```

#### Documenting private/non-exported/non-interface code is discouraged.

An exception is if one is satisfying a type-checker.

Prefer to make private code self-documenting, and failing that, use implementation comments to provide guidance.

> Why? JSDoc for everything is overkill.

```javascript
// discouraged - documenting a private method
class Foo {
  /**
   * @private
   * @param {string}
   */
  #method() {}
}
```

#### Creating files that contain only JSDoc annotations and no source code is discouraged. Instead, put JSDoc annotations in files with source code.

The exception is for global types that must be placed in files without source code, imports, or exports.

> Why? Files with JSDoc and no source code are unnecessary and confusing unless one is creating global types.

#### Prefer to place JSDoc annotations directly above where they are first referenced.

```javascript
// virtual JSDoc annotation above where first referenced
/**
 * A number or a string containing a number.
 *
 * @typedef {(number|string)} NumberLike
 */

/**
 * Set the magic number.
 *
 * @param {NumberLike} x The magic number.
 */
function foo(x) {}
```

#### Prefer to place type alias towards the top of a file.

> Why? This way the alias will be available within the entire file and will be easy for the reader to locate.

```javascript
/** @typedef {import ("./Component.js").Component} Component */
```

**[⬆ Table of Contents](#toc)**

---

## Globalization

#### Combine localization and internationalization into one concept: globalization.

> Why? Making localization and internationalization different concepts is confusing and unnecessary. IBM and Oracle also use globalization.

**[⬆ Table of Contents](#toc)**

---

## Programming Paradigms

#### (Optional) Consider a functional-lite approach, especially for helper/utility functions.

Some criteria for a functional-lite approach:

- Plan for composition.
  - Write small, unary functions that have outputs that can serve as inputs to other functions when possible.
  - Keep function signatures simple to generalize inputs.
- Prefer the use of pure functions.
  - Note, that a function is pure even if impure techniques are used in the function body as long as the impure techniques are not observable outside the function.
- Prefer idempotent functions.
- When triggering side-effects, try to isolate them and make them obvious.
- Use a point-free style if convenient, but do not get carried away.
- If using complex functors/monads, consider an explanatory comment because many developers are not familiar with this programming style.

#### Avoid becoming an architectural astronaut.

Obsessing over the perfect folder structure, names, and design will only ensure the application is never finished.

**[⬆ Table of Contents](#toc)**

---

## Abstraction Concepts

#### Be cautious when using terms for concepts that do not exist in Javascript. For example, including but not limited to terms like abstract classes, interfaces, or access modifiers like public, private, protected.

This isn't a prohibition of the usage of such terms; just be judicious.

> Why? Usage of such terms may cause confusion and unnecessary theological debates about the propriety of the use of concepts that do not exist in JavaScript.

```javascript
// discouraged
class IAbstractFoo {
  publicBar() {}
}
```

#### Avoid hard-to-maintain abstractions.

> Why? A complex abstraction, despite good intentions, is typically not maintained.

```javascript
// avoid - hungarian notation; hard to enforce across application
const intNum = 10;
const floatNum = 10.5;
```

**[⬆ Table of Contents](#toc)**

---

## Resources

Thanks to the guides below for inspiration.

- Airbnb JavaScript Style Guide.
- Google JavaScript Style Guide.
- [Naming cheatsheet](https://github.com/kettanaito/naming-cheatsheet#ahclc-pattern)

**[⬆ Table of Contents](#toc)**

---

## Epilogue

Perhaps the single most crucial point to take from any style guide is to be consistent. When an abrupt style change occurs, it can cause a cognitive break that throws a developer out of their groove. Try to be consistent!

\- Jake Knerr

**[⬆ Table of Contents](#toc)**

---
