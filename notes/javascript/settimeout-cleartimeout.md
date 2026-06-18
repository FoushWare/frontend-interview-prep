# setTimeout & clearTimeout

## setTimeout

Executes a function after a specified delay.

```js
setTimeout(() => {
  console.log("Hello");
}, 1000);
```

Output after 1 second:

```text
Hello
```

---

## Syntax

```js
setTimeout(callback, delay);
```

Parameters:

* callback
* delay (milliseconds)

---

## Return Value

`setTimeout` returns a timer ID.

```js
const timerId = setTimeout(() => {
  console.log("Hello");
}, 1000);
```

---

## clearTimeout

Cancels a scheduled timeout.

```js
const timerId = setTimeout(() => {
  console.log("Hello");
}, 1000);

clearTimeout(timerId);
```

Output:

```text
Nothing
```

---

## Why Debounce Uses clearTimeout

Without cancellation:

```js
setTimeout(func, 300);
setTimeout(func, 300);
setTimeout(func, 300);
```

Result:

```text
func()
func()
func()
```

With cancellation:

```js
clearTimeout(timerId);
timerId = setTimeout(func, 300);
```

Only the latest timer survives.

---

## Interview Question

### What does clearTimeout do?

It cancels a previously scheduled timeout before it executes.

---

## Revision Notes

Remember:

* setTimeout schedules work.
* clearTimeout cancels work.
* Debounce relies on clearTimeout.
