# JavaScript Interview Questions (Part 1)

Comprehensive JavaScript interview preparation for frontend engineers.

Focus areas:

* JavaScript fundamentals
* Scope
* Closures
* Hoisting
* `this`
* Execution context
* Functions
* Memory
* Tricky interview questions

---

# 1. What is JavaScript?

JavaScript is a:

* High-level language
* Single-threaded
* Interpreted/JIT compiled
* Dynamic language
* Prototype-based language

JavaScript runs in:

* Browser
* Server (Node.js)

JavaScript can:

* Manipulate DOM
* Handle async operations
* Communicate with APIs
* Manage UI state

---

## Interview Questions

### Junior

1. What is JavaScript?
2. Why is JavaScript important?

### Mid-Level

1. Explain JavaScript runtime.
2. Why is JavaScript single-threaded?

### Senior

1. Explain V8 engine.
2. Explain JIT compilation.

---

# 2. JavaScript Data Types

Two categories:

## Primitive Types

Immutable values.

Types:

```js id="j1u8fa"
string
number
boolean
null
undefined
symbol
bigint
```

Example:

```js id="g4s9od"
const name = "Ahmed";
const age = 30;
const isActive = true;
```

---

## Reference Types

Mutable.

Examples:

```js id="9myt0p"
object
array
function
date
map
set
```

Example:

```js id="n5mcl3"
const user = {
  name: "Ahmed",
};
```

---

## Primitive vs Reference

Primitive:

```js id="d6c58q"
let a = 5;
let b = a;

b = 10;

console.log(a);
```

Output:

```txt id="z9a5ox"
5
```

---

Reference:

```js id="ryby6y"
const user1 = {
  age: 20,
};

const user2 = user1;

user2.age = 50;

console.log(user1.age);
```

Output:

```txt id="jrb7gd"
50
```

Because objects share reference.

---

## Interview Questions

### Junior

1. Primitive vs reference?
2. Difference between `null` and `undefined`?

### Mid-Level

1. Why are objects mutable?
2. Explain memory references.

### Senior

1. Explain shallow copy vs deep copy.

---

# 3. Type Coercion

JavaScript automatically converts types.

Example:

```js id="8q2vny"
"5" + 1
```

Output:

```txt id="6u6s4g"
"51"
```

---

Example:

```js id="jlwmxy"
"5" - 1
```

Output:

```txt id="gkqv3n"
4
```

---

Why?

`+` prefers string concatenation.

`-` forces number conversion.

---

## Truthy & Falsy

Falsy values:

```js id="i0y4u9"
false
0
-0
0n
""
null
undefined
NaN
```

Everything else is truthy.

---

## Double Equals vs Triple Equals

### Loose Equality

```js id="jlwmc8"
5 == "5"
```

Output:

```txt id="1kq9gv"
true
```

Type coercion happens.

---

### Strict Equality

```js id="yv0n6v"
5 === "5"
```

Output:

```txt id="wlu0wf"
false
```

---

## Best Practice

Prefer:

```js id="i1rqza"
===
```

---

## Interview Questions

1. Difference `==` vs `===`?
2. What are falsy values?
3. Why `"5" + 1` differs from `"5" - 1`?

---

## Tricky Questions

### Question

```js id="1w5s6l"
[] == false
```

Output:

```txt id="2k3jdx"
true
```

Why?

Type coercion.

---

### Question

```js id="o3z44p"
null == undefined
```

Output:

```txt id="n4o3h9"
true
```

But:

```js id="syrjlwm"
null === undefined
```

Output:

```txt id="hzrxjl"
false
```

---

# 4. Variables

Three ways:

```js id="ibjpnw"
var
let
const
```

---

## var

Function scoped.

Allows redeclaration.

Example:

```js id="w2h9mx"
var x = 1;
var x = 2;
```

Works.

---

## let

Block scoped.

Cannot redeclare.

Example:

```js id="6lmryy"
let age = 10;
```

---

## const

Cannot reassign.

Example:

```js id="fwyfyo"
const name = "Ahmed";
```

---

Important:

Objects inside const can mutate.

Example:

```js id="6rquiw"
const user = {
  age: 20,
};

user.age = 30;
```

Works.

---

## Interview Questions

1. Difference var, let, const?
2. Why avoid var?
3. Can const object change?

---

## Tricky Question

```js id="tfc8gl"
const arr = [1, 2];

arr.push(3);
```

Will it work?

Yes.

Because reference unchanged.

---

# 5. Scope

Scope determines accessibility.

Types:

* Global scope
* Function scope
* Block scope
* Lexical scope

---

## Global Scope

Accessible everywhere.

```js id="m3jlwm"
const appName = "frontend";
```

---

## Function Scope

```js id="m9e23u"
function test() {
  const age = 10;
}
```

Only inside function.

---

## Block Scope

Created with:

```js id="jlwm8q"
{
}
```

Example:

```js id="7lf7pn"
if (true) {
  let x = 5;
}
```

Unavailable outside.

---

## Lexical Scope

Child accesses parent scope.

Example:

```js id="0v7pwk"
function outer() {
  const name = "Ahmed";

  function inner() {
    console.log(name);
  }

  inner();
}
```

---

## Interview Questions

1. Function scope vs block scope?
2. What is lexical scope?
3. Why var dangerous?

---

## Tricky Question

```js id="tmzj41"
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  });
}
```

Output:

```txt id="wgt7ps"
3
3
3
```

Why?

`var` is function scoped.

---

Fix:

```js id="jvshsr"
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  });
}
```

Output:

