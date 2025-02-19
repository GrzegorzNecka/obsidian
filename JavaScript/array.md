
## `Array.fromAsync` for consuming asynchronous iterables 

```js
const asyncIterable = (async function* () {
  for (let i = 0; i < 5; i++) {
    await new Promise((resolve) => setTimeout(
        resolve, 10 * i
    ));
    yield i;
  }
})();

await Array.fromAsync(asyncIterable) === [0, 1, 2, 3, 4]
```

1. [ mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fromAsync)

# immutable arrays methods
### All those methods return new array instead of mutating

```js
Array.prototype.toSorted()
Array.prototype.toReversed()
Array.prototype.toSpliced()
Array.prototype.with()
```

### safe React state update

```js
const [posts, setPosts] = useState([]);

setPosts(posts => posts.with(
    3,
    {...posts[3],
    "title": "Updated post title"})
);
```

### Group arrays into Objects or Maps  [1](https://www.fricze.com/@@base@@#fn1 "see footnote")

```js
Object.groupBy()
Map.groupBy()
```
2. [mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/groupBy)