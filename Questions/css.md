# CSS Interview Questions

A comprehensive guide to CSS interview preparation from Junior → Senior frontend engineer.

---

# 1. What is CSS?

CSS (**Cascading Style Sheets**) is used to style HTML elements.

CSS controls:

* Layout
* Spacing
* Colors
* Positioning
* Responsiveness
* Animations

Example:

```css
h1 {
  color: blue;
  font-size: 24px;
}
```

---

# 2. How CSS Works

Browser flow:

1. Parse HTML
2. Parse CSS
3. Create CSSOM
4. Combine DOM + CSSOM
5. Create render tree
6. Layout
7. Paint

---

## Interview Questions

### Junior

1. What is CSS?
2. Why separate CSS from HTML?

### Mid-Level

1. Explain browser rendering.
2. What blocks rendering?

### Senior

1. Difference between reflow and repaint?
2. How to optimize CSS rendering?

---

# 3. CSS Syntax

Example:

```css
.card {
  background: white;
  padding: 20px;
}
```

Structure:

```css
selector {
  property: value;
}
```

---

# 4. Selectors

## Basic Selectors

### Element Selector

```css
p {
  color: red;
}
```

---

### Class Selector

```css
.card {
  border-radius: 8px;
}
```

---

### ID Selector

```css
#header {
  background: black;
}
```

---

### Universal Selector

```css
* {
  margin: 0;
}
```

---

### Attribute Selector

```css
input[type="text"] {
  border: 1px solid gray;
}
```

---

## Combinators

### Descendant

```css
.container p {
}
```

---

### Child

```css
.container > p {
}
```

---

### Adjacent Sibling

```css
h1 + p {
}
```

---

### General Sibling

```css
h1 ~ p {
}
```

---

## Pseudo Classes

State-based styling.

```css
button:hover {
}

input:focus {
}

li:first-child {
}
```

---

## Pseudo Elements

```css
p::before {
  content: "";
}

p::after {
  content: "";
}
```

---

## Interview Questions

### Junior

1. Difference between class and id?
2. What are pseudo classes?

### Mid-Level

1. Difference between `>` and space selector?
2. Difference between pseudo class and pseudo element?

### Senior

1. Performance implications of complex selectors?

---

# 5. CSS Specificity

Determines which rule wins.

Priority:

```txt id="sc88g3"
Inline styles
ID selector
Class selector
Element selector
```

Example:

```css
#title {
  color: red;
}

.title {
  color: blue;
}
```

Result:

```txt id="ab97k1"
red
```

ID wins.

---

## Specificity Score

```txt id="t91gc5"
Inline = 1000
ID = 100
Class = 10
Element = 1
```

---

## !important

Avoid when possible.

Bad:

```css
color: red !important;
```

---

## Interview Questions

1. What is specificity?
2. Why avoid `!important`?
3. Which style wins?

Example:

```css
div {
  color: red;
}

.card {
  color: blue;
}

#main {
  color: green;
}
```

---

# 6. Box Model

Everything in CSS is a box.

Structure:

```txt id="yu1sdr"
Margin
Border
Padding
Content
```

Example:

```css
.card {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  margin: 10px;
}
```

---

## box-sizing

### content-box (default)

Width excludes padding/border.

### border-box

Width includes padding/border.

Recommended:

```css
* {
  box-sizing: border-box;
}
```

---

## Interview Questions

1. Explain box model.
2. Difference margin vs padding?
3. Why use border-box?

---

# 7. Display Property

## Block

Takes full width.

Examples:

```txt id="y9b8tm"
div
section
p
```

---

## Inline

Only needed width.

Examples:

```txt id="r8d1zm"
span
a
strong
```

---

## Inline-block

Inline but supports width/height.

---

## None

Hidden:

```css
display: none;
```

Removes element from layout.

---

## Visibility Hidden

```css
visibility: hidden;
```

Still occupies space.

---

## Interview Questions

1. Difference display none vs visibility hidden?
2. Difference inline vs inline-block?

---

# 8. Positioning

## Static

Default position.

---

## Relative

Moves relative to itself.

```css
.card {
  position: relative;
  top: 20px;
}
```

---

## Absolute

Relative to nearest positioned parent.

```css
.child {
  position: absolute;
}
```

