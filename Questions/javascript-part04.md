# Runtime APIs Interview Questions

Comprehensive Runtime APIs interview preparation for frontend engineers.

Focus areas:

* Browser Runtime APIs
* `fetch()`
* Storage APIs
* Timers
* Event Loop relation
* AbortController
* Browser APIs
* Performance
* Security
* Senior-Level Questions

---

# 1. What Are Runtime APIs?

Runtime APIs are browser-provided APIs available through JavaScript.

JavaScript itself does **not** provide:

```txt
fetch
setTimeout
DOM
localStorage
```

These come from:

```txt
Browser Runtime Environment
```

Example:

```js
console.log(window);
```

Browser APIs live on:

```txt
window
```

---

## Common Runtime APIs

```txt
DOM APIs
Fetch API
Storage APIs
Timers
History API
Navigator API
Geolocation API
Clipboard API
WebSocket
IntersectionObserver
ResizeObserver
```

---

## Interview Questions

### Junior

1. What are browser APIs?
2. Is `fetch()` part of JavaScript?

### Mid-Level

1. How browser APIs interact with JS?

### Senior

1. How Web APIs work with Event Loop?

---

# 2. Fetch API

Used for HTTP requests.

Example:

```js
async function getUsers() {
  const response =
    await fetch("/users");

  const data =
    await response.json();

  return data;
}
```

---

## Request Lifecycle

```txt
Request
→ Browser
→ Server
→ Response
→ JSON parse
→ UI update
```

---

## HTTP Methods

### GET

Fetch data.

```js
fetch("/users");
```

---

### POST

Create resource.

```js
fetch("/users", {
  method: "POST",
});
```

---

### PUT

Replace resource.

---

### PATCH

Partial update.

---

### DELETE

Delete resource.

---

## Headers

Example:

```js
fetch("/users", {
  headers: {
    Authorization:
      "Bearer token",
  },
});
```

---

## JSON Body

```js
fetch("/users", {
  method: "POST",

  headers: {
    "Content-Type":
      "application/json",
  },

  body: JSON.stringify({
    name: "Ahmed",
  }),
});
```

---

## response.ok

Important:

```js
if (!response.ok) {
  throw new Error(
    "Request failed"
  );
}
```

Because fetch only rejects for:

```txt
Network failures
```

Not:

```txt
404
500
```

---

## Interview Questions

### Junior

1. What is fetch?
2. GET vs POST?

### Mid-Level

1. Why check `response.ok`?
2. Why stringify request body?

### Senior

1. Retry strategy for failed requests?
2. How handle race conditions?

---

## Tricky Question

```js
fetch("/users")
  .then((res) => {
    console.log(res);
  });
```

Does this contain JSON?

No.

Need:

```js
res.json()
```

---

# 3. AbortController

Cancels requests.

Very important for React.

Example:

```js
const controller =
  new AbortController();

fetch("/users", {
  signal:
    controller.signal,
});

controller.abort();
```

---

## React Example

Avoid stale requests.

```js
useEffect(() => {
  const controller =
    new AbortController();

  fetch("/users", {
    signal:
      controller.signal,
  });

  return () => {
    controller.abort();
  };
}, []);
```

---

## Why Important?

Prevents:

```txt
Memory leaks
Race conditions
Unnecessary requests
```

---

## Interview Questions

1. What is AbortController?
2. Why useful in React?

---

# 4. Storage APIs

Browser storage.

Types:

```txt
localStorage
sessionStorage
cookies
```

---

# 5. localStorage

Persistent storage.

Data survives refresh.

Example:

```js
localStorage.setItem(
  "theme",
  "dark"
);
```

Read:

```js
localStorage.getItem(
  "theme"
);
```

Delete:

```js
localStorage.removeItem(
  "theme"
);
```

Clear:

```js
localStorage.clear();
```

---

## Important

Stores:

```txt
strings only
```

Objects require:

```js
JSON.stringify()
JSON.parse()
```

Example:

```js
localStorage.setItem(
  "user",
  JSON.stringify(user)
);
```

---

## Interview Questions

### Junior

1. What is localStorage?

### Mid-Level

1. Why stringify objects?

### Senior

1. Security concerns?

---

## Security Warning

Never store:

```txt
JWT tokens
passwords
sensitive data
```

Because vulnerable to:

```txt
XSS
```

---

# 6. sessionStorage

Temporary storage.

Dies when tab closes.

Example:

```js
sessionStorage.setItem(
  "step",
  "2"
);
```

---

## localStorage vs sessionStorage

### localStorage

Persistent.

---

### sessionStorage

Per tab.

Temporary.

---

## Interview Questions

1. localStorage vs sessionStorage?
2. When use sessionStorage?

---

# 7. Cookies

Small browser storage.

Automatically sent to server.

Example:

```js
document.cookie =
  "theme=dark";
```

---

## Why Cookies?

Authentication.

---

