# CSS Selectors

A CSS Selector is a pattern that matches specific elements within the HTML Document, enabling you to control their style  
there are various ways to select an element in CSS , here are some of them

### 1. Element Selector

---

| prefix                  | Syntax            | Applies to                | specificity |
| ----------------------- | ----------------- | ------------------------- | ----------- |
| does not use any prefix | `<type>{` ~~~ `}` | all elements of that type | 0, 0, 0, 1  |

The element selector, also known as type selector, matches HTML elements by their tag name.  
Example:

```html
<style>
  p {
    font-size: 5rem;
  }
</style>
```

This `p` will select all `<p>` tags in the document and apply the style to them

### 2. Class Selector

---

| prefix | Syntax                 | Applies to                        | specificity |
| ------ | ---------------------- | --------------------------------- | ----------- |
| `.`    | `.class-name{` ~~~ `}` | elements with the same class name | 0, 0, 1, 0  |

The class selector matches elements with a given class attribute. It uses a dot ( `.` ) prefix followed by the class name. Multiple elements can have the same class
Example:

```html
<head>
  <style>
    .highlight {
      font-size: 5rem;
    }
  </style>
</head>

<body>
  <p class="highlight">Blue and centered paragraph.</p>
  <p>This paragraph is unchanged (no class).</p>
  <div class="highlight">Blue and centered div.</div>
</body>
```

This `.highlight` will select all elements with class `highlight` and apply the style to them

### 3. ID Selector

---

| prefix | Syntax              | Applies to                                       | specificity |
| ------ | ------------------- | ------------------------------------------------ | ----------- |
| `#`    | `#ID-name{` ~~~ `}` | single element with that specific `id` attribute | 0, 1, 0, 0  |

The ID selector targets the single element with a specific id attribute, Since IDs are meant to be unique, an ID selector matches at most one element. It uses a hash ( `#` ) prefix followed by the ID name. Multiple elements can have the same class
Example:

```html
<head>
  <style>
    #title {
      color: green;
    }
  </style>
</head>

<body>
  <h1 id="title">Main Heading (green)</h1>

  <h1>Other Heading (default style)</h1>
</body>
```

This `#title` will select at most one elements with ID `title` and apply the style to it.

### 4. Grouping Selector

---

| prefix | Syntax                        | Applies to            | specificity                                                             |
| ------ | ----------------------------- | --------------------- | ----------------------------------------------------------------------- |
| `,`    | `SELECTOR, SELECTOR{` ~~~ `}` | All Selected elements | calculated separately for each element and does not have a single score |

The grouping selector lets you combine multiple selectors with commas (`,`) applying the same style to all of them  
Example:

```html
<head>
  <style>
    h1,
    h2,
    p {
      color: purple;
      margin: 10px;
    }
  </style>
</head>

<body>
  <h1>Heading 1</h1>
  <h2>Heading 2</h2>
  <p>A paragraph with purple text.</p>
  <div>A div (not purple, not in the group).</div>
</body>
```

`h1`, `h2` and `p` All will have the same styling

> **📝Note:** You can group all selectors , not just Element selectors.
>
> ```html
> h1, .class-selector, #id-selector { styles }
> ```
>
> .

### 5. Descendant Selector

---

| prefix  | Syntax                       | Applies to                                               | specificity                                         |
| ------- | ---------------------------- | -------------------------------------------------------- | --------------------------------------------------- |
| `SPACE` | `SELECTOR SELECTOR{` ~~~ `}` | All elements on the right inside All element on the left | Calculated by adding the specificity of all element |

The Descendant selector applies the styling for the elements inside each others by having a Empty Space (` `) between each one.

> **💡 Tip:**
> better to start reading it from the right side as:  
> "All elements of the `Right Eleme` inside All elements of the `Left Element` inside All elements of the `Left Element`..."

Example:

```html
<head>
  <style>
    div p {
      background-color: yellow;
    }
    div p a {
      color: purple;
    }
  </style>
</head>

<body>
  <div>
    <p>Paragraph inside a div (yellow background).</p>
  </div>
  <p>Paragraph outside div (default background).</p>

  <div>
    <p>
      <a href="">Link inside a p inside a div (purple color).</a>
    </p>
  </div>

  <p>
    <a href="">Link inside a p outside a div (default color).</a>
  </p>
</body>
```

