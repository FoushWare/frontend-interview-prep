# JavaScript Interview Questions (Part 2)

Comprehensive JavaScript interview preparation for frontend engineers.

Focus areas:

* Arrays & Objects
* Prototypes
* Classes
* Async JavaScript
* Promises
* Event Loop
* Async/Await
* Error Handling
* Fetch API
* Polyfills
* Senior-Level Questions

---

# 12. Arrays

Arrays store ordered collections.

Example:

```js
const numbers = [1, 2, 3];
```

---

## Common Array Methods

### map()

Transforms array.

```js
const nums = [1, 2, 3];

const doubled = nums.map((n) => n * 2);

console.log(doubled);
```

Output:

```txt
[2, 4, 6]
```

---

### forEach()

Loops through array.

```js
numbers.forEach((n) => {
  console.log(n);
});
```

Returns:

```txt
undefined
```

---

### filter()

Filters items.

```js
const result = [1, 2, 3, 4]
  .filter((x) => x > 2);
```

Output:

```txt
[3,4]
```

---

### find()

Returns first match.

```js
const user = users.find(
  (u) => u.id === 1
);
```

---

### reduce()

Accumulates values.

```js
const total = [1, 2, 3]
  .reduce((acc, curr) => {
    return acc + curr;
  }, 0);
```

Output:

```txt
6
```

---

### some()

Returns true if at least one passes.

```js
arr.some((x) => x > 10);
```

---

### every()

Checks all items.

```js
arr.every((x) => x > 0);
```

---

## Mutating vs Non-Mutating

### Mutating

Changes original array.

```txt
push
pop
splice
sort
reverse
shift
unshift
```

---

### Non-Mutating

Returns new array.

```txt
map
filter
slice
concat
```

---

## Shallow Copy

```js
const newArr = [...oldArr];
```

Problem:

Nested objects still referenced.

---

## Interview Questions

### Junior

1. Difference `map` vs `forEach`?
2. `filter` vs `find`?

### Mid-Level

1. Difference mutable vs immutable operations?
2. Why avoid mutation in React?

### Senior

1. Performance considerations in large arrays?
2. Explain shallow copy issues.

---

## Tricky Questions

### Question

```js
const arr = [1, 2, 3];

const result = arr.map((x) => {
  x * 2;
});

console.log(result);
```

Output:

```txt
[undefined, undefined, undefined]
```

Why?

No `return`.

---

### Question

```js
console.log(
  [1, 2, 10].sort()
);
```

Output:

```txt
[1,10,2]
```

Why?

Sort converts to strings.

Fix:

```js
arr.sort((a, b) => a - b);
```

---

# 13. Objects

Objects store key-value pairs.

Example:

```js
const user = {
  name: "Ahmed",
  age: 30,
};
```

---

## Accessing Properties

### Dot Notation

```js
user.name;
```

---

### Bracket Notation

```js
user["name"];
```

Useful for dynamic keys.

---

## Object Methods

### Object.keys()

```js
Object.keys(user);
```

---

### Object.values()

```js
Object.values(user);
```

---

### Object.entries()

```js
Object.entries(user);
```

---

### Object.assign()

Copy object.

```js
Object.assign({}, user);
```

---

## Destructuring

```js
const { name, age } = user;
```

---

## Spread Operator

```js
const updatedUser = {
  ...user,
  age: 31,
};
```

---

## Deep vs Shallow Copy

Shallow:

```js
const copy = { ...obj };
```

Nested reference problem.

---

## Interview Questions

1. Difference dot vs bracket notation?
2. `Object.keys()` vs `entries()`?
3. Shallow vs deep copy?

---

## Tricky Question

```js
const a = {
  age: 20,
};

const b = a;

b.age = 50;

console.log(a.age);
```

Output:

```txt
50
```

Shared reference.

---

# 14. Prototypes

JavaScript uses prototype inheritance.

Every object inherits from a prototype.

Example:

```js
const user = {};
```

Internally:

```txt
Object.prototype
```

---

## Prototype Chain

Example:

```js
user.toString()
```

Why works?

Inherited from prototype.

---

## Constructor Function

```js
function Person(name) {
  this.name = name;
}

Person.prototype.sayHi =
  function () {
    console.log("Hi");
  };
```

---

## Interview Questions

### Junior

1. What is prototype?

### Mid-Level

1. Prototype chain?

### Senior

1. Prototype inheritance internals?

---

# 15. Classes

Syntactic sugar over prototypes.

Example:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(this.name);
  }
}
```

---

## Inheritance

```js
class Admin extends User {
  deleteUser() {}
}
```

---

## super()

Calls parent constructor.

```js
super(name);
```

---

## Interview Questions

1. Class vs function constructor?
2. What does extends do?
3. What is super?

---

# 16. Promises

Handle async operations.

States:

```txt
pending
fulfilled
rejected
```

---

## Example

```js
const promise =
  new Promise((resolve) => {
    resolve("done");
  });
