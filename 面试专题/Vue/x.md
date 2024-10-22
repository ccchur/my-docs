https://juejin.cn/post/7106134886833979399
# 响应式的变化

在vue2中会使用`Object.defineProperty`将data中的属性重新遍历，劫持每个属性，给属性转换为`getter/setter`。每一个组件都会