Styling will be applied to all the `<p>` tags inside a `<div>`.  
Styling will be applied to all the `<a>` tags inside a `<p>` tags inside a `<div>`.

### 6. Child Selector

---

| prefix | Syntax                    | Applies to                         | specificity                                         |
| ------ | ------------------------- | ---------------------------------- | --------------------------------------------------- |
| `>`    | `Parent > Child{` ~~~ `}` | Only direct children of an element | Calculated by adding the specificity of all element |

The child selector matches only direct, outer children of an element and not nested elements using the (`>`) prefix.  
Example:

```html
<head>
  <style>
    ul > li {
      color: orange;
    }
  </style>
</head>

<body>
  <ul>
    <li>First item (orange)</li>
    <li>Second item (orange)</li>
    <ul>
      <li>Nested item (default color)</li>
    </ul>
  </ul>
</body>
```

Only the `li` in the outer `ul` will be effected

### 7. Adjacent Sibling Selector

---

| prefix | Syntax                                | Applies to                                         | specificity                                         |
| ------ | ------------------------------------- | -------------------------------------------------- | --------------------------------------------------- |
| `+`    | `Element + Targeted-Element{` ~~~ `}` | Only one element that is immediately after another | Calculated by adding the specificity of all element |

The adjacent sibling selector matches an element that is immediately after another using the (`+`) prefix.  
Example:

```html
<head>
  <style>
    h1 + p {
      background-color: lightgreen;
    }
  </style>
</head>

<body>
  <h1>Title</h1>
  <p>First paragraph (light green background).</p>
  <p>Second paragraph (default background).</p>

  <h1>SecondTitle</h1>
  <p>First paragraph (light green background).</p>
  <p>Second paragraph (default background).</p>
</body>
```

only one `<p>` tag that comes immediately after the `<h1>` tags will have the style applied to them

### 8. General Sibling Selector

---

| prefix | Syntax                               | Applies to                                                                                      | specificity                                         |
| ------ | ------------------------------------ | ----------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| `~`    | `Element ~ TargetedElement{` ~~~ `}` | elements that share the same parent and come after a given element, not necessarily immediately | Calculated by adding the specificity of all element |

The general sibling selector matches all elements that share the same parent and come after a given element, not necessarily immediately, it uses (`~`) prefix

Example:

```html
<head>
  <style>
    h1 ~ p {
      color: red;
    }
  </style>
</head>

<body>
  <h1>Heading</h1>
  <p>First paragraph after heading (red).</p>
  <div>Some other element</div>
  <p>Second paragraph after heading (red).</p>

  <h1>Another Heading</h1>
  <p>Paragraph after second heading (red).</p>
</body>
```

All the `<p>` tags that comes after the `<h1>` tags at any level under the same parent will have the style applied to them.

### 9. Attribute Selector

---

| prefix                | Syntax                         | Applies to                                      | specificity |
| --------------------- | ------------------------------ | ----------------------------------------------- | ----------- |
| `attribute and value` | `[attrebute="value"]{` ~~~ `}` | elements with the specified attribute and value | 0, 0, 1, 0  |

The attribute selector matches elements based on the presence or value of an attribute  
Example:

```html
<head>
  <style>
    input[type="text"] {
      border: 2px solid blue;
    }
  </style>
</head>

<body>
  <input type="text" placeholder="Text input (blue border)" />
  <input type="password" placeholder="Password (default)" />
  <button type="button">Button (default)</button>
</body>
```

only the inputs with `[type="text"]`, attribue: `type` and value: `text` gets styled

### 10. Pseudo-class Selector

---

| prefix    | Syntax                    | Applies to             | specificity |
| --------- | ------------------------- | ---------------------- | ----------- |
| `:Pseudo` | `Element:Pseudo{` ~~~ `}` | elements in a specific | 0, 0, 1, 0  |

A pseudo-class selector apply styles to elements in certain states, after using the (`:`) followed by the state  
Example:

```html
<head>
  <style>
    button:hover {
      background-color: yellow;
    }
  </style>
</head>

<body>
  <button>Hover over me</button>
</body>
```

When mouse cursor `hover` over this button , the color of it will become yellow
Other the pseudo-classes include:

