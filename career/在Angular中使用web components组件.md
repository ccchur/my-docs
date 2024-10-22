
https://juejin.cn/post/7010595352550047752

https://juejin.cn/post/7248906639705030717#heading-13

https://juejin.cn/post/7159221717959704589



## About Web Components

### web components的三个基本标准，三个API：

- **Custom element（自定义元素）**：一组 JavaScript API，允许你定义 custom elements 及其行为，然后可以在你的用户界面中按照需要使用它们。Web Components 需要使用 ES6 的 Class 语法来定义一个继承 `HTMLElement` 的类，然后通过 `window.customElements.define() API` 来注册，才能在代码中使用。
	```js
	class HelloWorld extends HTMLElement { 
		constructor() { 
			super() 
			this.innerHTML = 'Hello World' 
		} 
	} 
	window.customElements.define('hello-world', HelloWorld)
````

	```html
	<hello-world> </hello-world>
	```


- **Shadow DOM（影子 DOM）**：一组 JavaScript API，用于将封装的“影子”DOM 树附加到元素（与主文档 DOM 分开呈现）并控制其关联的功能。通过这种方式，你可以保持元素的功能私有，这样它们就可以被脚本化和样式化，而不用担心与文档的其他部分发生冲突。
![[Pasted image 20241021095431.png]]

创建：

```js
	const shadowRoot = element.attachShadow({mode: 'open'})
```

- **HTML template（HTML 模板）：** [`<template>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/template) 和 [`<slot>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/slot) 元素使你可以编写不在呈现页面中显示的标记模板。然后它们可以作为自定义元素结构的基础被多次重用。

### 自定义元素有其完整的生命周期，并调用其与之对应的回调函数。

- `constructor`: 自定义元素的构造函数，在初始化时被调用。在构造函数中必须调用 `super()` 方法以执行父类的构造函数。可以在构造函数中做一些初始化的工作，比如设置默认值和其他预渲染操作。

- `attributeChangedCallback`: 当自定义元素在新增、修改、删除属性时会被调用。必须设置 `static get observedAttributes` 来指定您需要监听的属性。此函数会先于 `connectedCallback` 执行。

- `connectedCallback`: 当自定义元素首次插入到 DOM 文档时调用。你应该这这里运行需要渲染的内容和设置一些需要监听的事件。

- `disconnectedCallback`: 当自定义元素从 DOM 文档中移除时调用。应该在这里清除一些存储状态或终止 Ajax 请求。


### 利用Web Component API，与Vue3中的函数方法：`defineCustomElement`

Angular之所以能够使用Vue的组件，主要是由于在原生的Web中提供了`Web Components`这样的API，
这个API的可以让开发者创建能够服用的自定义元素，就是类似于`<div> </div>`这样的元素。创建这样的自定义元素的好处就在于，可以在任何框架中去使用。

其中Vue框架里面也提供了一个方法`defineCustomElement()`，`defineCustomElement` 是 Vue 3 提供的一个函数，用于将 Vue 组件转换为原生的 Web Components（自定义元素）。

- 转换 Vue 组件： 它接受一个 Vue 组件定义作为输入，并返回一个可以注册为自定义元素的构造函数。
- 创建 Web Components： 使用返回的构造函数，你可以通过 `customElements.define()` 方法注册一个新的自定义元素。
- 保留 Vue 的特性： 转换后的组件仍然可以使用 Vue 的响应式系统、组件化和其他核心特性。
- 跨框架兼容： 由于输出的是标准的 Web Components，这些组件可以在任何支持 Web Components 的环境中使用，不仅限于 Vue 应用。
- 生命周期映射： Vue 的生命周期钩子会被适当地映射到 Web Components 的生命周期回调上。
- 属性和事件处理： 它会自动处理 props 到属性的映射，以及事件的发射和监听。