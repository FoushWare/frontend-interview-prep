# Problem: Classnames Utility

## Description
`classnames` is a widely used utility function in modern frontend applications (especially React) to conditionally join CSS class names together into a single space-separated string. 

Implement the `classNames` function to match this standard ecosystem behavior.

---

## Requirements

* **Handling Strings & Numbers:** Plain strings and numbers should be appended directly.
* **Handling Objects:** For objects, keys with truthy values should be included, while keys with falsy values must be ignored.
* **Handling Arrays:** Arrays should be recursively flattened following the same rules established for strings, objects, and nested arrays.
* **Falsy Values:** Falsy arguments (`null`, `undefined`, `false`, `""`, `0`) must be safely skipped entirely.
* **String Cleaning:** The final output string must not contain any duplicate or unnecessary internal spaces, nor any leading or trailing whitespace.

---

## Examples

### Basic Strings and Objects
```javascript
classNames('foo', 'bar'); // 'foo bar'
classNames('foo', { bar: true }); // 'foo bar'
classNames({ 'foo-bar': true }); // 'foo-bar'
classNames({ 'foo-bar': false }); // ''
classNames({ foo: true }, { bar: true }); // 'foo bar'
classNames({ foo: true, bar: false, qux: true }); // 'foo qux'
```



## Recursive Arrays & Mixed Values

```javascript
// Arrays are recursively flattened
classNames('a', ['b', { c: true, d: false }]); // 'a b c'

// Mixed types blend seamlessly
classNames(
  'foo',
  { bar: true, duck: false },
  'baz',
  { quux: true },
); // 'foo bar baz quux'

```

## ignoring false inputs

```javascript

classNames(null, false, 'bar', undefined, { baz: null }, ''); // 'bar'

```


### Skeleton Code

```javascript
/**
 * @param {...(any|Object|Array<any|Object|Array>)} args
 * @return {string}
 */
export default function classNames(...args) {
  throw 'Not implemented!';
}
}


```


