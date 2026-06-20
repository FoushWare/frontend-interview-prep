# Problem: Flatten Array

## Description
In modern JavaScript production code, you can use the built-in `Array.prototype.flat()`. However, implementing a custom `flatten` function remains one of the most common frontend interview questions because it tests core competencies in recursion, type checking, and array manipulation.

Implement a function `flatten` that returns a newly created array with all subarray elements concatenated recursively into a single level.

---

## Requirements

* **Recursive Unpacking:** All nested arrays, regardless of depth, must be completely flattened into a single-level array.
* **Immutability:** The function must return a *newly created* array and must not mutate the original input array.
* **Type Retention:** Standard non-array primitive elements (numbers, strings, etc.) must remain unchanged during the process.

---

## Examples

### Flat Arrays
```javascript
// Single-level arrays are unaffected
flatten([1, 2, 3]); // [1, 2, 3]

```



Single-level Nesting

``` javaScript
// Inner arrays are flattened into a single level
flatten([1, [2, 3]]); // [1, 2, 3]

flatten([
  [1, 2],
  [3, 4],
]); // [1, 2, 3, 4]

```

Deep Nesting

``` javaScript
// Flattens deeply nested layers recursively
flatten([1, [2, [3, [4, [5]]]]]); // [1, 2, 3, 4, 5]

```

Skeleton Code

```JavaScript
/**
 * @param {Array} array
 * @return {Array}
 */
export default function flatten(array) {
  // Share your implementation here!
}

```
