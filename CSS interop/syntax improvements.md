## `:is(), :where()`

### for shorter CSS selectors [1](https://www.fricze.com/@@base@@#fn1 "see footnote")

1. [https://developer.mozilla.org/en-US/docs/Web/CSS/:is](https://developer.mozilla.org/en-US/docs/Web/CSS/:is)

## Before `:is()`

```css
/* Level 0 */
h1 {
  font-size: 30px;
}

/* Level 1 */
section h1,
article h1,
aside h1,
nav h1 {
  font-size: 25px;
}

/* Level 2 */
section section h1,
section article h1,
section aside h1,
section nav h1,
article section h1,
article article h1,
article aside h1,
article nav h1…
```

## After `:is()` 🔥

```css
/* Level 0 */
h1 {
  font-size: 30px;
}
/* Level 1 */
:is(section, article, aside, nav) h1 {
  font-size: 25px;
}
/* Level 2 */
:is(section, article, aside, nav) :is(section, article, aside, nav) h1 {
  font-size: 20px;
}
```


## `:has()` – real parent selector! [1](https://www.fricze.com/@@base@@#fn1 "see footnote")

```
label:has(input:invalid) {
    color: red;
}
```

1. [https://codepen.io/wuuuuuuuuut/pen/abxEyzr](https://codepen.io/wuuuuuuuuut/pen/abxEyzr)


Available since 2022. Polyfill available

## Control CSS cascading with `@layer`

1. [https://developer.mozilla.org/en-US/docs/Web/CSS/@layer](https://developer.mozilla.org/en-US/docs/Web/CSS/@layer)
2. [https://css-tricks.com/css-cascade-layers/](https://css-tricks.com/css-cascade-layers/)
3. [https://www.oddbird.net/2022/06/21/cascade-layers-polyfill/](https://www.oddbird.net/2022/06/21/cascade-layers-polyfill/)


Available since 2022. Polyfill available

![[Pasted image 20250220150230.png]]

![[Pasted image 20250220150315.png]]

```css
@import url(headings.css) layer(default);
@import url(links.css) layer(default);
@import url(links-dimmed.css) layer(dimmed);

@layer default { audio[controls] { display: block; } }

```

# CSS Nesting! [1](https://www.fricze.com/@@base@@#fn1 "see footnote")

```css
// that's native CSS! 🥳
input {
  /* styles for input not in a label  */
  border: tomato 2px solid;
}
label {
  /* styles for label */
  font-family: system-ui;
  font-size: 1.25rem;
  & input {
    /* styles for input in a label  */
    border: blue 2px dashed;
  }
}
```

1. [https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting/Using_CSS_nesting](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting/Using_CSS_nesting)


## Individual transform properties [1](https://www.fricze.com/@@base@@#fn1 "see footnote")

```css
// old transform property
.logo {
    transform: rotate(45deg) scale(2) translate(40px, 0);
}

// new, individual properties
.logo {
    rotate: 45deg;
    scale: 2;
    translate: 40px, 0;
}
```

1. [https://blog.logrocket.com/deep-dive-css-individual-transform-properties](https://blog.logrocket.com/deep-dive-css-individual-transform-properties/)


