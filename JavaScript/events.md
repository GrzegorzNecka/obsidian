### Native EventTarget constructor

`.addEventListener()` on your own objects

```js

        class Counter extends EventTarget {
            constructor(initialValue = 0) {
              super();
              this.value = initialValue;
            }

            #emitChangeEvent() {
              this.dispatchEvent(new CustomEvent("valuechange", { detail: this.value }));

            }

            increment() {
              this.value++;
              this.#emitChangeEvent();
            }

            decrement() {
              this.value--;
              this.#emitChangeEvent();
            }
          }

          const counter = new Counter(0);

          counter.addEventListener("valuechange", (event) => {

            document.querySelector("#currentValue").innerText = event.detail;

          });
```