
```javascript
export default function classNames(...args) {
  const classes = [];

  for (const arg of args) {
    // Skip all falsy values immediately (null, undefined, false, "", etc.)
    if (!arg) continue;

    const argType = typeof arg;

    // Case 1: Strings or Numbers
    if (argType === 'string' || argType === 'number') {
      classes.push(arg);
    } 
    
    // Case 2: Arrays (Use recursion to unpack elements cleanly!)
    else if (Array.isArray(arg)) {
      const innerResult = classNames(...arg);
      if (innerResult) {
        classes.push(innerResult);
      }
    } 
    
    // Case 3: Objects
    else if (argType === 'object') {
      for (const key in arg) {
        // Protect the loop using the hasOwnProperty pattern we mastered!
        if (Object.prototype.hasOwnProperty.call(arg, key) && arg[key]) {
          classes.push(key);
        }
      }
    }
  }

  // Combine everything with single spaces safely
  return classes.join(' ');
}

```
