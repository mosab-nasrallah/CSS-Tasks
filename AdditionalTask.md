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

| prefix | Syntax                   | Applies to             | specificity |
| ------ | ------------------------ | ---------------------- | ----------- |
| `:`    | `Element:State{` ~~~ `}` | elements in a specific | 0, 0, 1, 0  |

A pseudo-class selector applies styles to elements in certain states using the (`:`) prefix  
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

This `.highlight` will select all elements with class `highlight` apply the style to them

### 11. Pseudo-element Selector

---

| prefix | Syntax                 | Applies to                        | specificity |
| ------ | ---------------------- | --------------------------------- | ----------- |
| `.`    | `.class-name{` ~~~ `}` | elements with the same class name | 0, 0, 1, 0  |

The class selector matches elements with a given class attribute. It uses a dot ( `.` ) prefix followed by the class name. Multiple elements can have the same class
Example

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

This `.highlight` will select all elements with class `highlight` apply the style to them

## CSS Cascade: Priority and Specificity