```

---

## then()

```js
fetchData()
  .then((data) => {
    console.log(data);
  });
```

---

## catch()

```js
fetchData()
  .catch((error) => {
    console.log(error);
  });
```

---

## finally()

Runs always.

---

## Promise.all()

Runs parallel.

Fails if one fails.

```js
Promise.all([
  api1(),
  api2(),
]);
```

---

## Promise.allSettled()

Waits for all.

---

## Interview Questions

### Junior

1. What is promise?

### Mid-Level

1. Promise states?
2. Promise.all vs allSettled?

### Senior

1. Sequential vs parallel requests?

---

## Tricky Question

```js
Promise.resolve(1)
  .then((x) => x + 1)
  .then(console.log);
```

Output:

```txt
2
```

---

# 17. Event Loop

JavaScript is single-threaded.

But async works via:

* Call stack
* Web APIs
* Callback queue
* Event loop

---

## Flow

1. Execute sync code
2. Async task sent to browser
3. Callback enters queue
4. Event loop checks stack
5. Executes callback

---

## Example

```js
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

console.log("3");
```

Output:

```txt
1
3
2
```

---

## Microtasks vs Macrotasks

### Microtasks

Higher priority.

Examples:

```txt
Promise.then
queueMicrotask
```

---

### Macrotasks

Examples:

```txt
setTimeout
setInterval
```

---

## Tricky Question

```js
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");
```

Output:

```txt
1
4
3
2
```

Why?

Promise microtask runs first.

---

## Interview Questions

1. Explain event loop.
2. Why timeout 0 not immediate?
3. Microtask vs macrotask?

---

# 18. Async / Await

Cleaner syntax for promises.

Example:

```js
async function getData() {
  const data =
    await fetch("/api");

  return data;
}
```

---

## Error Handling

```js
try {
  const data =
    await fetchData();
} catch (error) {
  console.log(error);
}
```

---

## Sequential vs Parallel

Sequential:

```js
await api1();
await api2();
```

Slower.

---

Parallel:

```js
await Promise.all([
  api1(),
  api2(),
]);
```

Faster.

---

## Interview Questions

1. async/await vs promise?
2. Why use Promise.all?

---

# 19. Error Handling

## try/catch

```js
try {
  throw new Error();
} catch (error) {
  console.log(error);
}
```

---

## Custom Error

```js
throw new Error(
  "Something failed"
);
```

---

## Interview Questions

1. Difference syntax vs runtime error?
2. Why use try/catch?

---

# 20. Fetch API

Used for HTTP requests.

Example:

```js
const response =
  await fetch("/users");

const data =
  await response.json();
```

---

## HTTP Methods

```txt
GET
POST
PUT
PATCH
DELETE
```

---

## Error Handling

```js
if (!response.ok) {
  throw new Error();
}
```

---

## Interview Questions

1. fetch vs axios?
2. Why check response.ok?

---

# 21. Debounce & Throttle

Very common interview topic.

---

## Debounce

Wait before execution.

Example:
Search input.

---

## Throttle

Runs every interval.

Example:
Scroll event.

---

## Basic Debounce

```js
function debounce(
  fn,
  delay
) {
  let timer;

  return function () {
    clearTimeout(timer);

    timer = setTimeout(() => {
      fn();
    }, delay);
  };
}
```

---

## Interview Questions

1. Debounce vs throttle?
2. Real-world use cases?

---

# 22. Polyfills

Reimplement JS feature.

Example:

```js
Array.prototype.myMap =
  function (cb) {
    const arr = [];

    for (
      let i = 0;
      i < this.length;
      i++
    ) {
      arr.push(
        cb(this[i], i)
      );
    }

    return arr;
  };
```

---

## Popular Polyfills

* map
* filter
* reduce
* bind
* Promise

---

# Common Mistakes

### Mutating state accidentally

Bad:

```js
user.name = "Ali";
```

React issue.

---

### Forgetting return in map

---

### Misunderstanding this

---

### Using await in loop unnecessarily

---

# Coding Exercises

## Exercise 1

Implement:

```txt
map()
```

---

## Exercise 2

Implement debounce.

---

## Exercise 3

Explain output:

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});

console.log("D");
```

---

## Exercise 4

Flatten nested array.

Example:

```js
[1, [2, [3]]]
```

---

## Exercise 5

Group array by property.

---

# Senior-Level Questions

1. Explain event loop deeply.
2. Why JavaScript single-threaded?
3. Explain prototype chain internals.
4. How async works behind the scenes?
5. Promise memory leak cases?
6. How V8 optimizes JS?
7. Deep copy strategies?
8. Performance optimization techniques?

---

# Most Important JS Topics for React Interviews

Priority:

1. Closures
2. Event loop
3. Async/await
4. Arrays & objects
5. Immutability
6. this
7. Scope
8. Hoisting
9. Promises
10. Debounce/throttle