```txt id="jlwm92"
0
1
2
```

---

# 6. Hoisting

Declarations move to top.

---

## var Hoisting

```js id="mjlwm0"
console.log(a);

var a = 5;
```

Output:

```txt id="80y8g4"
undefined
```

Equivalent:

```js id="jlwmya"
var a;

console.log(a);

a = 5;
```

---

## let & const

Temporal Dead Zone.

Example:

```js id="jlwm5a"
console.log(age);

let age = 20;
```

Output:

```txt id="jlwm4z"
ReferenceError
```

---

## Function Hoisting

Works:

```js id="44mfgs"
sayHello();

function sayHello() {
  console.log("Hi");
}
```

---

Function expression:

```js id="jlwm2x"
sayHello();

const sayHello = () => {};
```

Fails.

---

## Interview Questions

1. What is hoisting?
2. Why let safer?
3. What is TDZ?

---

# 7. Closures

A closure remembers variables from outer scope.

Example:

```js id="jlwm0c"
function outer() {
  let count = 0;

  return function inner() {
    count++;

    return count;
  };
}

const counter = outer();

counter();
counter();
```

Output:

```txt id="jlwm3e"
1
2
```

Because closure remembers `count`.

---

## Real Use Cases

### Private Variables

```js id="x6jlwm"
function bankAccount() {
  let balance = 0;

  return {
    deposit() {
      balance++;
    },

    getBalance() {
      return balance;
    },
  };
}
```

---

### React Hooks

Closures are heavily used in:

```txt id="jlwm1p"
useEffect
useCallback
event handlers
```

---

## Interview Questions

### Junior

1. What is closure?

### Mid-Level

1. Real-world use case?

### Senior

1. Closure memory leak example?
2. How closures work in React?

---

## Tricky Question

```js id="jlwm1t"
function create() {
  const arr = [];

  for (var i = 0; i < 3; i++) {
    arr.push(() => i);
  }

  return arr;
}

const result = create();

console.log(result[0]());
```

Output:

```txt id="jlwm6r"
3
```

Why?

Shared closure with `var`.

---

Fix:

```js id="jlwm5r"
for (let i = 0; i < 3; i++)
```

---

# 8. The `this` Keyword

`this` depends on how function is called.

---

## Global

Browser:

```js id="jlwm4x"
console.log(this);
```

Window object.

---

## Object Method

```js id="jlwm9y"
const user = {
  name: "Ahmed",

  say() {
    console.log(this.name);
  },
};
```

`this` → object.

---

## Arrow Function

Does NOT bind its own `this`.

Example:

```js id="jlwm2n"
const user = {
  name: "Ahmed",

  say: () => {
    console.log(this.name);
  },
};
```

Likely undefined.

---

## call, apply, bind

### call

```js id="sjlwm2"
fn.call(obj);
```

---

### apply

Arguments array.

```js id="0s8h1d"
fn.apply(obj, [1, 2]);
```

---

### bind

Returns new function.

```js id="jlwm0u"
const newFn = fn.bind(obj);
```

---

## Interview Questions

1. What determines this?
2. Arrow vs normal function?
3. call vs apply vs bind?

---

# 9. Functions

Types:

---

## Function Declaration

```js id="jlwm9c"
function sum(a, b) {
  return a + b;
}
```

---

## Function Expression

```js id="mjlwm4"
const sum = function () {};
```

---

## Arrow Function

```js id="djlwm9"
const sum = (a, b) => a + b;
```

---

## Higher Order Functions

Function accepts function.

Example:

```js id="3ujl8x"
arr.map((x) => x * 2);
```

---

## Callback Function

Passed to another function.

---

## Interview Questions

1. Function declaration vs expression?
2. Arrow function benefits?
3. Higher-order function?

---

# 10. Execution Context

JavaScript executes in contexts.

Types:

* Global execution context
* Function execution context

Contains:

* Variable environment
* Scope chain
* `this`

---

## Call Stack

Tracks execution order.

Example:

```js id="jlwm4t"
function one() {
  two();
}

function two() {
  three();
}

function three() {
  console.log("done");
}

one();
```

Stack:

```txt id="jlwm4r"
one
two
three
```

---

## Interview Questions

1. What is execution context?
2. What is call stack?
3. Stack overflow?

---

# 11. Memory Management

Stack:

Primitive values.

Heap:

Objects.

Example:

```js id="jlwm0s"
const user = {
  age: 30,
};
```

Stored in heap.

---

## Garbage Collection

Unused memory cleaned automatically.

Potential leaks:

* Closures
* Timers
* Event listeners

---

## Senior Questions

1. Memory leak examples?
2. How to avoid leaks in React?

---

# Most Important JS Topics

Priority:

1. Scope
2. Closures
3. Hoisting
4. this
5. Async JS
6. Event Loop
7. Promises
8. Objects & Arrays

---

# Practice Exercises

## Exercise 1

Explain output:

```js id="jlwm7k"
console.log(a);

var a = 10;
```

---

## Exercise 2

Explain:

```js id="jlwm3w"
let x = 5;

function test() {
  console.log(x);
}

test();
```

---

## Exercise 3

Build counter using closure.

---

## Exercise 4

Explain output:

```js id="7gxr3r"
const user = {
  name: "Ahmed",

  greet() {
    console.log(this.name);
  },
};

const fn = user.greet;

fn();
```

---

# Senior-Level Questions

1. Explain lexical environment.
2. Difference between scope and execution context?
3. How closures affect memory?
4. Why JavaScript single-threaded?
5. Explain call stack internals.
