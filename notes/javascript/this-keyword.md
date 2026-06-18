# The this Keyword

## Definition

`this` refers to the object that is calling the function.

---

## Example

```js
const person = {
  name: "Ahmed",

  sayHello() {
    console.log(this.name);
  },
};

person.sayHello();
```

Output:

```text
Ahmed
```

---

## Why?

Because:

```js
this === person
```

---

## Losing this

```js
const person = {
  name: "Ahmed",

  sayHello() {
    console.log(this.name);
  },
};

const fn = person.sayHello;

fn();
```

Output:

```text
undefined
```

Because:

```js
this !== person
```

anymore.

---

## call

```js
fn.call(person);
```

Output:

```text
Ahmed
```

---

## apply

```js
fn.apply(person);
```

Output:

```text
Ahmed
```

---

## Debounce Example

```js
return function (...args) {
  const context = this;

  setTimeout(() => {
    func.apply(context, args);
  }, wait);
};
```

This preserves the original `this`.

---

## Interview Question

### Why does debounce use apply?

Because the callback may depend on `this`, and we want to preserve the calling context.

---

## Revision Notes

Remember:

* this depends on how a function is called.
* apply allows us to control this.
* Debounce often preserves this.
