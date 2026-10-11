# CSS Flexbox Crash Course 🚀

## Table of Contents
1. [Basics](#1-basics)
2. [Flex Direction](#2-flex-direction)
3. [Justify Content](#3-justify-content)
4. [Align Items](#4-align-items)
5. [Flex Wrap](#5-flex-wrap)
6. [Flex Grow, Shrink & Basis](#6-flex-grow-shrink--basis)
7. [Align Self](#7-align-self)
8. [Order](#8-order)
9. [Gap](#9-gap)
10. [Real-World Examples](#10-real-world-examples)

---

## 1. Basics

Flexbox starts by adding `display: flex` to a **parent container**.

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
/* Without Flex: items stack vertically (block behavior) */
/* With Flex: items sit side-by-side in a row */

.container {
  display: flex;          /* Activates flexbox */
  background: #1a1a2e;
  padding: 10px;
}

.item {
  background: #e94560;
  color: white;
  padding: 20px 40px;
  margin: 5px;
  font-size: 24px;
}
```

**Result:**
```
┌──────────────────────────────────┐
│  [ 1 ]  [ 2 ]  [ 3 ]            │
└──────────────────────────────────┘
```

> **Key Concept:** The parent is the **flex container**. Children become **flex items**.

---

## 2. Flex Direction

Controls the **main axis** — the direction items flow.

```css
.container {
  display: flex;
  flex-direction: row;             /* DEFAULT - left to right → */
}

/* Other values: */
flex-direction: row-reverse;       /* right to left ← */
flex-direction: column;            /* top to bottom ↓ */
flex-direction: column-reverse;    /* bottom to top ↑ */
```

### Visual Comparison

```css
/* ROW (default) */
.row {
  display: flex;
  flex-direction: row;
}
```
```
[ 1 ] [ 2 ] [ 3 ]    →  main axis
```

```css
/* COLUMN */
.column {
  display: flex;
  flex-direction: column;
}
```
```
[ 1 ]
[ 2 ]     ↓ main axis
[ 3 ]
```

```css
/* ROW-REVERSE */
.row-reverse {
  display: flex;
  flex-direction: row-reverse;
}
```
```
            [ 3 ] [ 2 ] [ 1 ]    ←  main axis
```

---

## 3. Justify Content

Aligns items along the **main axis**.

```css
.container {
  display: flex;
  justify-content: flex-start;     /* DEFAULT */
}
```

### All Values Visualized

```css
/* flex-start (default) */
justify-content: flex-start;
┌──────────────────────────────────┐
│ [1] [2] [3]                     │
└──────────────────────────────────┘

/* flex-end */
justify-content: flex-end;
┌──────────────────────────────────┐
│                     [1] [2] [3] │
└──────────────────────────────────┘

/* center */
justify-content: center;
┌──────────────────────────────────┐
│          [1] [2] [3]            │
└──────────────────────────────────┘

/* space-between */
justify-content: space-between;
┌──────────────────────────────────┐
│ [1]         [2]         [3]     │
└──────────────────────────────────┘

/* space-around */
justify-content: space-around;
┌──────────────────────────────────┐
│   [1]       [2]       [3]      │
└──────────────────────────────────┘
/* Each item gets EQUAL margin on both sides */

/* space-evenly */
justify-content: space-evenly;
┌──────────────────────────────────┐
│    [1]      [2]      [3]       │
└──────────────────────────────────┘
/* EQUAL space between all items AND edges */
```

### Example: Centering a Button

```html
<div class="hero">
  <button class="cta">Get Started</button>
</div>
```

```css
.hero {
  display: flex;
  justify-content: center;    /* Centers horizontally */
  align-items: center;        /* Centers vertically */
  height: 100vh;
}
```

---

## 4. Align Items

Aligns items along the **cross axis** (perpendicular to main axis).

```css
.container {
  display: flex;
  height: 300px;               /* Need height to see the effect */
  align-items: stretch;        /* DEFAULT */
}
```

### All Values Visualized

```css
/* stretch (default) - items stretch to fill container */
align-items: stretch;
┌──────────────────────┐
│ [  1  ] [  2  ] [ 3 ]│
│ [     ] [     ] [   ]│
│ [     ] [     ] [   ]│
└──────────────────────┘

/* flex-start */
align-items: flex-start;
┌──────────────────────┐
│ [ 1 ] [ 2 ] [ 3 ]   │
│                      │
│                      │
└──────────────────────┘

/* flex-end */
align-items: flex-end;
┌──────────────────────┐
│                      │
│                      │
│ [ 1 ] [ 2 ] [ 3 ]   │
└──────────────────────┘

/* center */
align-items: center;
┌──────────────────────┐
│                      │
│ [ 1 ] [ 2 ] [ 3 ]   │
│                      │
└──────────────────────┘

/* baseline - aligns text baselines */
align-items: baseline;
┌──────────────────────────┐
│ [small] [ BIG ] [medium] │  ← text baselines align
│                          │
└──────────────────────────┘
```

---

## 5. Flex Wrap

By default, items squeeze into **one line**. `flex-wrap` lets them wrap.

```css
.container {
  display: flex;
  flex-wrap: nowrap;          /* DEFAULT - single line, items shrink */
}

flex-wrap: wrap;              /* Items wrap to next line ↓ */
flex-wrap: wrap-reverse;      /* Items wrap upward ↑ */
```

### Example

```html
<div class="gallery">
  <div class="photo">1</div>
  <div class="photo">2</div>
  <div class="photo">3</div>
  <div class="photo">4</div>
  <div class="photo">5</div>
  <div class="photo">6</div>
</div>
```

```css
.gallery {
  display: flex;
  flex-wrap: wrap;             /* Allow wrapping! */
}

.photo {
  width: 200px;
  height: 200px;
  margin: 5px;
  background: #0f3460;
}
```

```
/* If container is 650px wide: */
┌─────────────────────────────┐
│ [ 1 ] [ 2 ] [ 3 ]          │
│ [ 4 ] [ 5 ] [ 6 ]          │
└─────────────────────────────┘
```

### align-content (works with wrap)

Controls spacing of **wrapped lines**:

```css
.container {
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;     /* Lines packed to top */
  align-content: flex-end;       /* Lines packed to bottom */
  align-content: center;         /* Lines centered */
  align-content: space-between;  /* Equal space between lines */
  align-content: space-around;   /* Equal space around lines */
  align-content: stretch;        /* DEFAULT - lines stretch */
}
```

---

## 6. Flex Grow, Shrink & Basis

These go on **flex items** (children), not the container.

### flex-basis
Sets the **initial size** before growing/shrinking.

```css
.item {
  flex-basis: 200px;    /* Start at 200px (replaces width in row) */
}
```

### flex-grow
How much an item **grows** relative to others.

```css
.item-1 { flex-grow: 1; }    /* Gets 1 share of extra space */
.item-2 { flex-grow: 2; }    /* Gets 2 shares of extra space */
.item-3 { flex-grow: 1; }    /* Gets 1 share of extra space */
```

```
┌──────────────────────────────────────┐
│ [  1 share  ] [   2 shares   ] [ 1 ]│
└──────────────────────────────────────┘
```

### flex-shrink
How much an item **shrinks** when space is tight.

```css
.item-1 { flex-shrink: 1; }    /* Shrinks normally */
.item-2 { flex-shrink: 0; }    /* NEVER shrinks */
.item-3 { flex-shrink: 3; }    /* Shrinks 3x faster */
```

### The `flex` Shorthand ⭐

```css
/* flex: grow shrink basis */
.item {
  flex: 0 1 auto;     /* DEFAULT: don't grow, can shrink, auto size */
}

.item {
  flex: 1;            /* Same as: flex: 1 1 0%  → grow equally */
}

.item {
  flex: 0 0 250px;    /* Fixed 250px — won't grow or shrink */
}
```

### Example: Flexible Sidebar Layout

```css
.layout {
  display: flex;
}

.sidebar {
  flex: 0 0 250px;      /* Fixed 250px sidebar */
}

.main-content {
  flex: 1;               /* Takes ALL remaining space */
}
```

```
┌──────────────────────────────────────────┐
│ [  Sidebar   ] [      Main Content      ]│
│ [  250px     ] [      fills rest        ]│
│ [  fixed     ] [      of space          ]│
└──────────────────────────────────────────┘
```

---

## 7. Align Self

Overrides `align-items` for a **single item**.

```css
.container {
  display: flex;
  align-items: flex-start;
  height: 300px;
}

.item-2 {
  align-self: flex-end;        /* Only this item goes to bottom */
}

.item-3 {
  align-self: center;          /* Only this item centers */
}
```

```
┌──────────────────────────────┐
│ [ 1 ]             [ 3 ]     │  ← 1 at top (flex-start)
│                              │  ← 3 centered
│          [ 2 ]               │  ← 2 at bottom (flex-end)
└──────────────────────────────┘
```

---

## 8. Order

Changes **visual order** without changing HTML.

```css
.item-1 { order: 3; }    /* Appears third */
.item-2 { order: 1; }    /* Appears first */
.item-3 { order: 2; }    /* Appears second */
/* Default order is 0 for all items */
```

```
HTML:  [ 1 ] [ 2 ] [ 3 ]
Visual: [ 2 ] [ 3 ] [ 1 ]
```

---

## 9. Gap

Adds space **between** flex items (not on the edges).

```css
.container {
  display: flex;
  gap: 20px;               /* 20px between ALL items */

  /* OR separate values: */
  row-gap: 20px;           /* Between rows (when wrapped) */
  column-gap: 10px;        /* Between columns */

  /* Shorthand: */
  gap: 20px 10px;          /* row-gap column-gap */
}
```

```
/* gap: 20px */
┌──────────────────────────────┐
│ [1]  20px  [2]  20px  [3]   │  ← No space at edges!
└──────────────────────────────┘
```

---

## 10. Real-World Examples

### 📌 Example 1: Navigation Bar

```html
<nav class="navbar">
  <div class="logo">MyBrand</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
  <button class="cta-btn">Sign Up</button>
</nav>
```

```css
.navbar {
  display: flex;
  justify-content: space-between;  /* Logo | Links | Button */
  align-items: center;             /* Vertically centered */
  padding: 15px 30px;
  background: #16213e;
  color: white;
}

.logo {
  font-size: 24px;
  font-weight: bold;
}

.nav-links {
  display: flex;                   /* Nested flex! */
  list-style: none;
  gap: 30px;                       /* Space between links */
}

.nav-links a {
  color: white;
  text-decoration: none;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: #e94560;
}

.cta-btn {
  background: #e94560;
  color: white;
  border: none;
  padding: 10px 25px;
  border-radius: 5px;
  cursor: pointer;
}
```

```
┌──────────────────────────────────────────────────┐
│ MyBrand     Home  About  Services  Contact  [Sign Up] │
└──────────────────────────────────────────────────┘
```

---

### 📌 Example 2: Card Layout (Responsive)

```html
<div class="card-container">
  <div class="card">
    <img src="https://picsum.photos/300/200" alt="Card Image">
    <div class="card-body">
      <h3>Card Title 1</h3>
      <p>Lorem ipsum dolor sit amet consectetur.</p>
      <button>Read More</button>
    </div>
  </div>
  <div class="card">
    <img src="https://picsum.photos/300/201" alt="Card Image">
    <div class="card-body">
      <h3>Card Title 2</h3>
      <p>Lorem ipsum dolor sit amet consectetur adipiscing.</p>
      <button>Read More</button>
    </div>
  </div>
  <div class="card">
    <img src="https://picsum.photos/300/202" alt="Card Image">
    <div class="card-body">
      <h3>Card Title 3</h3>
      <p>Lorem ipsum dolor.</p>
      <button>Read More</button>
    </div>
  </div>
</div>
```

```css
.card-container {
  display: flex;
  flex-wrap: wrap;              /* Cards wrap on small screens */
  gap: 20px;
  justify-content: center;
  padding: 20px;
}

.card {
  display: flex;
  flex-direction: column;       /* Stack image + content vertically */
  flex: 0 1 300px;              /* Start at 300px, can shrink, won't grow */
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.card-body {
  display: flex;
  flex-direction: column;       /* Nested flex column! */
  flex: 1;                      /* Fill remaining card space */
  padding: 20px;
}

.card-body p {
  flex: 1;                      /* Push button to bottom */
}

.card-body button {
  align-self: flex-start;       /* Button doesn't stretch full width */
  background: #0f3460;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}
```

```
┌──────────┐  ┌──────────┐  ┌──────────┐
│  [image] │  │  [image] │  │  [image] │
│          │  │          │  │          │
│  Title 1 │  │  Title 2 │  │  Title 3 │
│  text... │  │  text... │  │  text... │
│          │  │  more... │  │          │
│ [Button] │  │ [Button] │  │ [Button] │  ← all buttons at bottom!
└──────────┘  └──────────┘  └──────────┘
```

---

### 📌 Example 3: Holy Grail Layout

```html
<div class="holy-grail">
  <header class="hg-header">Header</header>
  <div class="hg-body">
    <nav class="hg-nav">Sidebar Left</nav>
    <main class="hg-main">Main Content</main>
    <aside class="hg-aside">Sidebar Right</aside>
  </div>
  <footer class="hg-footer">Footer</footer>
</div>
```

```css
.holy-grail {
  display: flex;
  flex-direction: column;       /* Stack header/body/footer */
  min-height: 100vh;
}

.hg-header, .hg-footer {
  background: #16213e;
  color: white;
  padding: 20px;
  text-align: center;
}

.hg-body {
  display: flex;                /* Nested flex for columns */
  flex: 1;                     /* Takes remaining vertical space */
}

.hg-nav {
  flex: 0 0 200px;             /* Fixed 200px left sidebar */
  background: #1a1a2e;
  color: white;
  padding: 20px;
}

.hg-main {
  flex: 1;                     /* Main content fills space */
  padding: 20px;
  background: #f5f5f5;
}

.hg-aside {
  flex: 0 0 150px;             /* Fixed 150px right sidebar */
  background: #1a1a2e;
  color: white;
  padding: 20px;
}

/* RESPONSIVE: Stack on mobile */
@media (max-width: 768px) {
  .hg-body {
    flex-direction: column;    /* Stack sidebars below main */
  }

  .hg-nav, .hg-aside {
    flex: 0 0 auto;            /* Auto height when stacked */
  }
}
```

```
Desktop:
┌──────────────────────────────────────┐
│              HEADER                  │
├──────────┬─────────────┬────────────┤
│ Sidebar  │             │  Sidebar   │
│  Left    │   Main      │   Right    │
│  200px   │   Content   │   150px    │
│  fixed   │   flexible  │   fixed    │
├──────────┴─────────────┴────────────┤
│              FOOTER                  │
└──────────────────────────────────────┘

Mobile (< 768px):
┌────────────────┐
│     HEADER     │
├────────────────┤
│  Main Content  │
├────────────────┤
│  Sidebar Left  │
├────────────────┤
│ Sidebar Right  │
├────────────────┤
│     FOOTER     │
└────────────────┘
```

---

### 📌 Example 4: Centering (The Classic Problem)

```css
/* PERFECTLY center anything */
.center-everything {
  display: flex;
  justify-content: center;    /* Horizontal center */
  align-items: center;        /* Vertical center */
  height: 100vh;
}

/* That's it. Two lines. */
```

---

### 📌 Example 5: Footer Sticking to Bottom

```html
<div class="page">
  <header>Header</header>
  <main>Short content here...</main>
  <footer>Footer</footer>
</div>
```

```css
.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1;    /* Main grows to push footer down */
}
```

```
Even with short content:
┌─────────────────┐
│     Header      │
├─────────────────┤
│  Short content  │
│                 │
│   (flex: 1      │
│    fills this)  │
│                 │
├─────────────────┤
│     Footer      │  ← Always at bottom!
└─────────────────┘
```

---

## 🧠 Quick Reference Cheat Sheet

```
╔══════════════════════════════════════════════════════════════╗
║                  FLEX CONTAINER PROPERTIES                  ║
╠══════════════════════════════════════════════════════════════╣
║ display:         flex | inline-flex                         ║
║ flex-direction:  row | row-reverse | column | column-reverse║
║ flex-wrap:       nowrap | wrap | wrap-reverse               ║
║ justify-content: flex-start|flex-end|center|space-between   ║
║                  space-around | space-evenly                ║
║ align-items:     stretch|flex-start|flex-end|center|baseline║
║ align-content:   stretch|flex-start|flex-end|center         ║
║                  space-between | space-around               ║
║ gap:             <row-gap> <column-gap>                     ║
╠══════════════════════════════════════════════════════════════╣
║                    FLEX ITEM PROPERTIES                     ║
╠══════════════════════════════════════════════════════════════╣
║ flex-grow:       0 (default) | <number>                     ║
║ flex-shrink:     1 (default) | <number>                     ║
║ flex-basis:      auto (default) | <length>                  ║
║ flex:            <grow> <shrink> <basis>  (shorthand)       ║
║ align-self:      auto|flex-start|flex-end|center|stretch    ║
║ order:           0 (default) | <integer>                    ║
╚══════════════════════════════════════════════════════════════╝
```

---

## 🎮 Practice Resources

| Resource | URL |
|----------|-----|
| **Flexbox Froggy** | [flexboxfroggy.com](https://flexboxfroggy.com) |
| **Flexbox Defense** | [flexboxdefense.com](http://www.flexboxdefense.com) |
| **CSS Tricks Guide** | [css-tricks.com/snippets/css/a-guide-to-flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) |

> **Golden Rule:** `justify-content` = **main axis**, `align-items` = **cross axis**. When you change `flex-direction`, **the axes swap!** 🔄