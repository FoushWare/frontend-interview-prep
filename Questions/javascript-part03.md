# DOM Interview Questions

Comprehensive DOM interview preparation for frontend engineers.

Focus areas:

* DOM fundamentals
* DOM manipulation
* DOM traversal
* Events
* Event bubbling
* Capturing
* Event delegation
* Performance
* Browser rendering
* Senior-level DOM questions

---

# 1. What is DOM?

DOM stands for:

**Document Object Model**

The DOM is a tree-like representation of HTML.

Browser converts HTML into objects JavaScript can interact with.

Example HTML:

```html
<body>
  <div>
    <button>Click</button>
  </div>
</body>
```

DOM tree:

```txt
Document
 └── body
      └── div
           └── button
```

---

## Why DOM Matters

JavaScript uses DOM to:

* Read content
* Update UI
* Add/remove elements
* Listen to events
* Change styles

---

## Interview Questions

### Junior

1. What is DOM?
2. Why do we need DOM?

### Mid-Level

1. How browser creates DOM?
2. Difference between DOM and HTML?

### Senior

1. How DOM updates affect performance?
2. Explain render tree.

---

# 2. Selecting Elements

---

## getElementById()

Find by ID.

```js
const title =
  document.getElementById(
    "title"
  );
```

---

## getElementsByClassName()

Returns:

```txt
HTMLCollection
```

Example:

```js
document.getElementsByClassName(
  "card"
);
```

---

## getElementsByTagName()

```js
document.getElementsByTagName(
  "div"
);
```

---

## querySelector()

Returns first match.

```js
document.querySelector(
  ".card"
);
```

---

## querySelectorAll()

Returns:

```txt
NodeList
```

Example:

```js
document.querySelectorAll(
  ".card"
);
```

---

## HTMLCollection vs NodeList

### HTMLCollection

Live collection.

Auto updates.

---

### NodeList

Static.

---

## Interview Questions

1. querySelector vs querySelectorAll?
2. HTMLCollection vs NodeList?
3. Why prefer querySelector?

---

# 3. DOM Manipulation

---

## Change Text

### textContent

Safe text.

```js
element.textContent =
  "Hello";
```

---

### innerHTML

Inject HTML.

```js
element.innerHTML =
  "<strong>Hello</strong>";
```

Danger:

```txt
XSS risk
```

---

## Change Attribute

```js
element.setAttribute(
  "disabled",
  true
);
```

---

## classList

### add

```js
element.classList.add(
  "active"
);
```

---

### remove

```js
element.classList.remove(
  "active"
);
```

---

### toggle

```js
element.classList.toggle(
  "dark"
);
```

---

### contains

```js
element.classList.contains(
  "active"
);
```

---

## Styling

Bad:

```js
element.style.color =
  "red";
```

Better:

```js
element.classList.add(
  "error"
);
```

---

## Interview Questions

### Junior

1. Difference `innerHTML` vs `textContent`?
2. Why classList useful?

### Mid-Level

1. Security concerns with innerHTML?

### Senior

1. DOM manipulation performance concerns?

---

## Tricky Question

```js
div.innerHTML +=
  "<p>Hello</p>";
```

Problem:

Can trigger unnecessary DOM recreation.

---

# 4. Creating Elements

---

## createElement()

```js
const div =
  document.createElement(
    "div"
  );
```

---

## Append Child

```js
document.body.appendChild(
  div
);
```

---

## append()

Can add multiple.

```js
container.append(
  div1,
  div2
);
```

---

## prepend()

Adds to beginning.

---

## remove()

```js
element.remove();
```

---

## replaceChild()

Replace element.

---

## Interview Questions

1. createElement vs innerHTML?
2. append vs appendChild?

---

# 5. DOM Traversal

Move through DOM tree.

---

## Parent

```js
element.parentElement;
```

---

## Children

```js
element.children;
```

---

## First Child

```js
element.firstElementChild;
```

---

## Last Child

```js
element.lastElementChild;
```

---

## Next Sibling

```js
element.nextElementSibling;
```

---

## Previous Sibling

```js
element.previousElementSibling;
```

---

## closest()

Very useful.

Find nearest parent.

```js
button.closest(
  ".card"
);
```

---

## Interview Questions

1. parentNode vs parentElement?
2. children vs childNodes?
3. Why closest useful?

---

# 6. Events

Events allow interaction.

Examples:

```txt
click
submit
input
change
keydown
keyup
mouseover
```

---

## addEventListener()

Best approach.

```js
button.addEventListener(
  "click",
  () => {
    console.log("clicked");
  }
);
```

---

## Event Object

```js
button.addEventListener(
  "click",
  (event) => {
    console.log(event);
  }
);
```

---

## Important Event Properties

### target

Clicked element.

```js
event.target;
```

---

### currentTarget

Attached element.

---

## preventDefault()

Stops default behavior.

Example:

```js
form.addEventListener(
  "submit",
  (e) => {
    e.preventDefault();
  }
);
```

---

## stopPropagation()

Stops bubbling.

