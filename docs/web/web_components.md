# web components

web components 将需要实现的功能组件化，从而达到复用化，加速 web 开发的速度。

web components 的实现包括三个部分：

- custom elements 自定义元素
- shadom DOM 阴影节点
- HTML template
  - `<template>`
  - `<slot>`

## 技术套件

### 自定义元素

自定义元素包括两种： 独立自定义元素和自定义内置元素。

独立自定义元素即扩展`HTMLElement`的类。

```js
class MyComponent extends HTMLElement {
  constructor() {
    super()
  }
}
```

自定义内置元素即扩展具体的 HTML 元素的类。

```js
class MyBuiltInComponent extends HTMLParagraphElement {
  constructor() {
    super()
  }
}
```

自定义元素最终被 `CustomElementRegistry` 添加。

浏览器中的， `window` 对象自带一个`CustomElementRegistry`的实例，
即 `window.customElements`, 自定义的元素即可如此添加：

```js
customElements.define('my-component', MyComponent)
customElements.define('my-built-in-component', MyComponent, { extends: 'p' })
```

### 阴影节点

一个`ShadowRoot`对象，
在阴影节点下， 浏览器单独渲染节点树，因此样式，布局都得到了封装。

### HTML template

`<template>` 标签在浏览器加载文档时，会去解析其中的内容，但是只是为了校验其中内容的
合法性，并不会对其进行渲染.

---

综上， web components 实际上是一 web 技术套件，包含新的标签， web 对象，web API。

## 生态

一些库对这些 web 技术进行了封装，可以按照更工程化的方式去编写 web 组件，
然后通过编译过程将其打包为原生的 api。

例如：

- `lit-element`
- `smart`
- `stencil`

由于 web component 不依赖与具体的前端框架（本身属于 web 标准的一部分）