---

## Fixed

Relative to viewport.

Sticky navbar example.

---

## Sticky

Behaves relative until scroll threshold.

```css
header {
  position: sticky;
  top: 0;
}
```

---

## z-index

Controls stacking order.

Requires positioned element.

---

## Interview Questions

### Junior

1. Difference relative vs absolute?

### Mid-Level

1. Why z-index not working?

### Senior

1. Explain stacking context.

---

# 9. Units

## Absolute

### px

Fixed size.

---

## Relative

### %

Relative to parent.

### em

Relative to parent font size.

### rem

Relative to root font size.

### vw

Viewport width.

### vh

Viewport height.

---

## Best Practice

Prefer:

```txt id="jv2mqt"
rem
%
vw
vh
```

For responsive design.

---

## Interview Questions

1. Difference em vs rem?
2. Why avoid px sometimes?

---

# 10. Flexbox

One-dimensional layout system.

---

## Container

```css
.container {
  display: flex;
}
```

---

## Direction

```css
flex-direction: row;
flex-direction: column;
```

---

## Alignment

### justify-content

Main axis.

```css
justify-content: center;
```

---

### align-items

Cross axis.

```css
align-items: center;
```

---

## Centering Example

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

## Flex Grow

```css
flex-grow: 1;
```

Expands available space.

---

## Interview Questions

### Junior

1. What is Flexbox?

### Mid-Level

1. Difference justify-content vs align-items?

### Senior

1. Flexbox performance concerns?

---

# 11. CSS Grid

Two-dimensional layout.

Example:

```css
.container {
  display: grid;

  grid-template-columns:
    repeat(3, 1fr);

  gap: 20px;
}
```

---

## fr Unit

Fractional unit.

Example:

```css
1fr 2fr
```

---

## Grid Areas

```css
grid-template-areas:
  "header header"
  "sidebar content";
```

---

## Grid vs Flexbox

### Flexbox

One direction.

### Grid

Two directions.

---

## Interview Questions

1. Grid vs Flexbox?
2. What is fr?
3. When to use grid?

---

# 12. Media Queries

Responsive design.

Example:

```css
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```

---

## Mobile First

Recommended:

```css
.card {
}

@media (min-width: 768px) {
}
```

---

## Interview Questions

1. What are media queries?
2. Mobile-first vs desktop-first?

---

# 13. Overflow

```css
overflow: hidden;
overflow: auto;
overflow: scroll;
```

---

## Interview Questions

1. Difference auto vs hidden?
2. Why overflow issues happen?

---

# 14. Animations

## Transition

```css
button {
  transition: 0.3s;
}
```

---

## Transform

```css
transform: scale(1.1);
transform: translateX(20px);
```

---

## Keyframes

```css
@keyframes fade {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}
```

---

## Interview Questions

1. transition vs animation?
2. Why transform better than top/left?

---

# 15. Responsive Design

Best Practices:

* Flexbox/Grid
* rem
* Media queries
* Min/max width
* Mobile-first

---

# Common CSS Mistakes

### z-index not working

Cause:
No positioned element.

---

### Width overflow

Cause:

```css
width: 100vw;
```

Creates horizontal scroll.

---

### Margin collapse confusion

Vertical margins collapse.

---

# Tricky Interview Questions

### Why height: 100% not working?

Parent needs explicit height.

---

### Why margin auto center not working?

Needs width.

---

### Why absolute element misplaced?

Parent lacks:

```css
position: relative;
```

---

# Coding Exercises

## Exercise 1

Center element vertically and horizontally.

---

## Exercise 2

Create responsive navbar.

Requirements:

* desktop row
* mobile column

---

## Exercise 3

Build dashboard layout using Grid.

Requirements:

* sidebar
* header
* content

---

# Senior-Level Questions

1. Explain repaint vs reflow.
2. How to improve CSS performance?
3. Explain stacking context.
4. Critical rendering path?
5. Why transform preferred for animation?
6. CSS architecture approaches?

   * BEM
   * CSS Modules
   * Styled Components

---

# Most Important CSS Topics for Interviews

Priority:

1. Flexbox
2. Grid
3. Positioning
4. Specificity
5. Box model
6. Responsive design
7. Units
8. Selectors