### 💻Interactive/User Action Pseudo-Classes

| Pseudo-Class     | Description                                                                   | Example                                           |
| ---------------- | ----------------------------------------------------------------------------- | ------------------------------------------------- |
| `:hover`         | Applies when the user's mouse pointer is over an element.                     | `a:hover { color: red; }`                         |
| `:active`        | Applies while an element is being activated (e.g., pressed down).             | `button:active { background: darkblue; }`         |
| `:focus`         | Applies when an element has received input focus.                             | `input:focus { border: 2px solid blue; }`         |
| `:focus-visible` | Applies when the browser shows a visible focus indicator (for accessibility). | `a:focus-visible { outline: 3px dashed orange; }` |
| `:focus-within`  | Applies to an element when it or any of its descendants has focus.            | `form:focus-within { border: 1px solid green; }`  |

### 🔗 Link & History Pseudo-Classes

| Pseudo-Class | Description                                         | Example                        |
| ------------ | --------------------------------------------------- | ------------------------------ |
| `:link`      | Applies to unvisited links.                         | `a:link { color: blue; }`      |
| `:visited`   | Applies to links that the user has already visited. | `a:visited { color: purple; }` |

### 🏗️ Structural Pseudo-Classes

| Pseudo-Class     | Description                                                                  | Example                                        |
| ---------------- | ---------------------------------------------------------------------------- | ---------------------------------------------- |
| `:first-child`   | Matches an element that is the first child of its parent.                    | `p:first-child { font-weight: bold; }`         |
| `:nth-child(n)`  | Matches the n-th child of its parent (n can be _odd_, _even_, or a formula). | `li:nth-child(odd) { background: lightgray; }` |
| `:last-child`    | Matches an element that is the last child of its parent.                     | `li:last-child { border-bottom: none; }`       |
| `:only-child`    | Matches an element that is the only child of its parent.                     | `div > img:only-child { margin: auto; } `      |
| `:first-of-type` | Matches the first element of its type among siblings.                        | `div p:first-of-type { color: red; }`          |
| `:empty`         | Matches an element that has no children (including text).                    | `span:empty { display: none; }`                |

### 🎛️ Form & UI State Pseudo-Classes

| Pseudo-Class | Description                                                   | Example                                          |
| ------------ | ------------------------------------------------------------- | ------------------------------------------------ |
| `:checked`   | Matches a selected checkbox or radio button.                  | `input:checked + label { font-style: italic; }`  |
| `:disabled`  | Matches form elements that are currently disabled.            | `input:disabled { opacity: 0.5; }`               |
| `:required`  | Matches form input fields that have the `required` attribute. | `input:required { border-left: 5px solid red; }` |
| `:valid`     | Matches form elements whose content validates successfully.   | `input:valid { border-color: green; } `          |
| `:invalid`   | Matches form elements whose content fails to validate.        | `input:invalid { border-color: red; }`           |
| `:read-only` | Matches an element the user cannot edit.                      | `input:read-only { background: #eee; }`          |

### ➕ Advanced & Functional Pseudo-Classes

| Pseudo-Class         | Description                                                                   | Example                                   |
| -------------------- | ----------------------------------------------------------------------------- | ----------------------------------------- |
| `:not(selector)`     | Matches an element that does not match the given selector.                    | `p:not(.intro) { margin-top: 20px; }`     |
| `:root`              | Matches the root element of the document (`<html>`).                          | `:root { font-size: 16px; }`              |
| `:target`            | Matches an element targeted by the URL's hash (`#id`).                        | `section:target { padding: 10px; }`       |
| `:has(selector)`     | The Parent Selector. Matches an element only if it contains a matching child. | `a:has(img) { border: 1px solid #ccc; } ` |
| `:is(selector-list)` | Matches an element that matches any selector in the provided list.            | `h1:is(.title, #main) { color: navy; }`   |

### 11. Pseudo-element Selector

---

| prefix | Syntax                             | Applies to                            | specificity |
| ------ | ---------------------------------- | ------------------------------------- | ----------- |
| `::`   | `Element::Pseudo-element{` ~~~ `}` | elements with Pseudo-element Selector | 0, 0, 0, 1  |

A pseudo-element selector starts with two colons (::) and selects a part of an element, or inserts something into it

