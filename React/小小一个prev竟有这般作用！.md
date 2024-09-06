最近在写一个记录用户账户分类的功能，偶然发现项目中有这样一行代码`setAccountTypes((prev) => [...prev, accountType]);`, 突然发现自己对其中的参数`prev`不太理解，于是便有了写下这篇文章的契机。

阅读本文你将收获：
-   闭包如何捕获渲染时的状态。
-   为什么多个状态更新可能不会如预期工作（如果它们都基于同一个快照值）。
-   函数式更新如何解决这个问题，确保我们总是使用最新的状态值。

## 分析代码


`setAccountTypes((prev) => [...prev, accountType]);`

这行代码使用 `setState` 的**函数式**更新形式。让我们逐部分解析：

1.  `setAccountTypes` 是一个用来更新 `accountTypes` 状态的函数，它来自于 `useState` hook。

1.  `(prev) => {...}` 是一个箭头函数。这个函数接收一个参数 `prev`，代表当前的状态值（即更新前的 `accountTypes`）。

1.  `[...prev, accountType]` 是这个函数的返回值，它将成为 `accountTypes` 的新值。这里使用了展开运算符 `...` 来创建一个新数组。

    -   `...prev` 展开了当前的 `accountTypes` 数组的所有元素
    -   `accountType` 是要添加的新类型

1.  整体来说，这行代码的作用是：基于当前的 `accountTypes` 数组创建一个新数组，并在其中添加一个新的 `accountType`。

## 为什么这样写？

`setAccountTypes((prev) => [...accountTypes, accountType]);`

这样写可以吗？

**答案是可以，但是有可能出问题！**

让我们回到React官网，重新看看useState hook相关部分的描述：


![image.png](https://p9-xtjj-sign.byteimg.com/tos-cn-i-73owjymdk6/43e8b5fc9c704f11aa43362c1abff9e1~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAg5qy45Zi_Y2NjaHVy:q75.awebp?rk3s=f64ab15b&x-expires=1726218306&x-signature=%2FY3Sf5JLxOav7vHUkI9hi%2FvZodI%3D)

这是一个初学者容易犯的错误，`useState`并非是一个同步的hook，因此在频繁修改数据的时候需要特别注意，让我们看看官网是如何解决的：


![image.png](https://p9-xtjj-sign.byteimg.com/tos-cn-i-73owjymdk6/71ccdc6779904e36911eadb61725e69c~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAg5qy45Zi_Y2NjaHVy:q75.awebp?rk3s=f64ab15b&x-expires=1726218306&x-signature=46fDlVAyPfm5j7BP02kGg2aWTLI%3D)

从官网的描述中可以理解，使用一个更新函数去代替直接调用原数据。这里所说的 “*这里，`a => a + 1` 是更新函数。它获取 待定状态 并从中计算 下一个状态*”，不太理解什么是待定状态，为什么使用更新函数就是待定状态了。让我们再细细研究。

## 原因

1.  闭包和状态快照

当 React 调用你的组件函数时，它会为该渲染创建一个"快照"。这个快照包含了那一刻的 props 和 state 值。更新函数（例如 `prevState => ...`）会捕获这个最新的快照。

2.  更新队列机制

React 内部维护了一个更新队列。当你调用 `setState` 时，React 会将这个更新加入队列，而不是立即应用。

3.  函数式更新的特殊处理

当 React 处理更新队列时，它对函数式更新有特殊处理：
这个简化的模拟展示了 React 如何处理状态更新：

- 所有更新首先被加入队列。
- 处理队列时，React 会依次执行每个更新。
- 对于函数式更新，React 会传入当前最新的状态值。
- 对于直接赋值，React 直接使用该值。

接下来举一个例子：

```jsx
function Counter() { 
    const [count, setCount] = useState(0); 
    const handleClick = () => { 
        console.log('Current count:', count); // 闭包捕获的值
        setCount(count + 1); // 不使用函数式更新 
        setCount(count + 1); // 不使用函数式更新 
        setCount(prevCount => { 
            console.log('Previous count in update function:', prevCount); 
            return prevCount + 1; 
        }); 
        console.log('Count after updates:', count); // 闭包捕获的值仍然是旧的 
     };
 return ( 
     <div> <p>Count: {count}</p> 
         <button onClick={handleClick}>Increment</button> 
     </div> 
 );}
```
在这个例子中，`handleClick` 函数是一个闭包。它可以访问 `count` 状态，即使在之后被调用时也是如此。当 React 渲染组件时，会创建一个该时刻所有 props 和 state 的"快照"。这个快照在该次渲染期间保持不变。 在我们的例子中，每次 `Counter` 组件渲染时，都会创建一个新的 `handleClick` 函数。这个函数捕获了那一刻的 `count` 值。：

-   当你点击按钮时，`handleClick` 函数被调用。

-   第一个 `console.log` 会输出点击时 `count` 的当前值。

-   两个 `setCount(count + 1)` 调用都是基于同一个 `count` 值，因为它们都来自同一个渲染快照。

-   函数式更新 `setCount(prevCount => ...)` 不依赖于闭包中的 `count` 值，而是接收 React 提供的最新状态。

-   最后一个 `console.log` 仍然会显示旧的 `count` 值，因为这个值来自创建这个闭包时的快照。

## 最后

回收文章的标题，这个**prev**可以是其他命名，其实所指的是它所在的**更新函数**，在频繁使用的useState hook中居然牵连了react渲染，闭包，快照等的知识，精通可真难呀~



