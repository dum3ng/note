# traits

## Object.create(null) vs {}

object created by `Object.create(null)` is totally empty, its prototype is null.

`{}` is an object, which has prototype is `Object.prototype`.

```js
const a = Object.create(null);
const b = {};
```

see [stackoverflow](https://stackoverflow.com/questions/37471799/difference-between-object-createnull-vs)

## where is variable declared by `const` and `let` in the global scope

```js
var a = 3;
window.a; // 3
const b = 43;
let c = 13;
window.b; // undefined
window.c; // undefined
```

Variable defined by `var` is in the global scope, and can be accessed by
`global[property]`, and in browser, global variable is `window`, so `window.a`
is the same as `a`.

TODO:

## `event.stopImmediatePropagation` vs `event.stopPropagation`

```js
button.addEventListener("click", () => {
  console.log(1);
});
button.addEventListener("click", (e) => {
  e.stopImmediatePropagation();
  console.log(2);
});
button.addEventListener("click", () => {
  console.log(3);
});

// resutt:  1 2
```

When an object add multiple event listeners, the listeners will trigger in order
when event is fired by default, and call `stopImmediatePropagation` will stop
the following listener to execute.

## async/await in `forEach`

```js
function delay(value) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(value);
    }, 1500);
  });
}

async function test() {
  const arr = [1, 2, 3];
  arr.forEach(async (x) => {
    const r = await delay(x);
    console.log(r);
  });
}

test();
```

The above code will not print value one after another with a delay.

More detailed explanation can be found [here](https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop)
