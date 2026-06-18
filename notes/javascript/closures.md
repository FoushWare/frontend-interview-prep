# Closures

## Definition

A closure is created when a function remembers variables from its outer scope even after the outer function has finished executing.

Closures are one of the most important concepts in JavaScript.

---

## Basic Example

```js
function outer() {
  let count = 0;

  return function inner() {
    count++;
    console.log(count);
  };
}

const increment = outer();

increment(); // 1
increment(); // 2
increment(); // 3
```

---

## Why Does This Work?

Normally, local variables disappear after a function finishes.

```js
function test() {
  let name = "Ahmed";
}
```

After `test()` finishes, `name` is gone.

However, when a function references variables from an outer scope, JavaScript keeps those variables alive.

```js
function outer() {
  let count = 0;

  return function () {
    count++;
  };
}
```

The returned function forms a closure over `count`.

---

## Closure Visualization

```text
outer()
 |
 | count = 0
 |
 return inner()
       |
       v
inner remembers count
```

Even after `outer()` finishes, `count` still exists.

---

## Common Use Cases

### Private Variables

```js
function createCounter() {
  let count = 0;

  return {
    increment() {
      count++;
    },

    getCount() {
      return count;
    },
  };
}
```

---

### Debounce

```js
function debounce(func, wait) {
  let timeoutId;

  return function () {
    clearTimeout(timeoutId);
  };
}
```

The returned function remembers `timeoutId`.

---

## Interview Question

### What is a closure?

A closure is a function that remembers variables from its lexical scope even after the outer function has finished execution.

---

## Revision Notes

Remember:

* Functions remember outer variables.
* Closures power debounce.
* Closures power throttle.
* Closures are used for private state.
