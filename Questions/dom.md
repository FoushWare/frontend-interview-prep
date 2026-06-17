# DOM Interview Questions

## 1. What is the DOM?

### Answer
The DOM (Document Object Model) is a programming interface for HTML and XML documents. It represents the page as a tree of objects that JavaScript can access and manipulate.

### Example

```html
<h1 id="title">Hello</h1>

<script>
const heading = document.getElementById("title");
heading.textContent = "Welcome";
</script>
```

---

## 2. What is the difference between children and childNodes?

### Answer
- `children` returns only element nodes.
- `childNodes` returns all node types including text nodes, comments, and elements.

### Example

```html
<div id="box">
  <p>Text</p>
</div>
```

```js
box.children; // [p]
box.childNodes; // [text, p, text]
```

---

## 3. What is event bubbling?

### Answer
Event bubbling is the process where an event starts from the target element and propagates upward through its ancestors.

### Example

```html
<div id="parent">
  <button id="child">Click</button>
</div>
```

```js
parent.addEventListener("click", () => console.log("parent"));
child.addEventListener("click", () => console.log("child"));
```

Output:

```
child
parent
```

---

## 4. What is event delegation?

### Answer
Event delegation is a technique where a parent element handles events for its child elements using event bubbling.

### Benefits
- Better performance
- Fewer event listeners
- Works with dynamically added elements

### Example

```js
document.getElementById("list").addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    console.log(e.target.textContent);
  }
});
```

---

## 5. Difference between preventDefault() and stopPropagation()?

### Answer

| Method | Purpose |
|----------|----------|
| preventDefault() | Prevents browser default behavior |
| stopPropagation() | Prevents event bubbling/capturing |

### Example

```js
event.preventDefault();
```

Prevents form submission.

```js
event.stopPropagation();
```

Prevents parent handlers from running.