---

## Interview Questions

### Junior

1. What is addEventListener?
2. preventDefault purpose?

### Mid-Level

1. target vs currentTarget?

### Senior

1. Event system internals?

---

# 7. Event Bubbling

Default behavior.

Event goes:

```txt
child → parent → root
```

Example:

```html
<div id="parent">
  <button id="child">
    Click
  </button>
</div>
```

---

Example:

```js
parent.addEventListener(
  "click",
  () => {
    console.log("parent");
  }
);

child.addEventListener(
  "click",
  () => {
    console.log("child");
  }
);
```

Output:

```txt
child
parent
```

---

## Interview Questions

1. What is event bubbling?
2. Why useful?

---

# 8. Event Capturing

Opposite direction.

```txt
root → child
```

Enable:

```js
addEventListener(
  "click",
  handler,
  true
);
```

---

## Interview Questions

1. Bubbling vs capturing?
2. When use capture?

---

# 9. Event Delegation

Very important interview topic.

Attach one listener to parent.

Instead of many listeners.

Bad:

```js
buttons.forEach((btn) => {
  btn.addEventListener(
    "click",
    handler
  );
});
```

Better:

```js
container.addEventListener(
  "click",
  (event) => {
    if (
      event.target.matches(
        ".btn"
      )
    ) {
      console.log("clicked");
    }
  }
);
```

---

## Benefits

* Better performance
* Handles dynamic elements
* Cleaner code

---

## Real Example

Todo list.

New items still work.

---

## Interview Questions

### Junior

1. What is event delegation?

### Mid-Level

1. Why delegation improves performance?

### Senior

1. Delegation edge cases?

---

# 10. DOM Performance

DOM manipulation expensive.

Avoid:

```txt
reflow
repaint
layout thrashing
```

---

## Bad Example

Repeated DOM update.

```js
for (
  let i = 0;
  i < 1000;
  i++
) {
  list.innerHTML +=
    "<li>Item</li>";
}
```

---

## Better

Use:

```txt
DocumentFragment
```

Example:

```js
const fragment =
  document.createDocumentFragment();

for (
  let i = 0;
  i < 1000;
  i++
) {
  const li =
    document.createElement(
      "li"
    );

  fragment.appendChild(li);
}

list.appendChild(fragment);
```

---

## Reflow vs Repaint

### Reflow

Layout recalculation.

Expensive.

Triggered by:

```txt
width
height
position
font-size
```

---

### Repaint

Visual update only.

Less expensive.

Triggered by:

```txt
background
color
visibility
```

---

## Interview Questions

1. Reflow vs repaint?
2. How optimize DOM performance?

---

# 11. Browser Rendering

Steps:

1. Parse HTML
2. Build DOM
3. Parse CSS
4. Build CSSOM
5. Render Tree
6. Layout
7. Paint
8. Composite

---

## Render Blocking

Examples:

```txt
CSS
sync scripts
```

---

## Interview Questions

1. Critical rendering path?
2. Why CSS blocks render?

---

# 12. Mutation Observer

Observe DOM changes.

Example:

```js
const observer =
  new MutationObserver(
    (mutations) => {
      console.log(
        mutations
      );
    }
  );

observer.observe(
  document.body,
  {
    childList: true,
  }
);
```

---

## Interview Questions

1. What is MutationObserver?
2. Real-world use case?

---

# 13. Memory Leaks in DOM

Common causes:

### Event listeners not removed

Bad:

```js
element.addEventListener(
  "click",
  handler
);
```

Without cleanup.

---

### Detached DOM nodes

Element removed but referenced.

---

### Timers

Forgot cleanup.

---

## React Example

```js
useEffect(() => {
  window.addEventListener(
    "resize",
    resize
  );

  return () => {
    window.removeEventListener(
      "resize",
      resize
    );
  };
}, []);
```

---

## Interview Questions

1. Memory leak examples?
2. How debug memory leaks?

---

# Tricky Questions

### Question

```js
event.target
```

vs

```js
event.currentTarget
```

Difference?

---

### Question

```js
document.querySelectorAll(
  "div"
);
```

Returns:

```txt
NodeList
```

---

### Question

Why event delegation works?

Because bubbling.

---

# Practical Exercises

## Exercise 1

Create modal.

Requirements:

* open
* close
* escape key

---

## Exercise 2

Build todo list using delegation.

---

## Exercise 3

Create dropdown menu.

---

## Exercise 4

Explain output:

```js
button.addEventListener(
  "click",
  (event) => {
    console.log(
      event.target
    );
  }
);
```

---

# Senior-Level Questions

1. Explain browser rendering deeply.
2. DOM optimization techniques?
3. Reflow vs repaint?
4. Event delegation internals?
5. Why virtual DOM exists?
6. Browser event system?
7. How React synthetic events work?

---

# Most Important DOM Topics

Priority:

1. Event delegation
2. Bubbling/capturing
3. DOM manipulation
4. querySelector
5. Traversal
6. Performance
7. Rendering
8. Memory leaks
