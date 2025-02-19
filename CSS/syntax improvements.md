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

28 min