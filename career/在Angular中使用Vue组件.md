
https://juejin.cn/post/7010595352550047752

https://juejin.cn/post/7248906639705030717#heading-13

https://juejin.cn/post/7159221717959704589

利用Web Component API，与Vue3中的函数方法：`defineCustomElement`

Angular之所以能够使用Vue的组件，主要是由于在原生的Web中提供了`Web Components`这样的API，
这个API的可以让开发者创建能够服用的自定义元素，就是类似于`<div> </div>`这样的元素。创建这样的自定义元素的好处就在于，可以在任何框架中去使用。

其中Vue框架里面也提供了一个方法`defineCustomElement()`，`defineCustomElement` 是 Vue 3 提供的一个函数，用于将 Vue 组件转换为原生的 Web Components（自定义元素）。

- 转换 Vue 组件： 它接受一个 Vue 组件定义作为输入，并返回一个可以注册为自定义元素的构造函数。
- 创建 Web Components： 使用返回的构造函数，你可以通过 `customElements.define()` 方法注册一个新的自定义元素。
- 保留 Vue 的特性： 转换后的组件仍然可以使用 Vue 的响应式系统、组件化和其他核心特性。
- 跨框架兼容： 由于输出的是标准的 Web Components，这些组件可以在任何支持 Web Components 的环境中使用，不仅限于 Vue 应用。
- 生命周期映射： Vue 的生命周期钩子会被适当地映射到 Web Components 的生命周期回调上。
- 属性和事件处理： 它会自动处理 props 到属性的映射，以及事件的发射和监听。
