
# React Interview Questions

## 1. Why React?

### Answer
React simplifies building interactive user interfaces through reusable components, declarative rendering, and efficient updates using the Virtual DOM.

---

## 2. What is the Virtual DOM?

### Answer
The Virtual DOM is a lightweight JavaScript representation of the real DOM.

React compares the previous Virtual DOM with the new Virtual DOM and updates only the changed parts.

### Benefits
- Faster updates
- Better performance
- Simplified UI development

---

## 3. What is the difference between state and props?

### Answer

| State | Props |
|---------|---------|
| Managed inside component | Passed from parent |
| Mutable | Read-only |
| Causes re-render | Causes re-render |

---

## 4. What is useMemo?

### Answer
`useMemo` memoizes a calculated value and recomputes it only when dependencies change.

### Example

```js
const expensiveValue = useMemo(() => {
  return calculate(items);
}, [items]);
```

---

## 5. What is useCallback?

### Answer
`useCallback` memoizes a function reference.

### Example

```js
const handleClick = useCallback(() => {
  console.log("clicked");
}, []);
```

---

## 6. useMemo vs useCallback

### Answer

| useMemo | useCallback |
|-----------|------------|
| Memoizes values | Memoizes functions |
| Returns result | Returns function |

---

## 7. Controlled vs Uncontrolled Components

### Controlled

```jsx
<input
  value={value}
  onChange={(e) => setValue(e.target.value)}
/>
```

State controls input.

### Uncontrolled

```jsx
<input ref={inputRef} />
```

DOM controls input.

### Interview Answer
Controlled components provide better validation and predictability. Uncontrolled components are simpler for small forms.
