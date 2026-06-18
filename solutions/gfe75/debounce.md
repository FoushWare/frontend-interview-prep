# Polyfill: Debounce

## Problem Statement
Implement a `debounce(func, wait)` utility function that delays the execution of the provided `func` until after `wait` milliseconds have elapsed since the last time the debounced function was invoked. 

## Requirements
* **Delayed Execution:** `func` should not invoke immediately; it must wait for the duration of `wait`.
* **Argument & Context Preservation:** The returned function must capture and pass the latest arguments and preserve the correct `this` context to `func` upon execution.
* **Reset on Consecutive Calls:** Every new call to the debounced function within the `wait` window must clear the existing timer and start a new one.

---

## Solution

Here is the robust, production-ready implementation utilizing JavaScript closures and `setTimeout`.

```javascript
/**
 * @param {Function} func
 * @param {number} wait
 * @return {Function}
 */
function debounce(func, wait) {
  let timeoutId = null;

  return function (...args) {
    // Preserve the execution context (this)
    const context = this;

    // Clear any existing active timeout to reset the wait window
    if (timeoutId !== null) {
      clearTimeout(timeoutId);
    }

    // Schedule the function execution
    timeoutId = setTimeout(() => {
      func.apply(context, args);
    }, wait);
  };
}
