# Problem: Array.prototype.reduce

## Description
`Array.prototype.reduce` is a way of "reducing" elements in an array by calling a "reducer" callback function on each element in order and passing along the return value from the previous callback. The final result of running the reducer across all elements of the array is a single value.

Implement `Array.prototype.reduce`. To avoid overwriting the actual `Array.prototype.reduce`, which is being used by autograders, implement it as `Array.prototype.myReduce`.

---

## Requirements

* **Delayed/Sequential Execution:** The method must process the array elements in order from left to right.
* **Argument & Context Preservation:** The callback function should receive four arguments:
  1. `accumulator` (the total or result from the previous iteration)
  2. `currentValue` (the current element being processed)
  3. `currentIndex` (the index of the current element)
  4. `array` (the source array itself)
* **Initial Value Handling:** * If an `initialValue` is provided, the loop starts at index `0` and the accumulator is set to `initialValue`.
  * If no `initialValue` is provided, the first real element in the array becomes the accumulator, and processing starts from the next real element.
* **Sparse Arrays:** The function must completely skip empty slots ("holes") in sparse arrays without invoking the callback function on them.
* **Safety Guards:** * Throw a `TypeError` if the provided callback is not a function.
  * Throw a `TypeError` if the array is empty (or completely hollow/sparse) and no `initialValue` is provided.

---

## Examples

```javascript
// Example 1: With an initial value of 0
[1, 2, 3].myReduce((prev, curr) => prev + curr, 0); 
// Returns: 6

// Example 2: With an initial value of 4
[1, 2, 3].myReduce((prev, curr) => prev + curr, 4); 
// Returns: 10

// Example 3: Without an initial value
[1, 2, 3].myReduce((prev, curr) => prev + curr); 
// Returns: 6