## Cookie Problems

Small size.

Sent on every request.

---

## Secure Cookies

Important flags:

```txt
HttpOnly
Secure
SameSite
```

---

## Interview Questions

1. Cookies vs localStorage?
2. Why HttpOnly important?

---

# 8. Timers

Browser timer APIs.

---

## setTimeout()

Runs once.

Example:

```js
setTimeout(() => {
  console.log("Hi");
}, 1000);
```

---

## clearTimeout()

Stops timeout.

```js
clearTimeout(id);
```

---

## setInterval()

Repeats.

```js
setInterval(() => {
  console.log("tick");
}, 1000);
```

---

## clearInterval()

Stops interval.

---

## Interview Questions

### Junior

1. Difference timeout vs interval?

### Mid-Level

1. Why timeout 0 delayed?

### Senior

1. Timer drift issues?

---

## Tricky Question

```js
setTimeout(() => {
  console.log("A");
}, 0);
```

Immediate?

No.

Waits for stack empty.

---

# 9. requestAnimationFrame

Better animation timing.

Example:

```js
requestAnimationFrame(
  animate
);
```

Better than:

```txt
setInterval
```

For animation.

Because synced with repaint.

---

## Interview Questions

1. Why requestAnimationFrame?
2. Why avoid setInterval for animation?

---

# 10. Navigator API

Browser/device info.

Example:

```js
navigator.userAgent;
```

---

## Online Status

```js
navigator.onLine;
```

---

## Clipboard API

Copy text.

```js
navigator.clipboard.writeText(
  "Hello"
);
```

---

## Interview Questions

1. Clipboard API use case?
2. navigator purpose?

---

# 11. Geolocation API

Get user location.

Example:

```js
navigator.geolocation.getCurrentPosition(
  (position) => {
    console.log(
      position
    );
  }
);
```

Requires permission.

---

## Interview Questions

1. Why permission required?
2. Geolocation limitations?

---

# 12. IntersectionObserver

Very common interview topic.

Observe visibility.

Example:

```js
const observer =
  new IntersectionObserver(
    (entries) => {
      console.log(entries);
    }
  );

observer.observe(
  element
);
```

---

## Use Cases

```txt
Lazy loading
Infinite scroll
Analytics
Animations
```

---

## Why Better?

Avoid expensive:

```txt
scroll event listeners
```

---

## Interview Questions

1. Why use IntersectionObserver?
2. Infinite scroll implementation?

---

# 13. ResizeObserver

Watch size changes.

Example:

```js
const observer =
  new ResizeObserver(
    (entries) => {
      console.log(entries);
    }
  );
```

---

## Use Cases

Responsive charts.

Dynamic UI.

---

# 14. History API

Single Page Apps.

Navigate without reload.

Example:

```js
history.pushState(
  {},
  "",
  "/profile"
);
```

Back:

```js
history.back();
```

---

## React Relation

Used by routers.

---

## Interview Questions

1. Why History API important?
2. How SPA routing works?

---

# 15. WebSocket

Real-time communication.

Example:

```js
const socket =
  new WebSocket(
    "ws://example"
  );
```

---

## Use Cases

```txt
chat
notifications
stock prices
gaming
```

---

## HTTP vs WebSocket

### HTTP

Request-response.

---

### WebSocket

Persistent connection.

---

## Interview Questions

1. WebSocket vs HTTP?
2. Real-time use case?

---

# 16. Event Loop + Runtime APIs

Example:

```js
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");
```

Output:

```txt
1
4
3
2
```

Why?

```txt
microtask > macrotask
```

---

# Common Runtime Mistakes

### Forgetting cleanup

Bad:

```js
setInterval(() => {
  console.log("tick");
}, 1000);
```

Without:

```js
clearInterval()
```

---

### Storing objects directly

Wrong:

```js
localStorage.setItem(
  "user",
  user
);
```

---

### Ignoring fetch errors

Bad:

```js
fetch("/api");
```

Without handling.

---

# Practical Exercises

## Exercise 1

Create fetch wrapper.

Requirements:

* try/catch
* response.ok
* reusable

---

## Exercise 2

Implement theme persistence.

Requirements:

* localStorage
* dark/light

---

## Exercise 3

Debounced search request.

---

## Exercise 4

Cancel request using:

```txt
AbortController
```

---

## Exercise 5

Infinite scroll using:

```txt
IntersectionObserver
```

---

# Senior-Level Questions

1. How browser APIs work?
2. Event loop internals?
3. localStorage security risks?
4. requestAnimationFrame internals?
5. How SPA navigation works?
6. How retry strategy works for APIs?
7. Polling vs WebSocket?
8. How avoid race conditions in React?

---

# Most Important Runtime Topics

Priority:

1. Fetch
2. localStorage/sessionStorage
3. Timers
4. AbortController
5. Event loop
6. IntersectionObserver
7. WebSocket
8. History API
