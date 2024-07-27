# 大体比较

以下是React、Vue和Angular三个前端框架的主要异同点对比:

| 特性    | React        | Vue              | Angular             |
| ----- | ------------ | ---------------- | ------------------- |
| 开发商   | Facebook     | 尤雨溪(个人)          | Google              |
| 发布年份  | 2013         | 2014             | 2010                |
| 编程范式  | 组件化          | 组件化              | 组件化                 |
| 核心语言  | JavaScript   | JavaScript       | TypeScript          |
| 学习曲线  | 中等           | 较低               | 较陡                  |
| 性能    | 高            | 高                | 高                   |
| 数据绑定  | 单向           | 双向               | 双向                  |
| 模板语法  | JSX          | 模板               | 模板                  |
| 状态管理  | Redux, MobX  | Vuex             | RxJS, NgRx          |
| 路由    | React Router | Vue Router       | Angular Router      |
| 社区支持  | 非常强大         | 强大               | 强大                  |
| 适用规模  | 小到大型项目       | 小到大型项目           | 中到大型项目              |
| 生态系统  | 丰富           | 逐渐丰富             | 完整                  |
| 服务端渲染 | Next.js      | Nuxt.js          | Angular Universal   |
| 移动开发  | React Native | Vue Native, Weex | Ionic, NativeScript |
# 模板语法
## React
 > 在React中使用JSX（如果使用的是TS的话，则为TSX），JSX是JavaScript的语法扩展，允许在JavaScript中直接编写类似HTML的代码。

特点：
- 在JavaScript中直接编写UI结构
- 可以直接在模板中使用JavaScript表达式
- 需要编译转换为JavaScript
示例：
```JSX
function Welcome(props) {   
	return <h1>Hello, {props.name}</h1>; 
} 
const element = <Welcome name="Sara" />;
```
## Vue
> Vue使用基于HTML的模板语法，允许声明式地将渲染的DOM绑定到底层组件实例的数据。

特点：
- 更接近传统HTML
- 使用特殊的指令（如v-if, v-for）来处理逻辑
- 插值使用双大括号 {{ }}
示例：
```vue
<template>
	<div>
		 <h1>{{ title }}</h1> 
		 <ul> <li v-for="item in items" :key="item.id">{{ item.name }}</li> </ul>      </div> 
</template>

```
## Angular
> Angular也使用基于HTML的模板语法，但有其独特的特性和语法。

特点：
- 使用双大括号 {{ }} 进行插值
- 使用方括号 [] 进行属性绑定
- 使用圆括号 () 进行事件绑定
- 使用星号 * 表示结构性指令（如 `*ngIf`, `*ngFor`）
示例：
```html
<h1>{{title}}</h1>
<ul>
  <li *ngFor="let item of items">{{item.name}}</li>
</ul>
<button (click)="onButtonClick()">Click me</button>
```

# 事件绑定
## React
> React使用驼峰命名的事件名，并直接传递一个函数作为事件处理器。

特点：
- 使用驼峰命名（例如：onClick, onSubmit）
- 直接传递函数引用
- 事件处理函数通常在类组件中定义为方法，或在函数组件中定义为函数
示例：
```javascript
function Button() {
  const handleClick = (e) => {
    console.log('Button clicked', e);
  };

  return <button onClick={handleClick}>Click me</button>;
}
```
## Vue
> Vue使用 `v-on` 指令或其缩写 `@` 来绑定事件。

```html
<template>
  <button @click="handleClick">Click me</button>
</template>

<script>
export default {
  methods: {
    handleClick(event) {
      console.log('Button clicked', event);
    }
  }
}
</script>
```

## Angular
> Angular使用圆括号 `()` 来进行事件绑定。

特点：
- 使用 `(event)` 语法
- 可以在模板中使用简单的语句
- 复杂逻辑通常调用组件类中定义的方法
示例：
```typescript
@Component({
  selector: 'app-button',
  template: '<button (click)="handleClick($event)">Click me</button>'
})
export class ButtonComponent {
  handleClick(event: MouseEvent) {
    console.log('Button clicked', event);
  }
}
```

# 插槽
## React
> React没有直接的"插槽"概念，但使用 props.children 或自定义 props 来实现类似功能。

父组件：
```jsx
function Father () {
	return (
		<>
			<Son> 111 </Son>
		</>
	)
}
```
子组件：
```jsx
export default function Son (props) {
	return (
		<p>{props.children}</p>
	)
}
```

## Vue
> Vue提供了三种主要类型的插槽：默认插槽、命名插槽和作用域插槽。

### 默认插槽

子组件：
``` html
<template>
	<div> 
		<h2>子组件标题</h2> 
		<slot></slot>
	</div>
</template>
```
父组件：
```HTML
<template>
	<ChildComponent>
		<p>这是插入到默认插槽的内容</p> 
	</ChildComponent>
</template>
```
### 具名插槽

子组件：
``` html
<template>
  <div class="container">
    <header>
      <slot name="header"></slot>
    </header>
    <main>
      <slot></slot>
    </main>
    <footer>
      <slot name="footer"></slot>
    </footer>
  </div>
</template>
```
父组件：
```HTML
<template>
  <LayoutComponent>
    <template v-slot:header>
      <h1>页面标题</h1>
    </template>

    <p>主要内容放在默认插槽</p>

    <template v-slot:footer>
      <p>页脚内容</p>
    </template>
  </LayoutComponent>
</template>
```
### 作用域插槽
> 作用域插槽允许子组件向父组件传递数据。

子组件：
``` html
<template>
  <ul>
    <li v-for="item in items" :key="item.id">
      <slot :item="item">
        {{ item.name }}
      </slot>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { id: 1, name: 'Item 1', description: 'Description 1' },
        { id: 2, name: 'Item 2', description: 'Description 2' },
      ]
    }
  }
}
</script>
```
父组件：
```HTML
<template>
  <ListComponent>
    <template v-slot:default="slotProps">
      <strong>{{ slotProps.item.name }}</strong>
      <em>{{ slotProps.item.description }}</em>
    </template>
  </ListComponent>
</template>
```
## Angular
> Angular 并没有直接使用"插槽"这个术语，但它提供了一个类似的功能，称为"内容投影"（Content Projection）。这个功能使用 `<ng-content>` 元素来实现。

### 基本用法
子组件：
```typescript
@Component({
  selector: 'app-child',
  template: `
    <div class="child-wrapper">
      <h2>子组件标题</h2>
      <ng-content></ng-content>
    </div>
  `
})
export class ChildComponent {}
```

父组件使用:
```ts
<app-child>
  <p>这是投影到子组件的内容</p>
</app-child>
```
### 多个投影点
子组件：
```typescript
@Component({
  selector: 'app-layout',
  template: `
    <header>
      <ng-content select="[header]"></ng-content>
    </header>
    <main>
      <ng-content></ng-content>
    </main>
    <footer>
      <ng-content select="[footer]"></ng-content>
    </footer>
  `
})
export class LayoutComponent {}
```

父组件使用:
```ts
<app-layout>
  <div header>这是头部内容</div>
  <p>这是主要内容</p>
  <div footer>这是底部内容</div>
</app-layout>
```
### 条件内容投影
可以使用 `*ngIf` 来条件性地显示投影内容：
```typescript
@Component({
  selector: 'app-child',
  template: `
    <div class="child-wrapper">
      <ng-content *ngIf="showContent"></ng-content>
    </div>
  `
})
export class ChildComponent {
  @Input() showContent: boolean = true;
}
```

## 生命周期
