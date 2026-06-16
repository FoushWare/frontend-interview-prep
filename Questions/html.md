# HTML Interview Questions

---

# 1. What is HTML?

HTML (**HyperText Markup Language**) is the standard markup language used to structure web pages.

HTML defines:

* Structure
* Content
* Meaning (semantics)

Example:

```html
<h1>Hello World</h1>
<p>This is a paragraph</p>
```

HTML is **not a programming language**.

It does not contain:

* Loops
* Variables
* Conditions

It describes content structure.

---

# 2. HTML Document Structure

Basic structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
  />
  <title>Document</title>
</head>

<body>
  <h1>Hello</h1>
</body>
</html>
```

---

## Interview Questions

### Junior

1. What is HTML?
2. Why use `DOCTYPE`?
3. What is `<head>`?
4. What is `<body>`?

### Mid-Level

1. What happens if `DOCTYPE` is missing?
2. Explain browser rendering process.

### Senior

1. How does browser parse HTML?
2. What blocks rendering?

---

# 3. Semantic HTML

Semantic HTML gives meaning to content.

Bad:

```html
<div class="header"></div>
<div class="content"></div>
<div class="footer"></div>
```

Good:

```html
<header></header>
<main></main>
<footer></footer>
```

Common semantic tags:

```html
<header>
<nav>
<main>
<section>
<article>
<aside>
<footer>
```

---

## Why Semantic HTML Matters

### 1. Accessibility

Screen readers understand structure.

### 2. SEO

Search engines understand content better.

### 3. Maintainability

Cleaner code.

---

## Important Differences

### `section` vs `div`

`section`

* semantic
* grouped content

`div`

* generic container

---

### `article` vs `section`

`article`

* independent reusable content

Example:

* blog post
* news card

`section`

* grouped topic

---

## Interview Questions

### Junior

1. What is semantic HTML?
2. Why not use div everywhere?

### Mid-Level

1. Difference between article and section?
2. Why does semantic HTML matter?

### Senior

1. How does semantic HTML affect accessibility?

---

# 4. Block vs Inline Elements

## Block Elements

Take full width.

Examples:

```html
<div>
<p>
<section>
<h1>
```

---

## Inline Elements

Take only needed width.

Examples:

```html
<span>
<a>
<strong>
```

---

## Interview Questions

1. Difference between block and inline?
2. Can inline elements have width?
3. Difference between `span` and `div`?

---

# 5. Head Tag

Contains metadata.

```html
<head>
  <title>My Website</title>

  <meta charset="UTF-8" />

  <meta
    name="description"
    content="Frontend interview prep"
  />

  <link rel="stylesheet" href="style.css" />

  <script src="app.js"></script>
</head>
```

---

## Important Tags

### title

Page title.

### meta

Metadata.

### link

External files.

### script

JavaScript.

### style

Internal CSS.

---

## Interview Questions

1. Purpose of `<head>`?
2. Difference between script and link?
3. Why viewport meta tag?

---

# 6. Script Loading

Bad:

```html
<script src="app.js"></script>
```

Better:

```html
<script defer src="app.js"></script>
```

---

## async vs defer

### async

* downloads in parallel
* executes immediately

Execution order ❌ not guaranteed

---

### defer

* downloads in parallel
* executes after HTML parsed

Execution order ✅ guaranteed

---

## Interview Questions

1. Difference between async and defer?
2. Why place script at bottom?
3. When to use async?

---

# 7. Forms

Example:

```html
<form action="/submit" method="POST">
  <input
    type="email"
    required
  />

  <button type="submit">
    Submit
  </button>
</form>
```

---

## GET vs POST

### GET

* visible in URL
* for fetching data

### POST

* secure
* send data

---

## Form Submission Flow

1. User clicks submit
2. Browser validates
3. Request sent

---

## Interview Questions

1. Difference GET vs POST?
2. What happens on submit?
3. What does preventDefault do?

---

# 8. Inputs

Types:

```html
text
password
email
number
checkbox
radio
date
file
```

---

## Interview Questions

1. Difference radio vs checkbox?
2. Why use type email?
3. What input types exist?

---

# 9. Form Validation

HTML validation:

```html
<input required />
<input minlength="3" />
<input pattern="[A-Za-z]+" />
```

---

## Validation Attributes

* required
* minlength
* maxlength
* min
* max
* pattern

---

## Interview Questions

1. Client-side vs server-side validation?
2. Why server validation still needed?

---

# 10. Accessibility (A11Y)

Bad:

```html
<div onclick="submit()">
Submit
</div>
```

Good:

```html
<button>
Submit
</button>
```

---

## Best Practices

* Use labels

```html
<label for="email">
Email
</label>

<input id="email" />
```

* Alt text

```html
<img alt="User profile" />
```

---

## Interview Questions

1. What is accessibility?
2. Why labels matter?
3. Why semantic HTML helps screen readers?

---

# 11. SEO Basics

Important:

* Semantic HTML
* Meta description
* Title tags
* Alt text

---

## Interview Questions

1. How improve SEO?
2. Why title important?

---

# Tricky Questions

### What happens if multiple elements have same id?

Invalid HTML.

JS may behave unexpectedly.

---

### Difference between disabled and readonly?

`disabled`

* cannot interact
* not submitted

`readonly`

* submitted
* cannot edit

---

# Practical Exercises

## Exercise 1

Create a semantic blog page.

Use:

* header
* nav
* main
* article
* footer

---

## Exercise 2

Build login form with validation.

Requirements:

* email
* password
* required
* minlength

---

## Exercise 3

Explain:

```html
<script async src="a.js"></script>
<script defer src="b.js"></script>
```

What execution order happens?

---

# Senior-Level Questions

1. Explain browser rendering pipeline.
2. Critical rendering path?
3. How browser parses HTML?
4. Render blocking resources?
5. Accessibility best practices?
