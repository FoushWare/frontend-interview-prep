# HTML Interview Questions & Answers

## 1. What is HTML?

### Answer

HTML (HyperText Markup Language) is the standard markup language used to structure content on web pages.

It defines:

* Structure
* Content
* Meaning (semantics)

HTML is not a programming language because it does not contain logic such as loops, conditions, or functions.

Example:

```html
<h1>Hello World</h1>
<p>This is a paragraph</p>
```

---

## 2. Why do we use DOCTYPE?

### Answer

`<!DOCTYPE html>` tells the browser to render the page using modern HTML standards.

Without it, browsers may enter **Quirks Mode**, where they emulate older browser behavior and may render layouts inconsistently.

Example:

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Hello</h1>
  </body>
</html>
```

---

## 3. What is the purpose of the `<head>` tag?

### Answer

The `<head>` contains metadata about the document that is not displayed directly on the page.

Common elements inside `<head>`:

* title
* meta tags
* stylesheets
* scripts

Example:

```html
<head>
  <title>My Website</title>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="styles.css">
</head>
```

---

## 4. What is the difference between `<head>` and `<body>`?

### Answer

| Head                        | Body                         |
| --------------------------- | ---------------------------- |
| Contains metadata           | Contains visible content     |
| Not displayed               | Displayed to users           |
| Contains title, meta, links | Contains text, images, forms |

---

## 5. What is Semantic HTML?

### Answer

Semantic HTML uses elements that describe the meaning of the content.

Examples:

```html
<header>
<nav>
<main>
<section>
<article>
<footer>
```

Instead of:

```html
<div class="header">
<div class="content">
<div class="footer">
```

Benefits:

* Better accessibility
* Better SEO
* Easier maintenance

---

## 6. Why not use div everywhere?

### Answer

Using only divs makes the page structure unclear.

Semantic elements provide meaning to:

* Browsers
* Search engines
* Screen readers

Example:

```html
<header>
  <nav></nav>
</header>

<main>
  <article></article>
</main>
```

This structure is much easier to understand than nested divs.

---

## 7. Difference between section and article?

### Answer

### section

Represents a thematic grouping of content.

Example:

```html
<section>
  <h2>Contact Information</h2>
</section>
```

### article

Represents independent content that can stand alone.

Example:

```html
<article>
  <h2>News Article</h2>
  <p>Content...</p>
</article>
```

Examples of articles:

* Blog posts
* News articles
* Product cards

---

## 8. Difference between block and inline elements?

### Answer

### Block Elements

Take full available width.

Examples:

```html
<div>
<p>
<section>
<h1>
```

### Inline Elements

Take only the width they need.

Examples:

```html
<span>
<a>
<strong>
```

---

## 9. Difference between span and div?

### Answer

| div                      | span                  |
| ------------------------ | --------------------- |
| Block element            | Inline element        |
| Starts on new line       | Stays in same line    |
| Used for layout/grouping | Used for styling text |

Example:

```html
<div>Container</div>

<span>Inline text</span>
```

---

## 10. What is the viewport meta tag?

### Answer

The viewport meta tag controls how the page is displayed on mobile devices.

Example:

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0"
/>
```

Without it, mobile browsers may render the page at desktop width and scale it down.

---

## 11. Difference between async and defer?

### Answer

### async

* Downloads script in parallel
* Executes immediately after download
* Execution order is not guaranteed

```html
<script async src="analytics.js"></script>
```

### defer

* Downloads script in parallel
* Executes after HTML parsing
* Execution order is preserved

```html
<script defer src="app.js"></script>
```

### Interview Answer

Use `defer` for application scripts that depend on DOM structure.

Use `async` for independent scripts like analytics and ads.

---

## 12. Difference between GET and POST?

### Answer

### GET

* Retrieves data
* Parameters appear in URL
* Can be cached
* Should not modify data

Example:

```http
GET /users?id=1
```

### POST

* Sends data to server
* Data is in request body
* Used for create/update operations

Example:

```http
POST /users
```

---

## 13. What happens when a form is submitted?

### Answer

Browser process:

1. User clicks submit button
2. HTML validation runs
3. Form data collected
4. Request sent to server
5. Page reloads (unless prevented)

Example:

```html
<form action="/login" method="POST">
```

---

## 14. What does preventDefault() do?

### Answer

It prevents the browser's default behavior.

Example:

```js
form.addEventListener("submit", (event) => {
  event.preventDefault();
});
```

This prevents page refresh during form submission.

---

## 15. Difference between disabled and readonly?

### Answer

### disabled

```html
<input disabled>
```

* Cannot be edited
* Cannot be focused
* Not submitted with form

### readonly

```html
<input readonly>
```

* Cannot be edited
* Can receive focus
* Included in form submission

---

## 16. What is Accessibility (A11Y)?

### Answer

Accessibility means making websites usable by everyone, including users with disabilities.

Examples:

* Semantic HTML
* Keyboard navigation
* Labels
* Alt text
* ARIA attributes

---

## 17. Why are labels important?

### Answer

Labels improve accessibility and usability.

Example:

```html
<label for="email">
  Email
</label>

<input id="email">
```

Benefits:

* Screen reader support
* Larger clickable area
* Better form usability

---

## 18. Why is alt text important?

### Answer

Alt text describes images for users who cannot see them.

Example:

```html
<img
  src="profile.jpg"
  alt="User profile picture"
/>
```

Benefits:

* Accessibility
* SEO
* Fallback when image fails to load

---

## 19. How does semantic HTML improve SEO?

### Answer

Semantic elements help search engines understand page structure.

Example:

```html
<header>
<main>
<article>
<footer>
```

Search engines can better identify:

* Main content
* Navigation
* Articles
* Page hierarchy

---

## 20. Explain the browser rendering pipeline.

### Answer

Steps:

1. Browser downloads HTML
2. HTML parsed into DOM
3. CSS parsed into CSSOM
4. DOM + CSSOM → Render Tree
5. Layout calculation
6. Paint pixels
7. Composite layers

Pipeline:

```
HTML
 ↓
DOM
 ↓
Render Tree
 ↓
Layout
 ↓
Paint
 ↓
Composite
```

This process is commonly called the Critical Rendering Path.
