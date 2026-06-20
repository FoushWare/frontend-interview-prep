# Problem: Debounce

## Description
Debouncing controls how often a function can execute over time. When a JavaScript function is debounced with a wait time of `wait` milliseconds, it runs only after `wait` milliseconds have elapsed since the debounced function was last called.

You have probably encountered debouncing in daily life before, such as when entering an elevator. Only after some time passes without pressing the "Door open" button (the debounced function not being called) will the elevator door actually close (the callback function is executed).

Implement `debounce(func, wait)` so that `func` is called only after `wait` milliseconds have passed since the most recent call. 

---

## Requirements

* **Delayed Execution:** The returned function should not invoke `func` immediately.
* **Reset Timeline:** Every new call to the debounced function must reset the internal wait timer. 
* **Argument & Context Preservation:** When the delayed call finally runs, it must use the latest arguments and preserve the `this` value from the most recent call.

---

## Arguments
* `func` *(Function)*: The callback to debounce.
* `wait` *(number)*: The number of milliseconds to wait after the latest call.

## Returns
* *(Function)*: Returns the new debounced function.

---

## Examples

### Example 1: Single Call
```javascript
let i = 0;
function increment() {
  i++;
}
const debouncedIncrement = debounce(increment, 100);

// t = 0: Call debouncedIncrement().
debouncedIncrement(); // i = 0

// t = 50: i is still 0 because 100ms have not passed.

// t = 100: increment() was invoked and i is now 1.





/**
 * @param {Function} func
 * @param {number} wait
 * @return {Function}
 */
function debounce(func, wait) {
  // Share your implementation here!
}
