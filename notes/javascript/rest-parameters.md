# Rest Parameters (...args)

## Definition

Rest parameters collect multiple arguments into a single array.

---

## Example

```js
function test(...args) {
  console.log(args);
}

test(1, 2, 3);
```

Output:

```js
[1, 2, 3]
```

---

## Why Use It?

Sometimes we don't know how many arguments will be passed.

```js
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}

sum(1, 2, 3, 4);
```

Output:

```text
10
```

---

## Debounce Example

```js
return function (...args) {
  func(...args);
};
```

Suppose:

```js
debouncedSearch("hello");
```

Then:

```js
args = ["hello"];
```

Later:

```js
func(...args);
```

Becomes:

```js
search("hello");
```

---

## Interview Question

### What is the difference between rest and spread?

Rest:

```js
function test(...args) {}
```

Collects values.

Spread:

```js
func(...args);
```

Expands values.

---

## Revision Notes

Remember:

* Rest collects.
* Spread expands.
* Debounce uses both.