```html
<head>
  <style>
    p::before {
      content: "Note: ";
      color: red;
    }
  </style>
</head>

<body>
  <p>This text will have 'Note:' before it.</p>
  <p>Another paragraph prefixed with 'Note:'.</p>
  <div class="highlight">Blue and centered div.</div>
</body>
```

`p::before` allows you to insert content before a `<p>` element’s text. so, each `<p>` is prefixed with “Note:” in red  
here are some Pseudo-element Selector:

### ✨ Core Pseudo-element Selectors

| Pseudo-Class     | Description                                                                                                                    | Example                                |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------- |
| `::before`       | Inserts generated content before the content of the selected element. The `content` CSS property is required for this to work. | `p::before { content: "Note: "; }`     |
| `::after`        | Inserts generated content after the content of the selected element. Also requires the `content` property.                     | `a::after { content: " 🔗"; }`         |
| `::first-letter` | Selects and styles the first letter of the first line of a block-level element.                                                | `p::first-letter { font-size: 2em; }`  |
| `::first-line`   | Selects and styles the first line of a block-level element. The length of the first line depends on the width of the element.. | `p::first-line { font-weight: bold; }` |

### 🔍 Other Pseudo-element Selectors

| Pseudo-Class    | Description                                                                                                  | Example                                                   |
| --------------- | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------- |
| `::marker`      | Selects the marker box of a list item, typically the bullets (`•`) or numbers (`1.`).                        | `li::marker { color: #f00; }`                             |
| `::selection`   | Selects and styles the portion of an element that a user has highlighted (selected) with their mouse.        | `::selection { background: yellow; }`                     |
| `::placeholder` | Selects and styles the placeholder text inside form inputs (like `<input type="text" placeholder="...">`)    | `input::placeholder { color: grey; }`                     |
| `::backdrop`    | Selects the element behind a ذ or element in full-screen mode, allowing you to style the background overlay. | `dialog::backdrop { background-color: rgba(0,0,0,0.5); }` |

## CSS Cascade: Priority and Specificity

The browser follows a strict set of rules, known as The Cascade, to determine which style to apply when multiple rules target the same element and conflict over the same property (e.g., two rules setting the `color`). The priority is decided in three main steps:

### 1. The `!important` Flag (Highest Power)

When a style declaration includes the `!important` keyword (e.g., `color: red !important;`), it gains the highest priority, overriding all other rules unless another conflicting rule also uses `!important`

### 2. Specificity (The Tie-Breaker)

If no !important flag is used, the browser calculates the specificity score of each selector. The rule with the highest score wins, **regardless of its placement in the stylesheet**.

_Example: An ID selector will always override a Class selector, even if the class selector appears later
in the file._

```html
<head>
  <style>
    #blue {
      color: blue;
    }
    .green {
      color: green;
    }
  </style>
</head>

<body>
  <p id="blue" class="green">Blue paragraph.</p>
</body>
```

#### _In this example, the text color will be set to `#blue` even though the `.green` came after, but the specificity is higher for the `ID`_

• IDs (`#id`) contribute the most to the score.  
• Classes, Attributes, and
Pseudo-classes (`.class`, `[type]`, `:hover`) contribute less.  
• Elements and
Pseudo-elements (`p`, `::after`) contribute the least.

| Category                | Example                      | specificity  |
| ----------------------- | ---------------------------- | ------------ |
| Inline style attribute  | `<div style="color: blue;">` | (1, 0, 0, 0) |
| ID Selector             | `#my-id`                     | (0, 1, 0, 0) |
| Class Selector          | `.my-class`                  | (0, 0, 1, 0) |
| Attribute Selector      | `[type="submit"]`            | (0, 0, 1, 0) |
| Pseudo-class Selector   | `:hover`, `:nth-child(n)`    | (0, 0, 1, 0) |
| Element Selector        | `div`, `p`, `h1`             | (0, 0, 0, 1) |
| Pseudo-element Selector | `::before`, `::after`        | (0, 0, 0, 1) |
| Universal Selector      | `*`                          | (0, 0, 0, 0) |

### 3. Source Order (The Final Decider) If two conflicting

selectors have the exact same specificity score (e.g., two different class selectors: `.one` and `.two`), the browser applies the rule that was defined last in the stylesheet.
