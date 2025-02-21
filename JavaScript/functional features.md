
# Entry / exit animations

[https://developer.chrome.com/blog/entry-exit-animations/](https://developer.chrome.com/blog/entry-exit-animations/)

#### I dislike the fact that you still need to wait for animations to finish before you remove element from DOM. But hey, it's opportunity to use new `.getAnimations()` API

```
Promise.all(
  elem
    .getAnimations({ subtree: true })
    .map((animation) => animation.finished),
).then(() => elem.remove());
```


Firefox - behind flag

Safari - no implementation

Polyfill available

# Scroll Driven Animations

[https://scroll-driven-animations.style/](https://scroll-driven-animations.style/)
[https://github.com/flackr/scroll-timeline](https://github.com/flackr/scroll-timeline)


Firefox, Safari - no implementation. Can't polyfill 🤷🏼‍♂️

# View Transitions

### Animated transitions between separate DOM elements 🤩

- [https://http203-playlist.netlify.app/](https://http203-playlist.netlify.app/)
- [https://live-transitions.pages.dev/](https://live-transitions.pages.dev/)
- [https://developer.chrome.com/docs/web-platform/view-transitions/](https://developer.chrome.com/docs/web-platform/view-transitions/)