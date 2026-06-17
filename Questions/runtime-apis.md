# Runtime APIs Interview Questions

## 1. What is fetch()?

### Answer
`fetch()` is a modern browser API used to make HTTP requests. It returns a Promise.

### Example

```js
fetch("/api/users")
  .then(res => res.json())
  .then(data => console.log(data));
```

---

## 2. Fetch vs Axios

### Answer

| Feature | Fetch | Axios |
|----------|--------|--------|
| Built into browser | ✅ | ❌ |
| JSON parsing | Manual | Automatic |
| Interceptors | ❌ | ✅ |
| Timeout support | ❌ | ✅ |

### Interview Answer
Fetch is native and lightweight. Axios provides additional features like interceptors, automatic JSON transformation, and request cancellation.

---

## 3. localStorage vs sessionStorage

### Answer

| Feature | localStorage | sessionStorage |
|----------|--------------|----------------|
| Persistence | Until cleared | Until tab closes |
| Shared across tabs | Yes | No |
| Storage limit | ~5MB | ~5MB |

---

## 4. What is AbortController?

### Answer
AbortController allows cancellation of asynchronous operations such as fetch requests.

### Example

```js
const controller = new AbortController();

fetch("/users", {
  signal: controller.signal,
});

controller.abort();
```

---

## 5. setTimeout vs setInterval

### Answer

| setTimeout | setInterval |
|------------|------------|
| Runs once | Runs repeatedly |
| Better control | Automatic repetition |

### Example

```js
setTimeout(() => {
  console.log("Executed once");
}, 1000);
```

```js
setInterval(() => {
  console.log("Repeated");
}, 1000);
```
