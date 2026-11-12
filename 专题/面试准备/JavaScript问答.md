- 1. 数据类型
    
    八种：undefined, null, boolean, string, number, object, bigint, symbol
    
    - 基本数据类型
        
        undefined，null，boolean，number，string
        
    - 引用数据类型
        
        对象，数组，函数
        
- 2. typeof / instanceof / constructor / Object.prototype.toString.call()
    3. typeof

```JavaScript
console.log(typeof 2);               // number
console.log(typeof true);            // boolean
console.log(typeof 'str');           // string
console.log(typeof []);              // object    
console.log(typeof function(){});    // function
console.log(typeof {});              // object
console.log(typeof undefined);       // undefined
console.log(typeof null);            // object
```

```
  判断数据类型，但是数组，对象，null，都会被判断为object
```

2. instanceof

```JavaScript
console.log(2 instanceof Number);              // false
console.log(true instanceof Boolean);          // false 
console.log('str' instanceof String);          // false 
 
console.log([] instanceof Array);               // true
console.log(function(){} instanceof Function);  // true
console.log({} instanceof Object);              // true

```

```
  判断在其原型链中能否找到该类型的原型，只能判断引用数据类型
```

3. constructor

```JavaScript
console.log((2).constructor === Number);               // true
console.log((true).constructor === Boolean);           // true
console.log(('str').constructor === String);           // true
console.log(([]).constructor === Array);               // true
console.log((function() {}).constructor === Function); // true
console.log(({}).constructor === Object);              // true
```

```
  `constructor`有两个作用，一是判断数据的类型，二是对象实例通过 `constrcutor` 对象访问它的构造函数。需要注意，如果创建一个对象来改变它的原型，`constructor`就不能用来判断数据类型了
```

4. Object.prototype.toString.call()

```JavaScript
var a = Object.prototype.toString;
 
console.log(a.call(2));              // [object Number]
console.log(a.call(true));           // [object Boolean]
console.log(a.call('str'));          // [object String]
console.log(a.call([]));             // [object Array]
console.log(a.call(function(){}));   // [object Function]
console.log(a.call({}));             // [object Object]
console.log(a.call(undefined));      // [object Undefined]
console.log(a.call(null));           // [object Null]
```

```
  使用 Object 对象的原型方法 toString 来判断数据类型
```

- 3. null和undefined的区别
    
    undefined 代表的含义是**未定义**，null 代表的含义是**空对象**。一般变量声明了但还没有定义的时候会返回 undefined，null主要用于赋值给一些可能会返回对象的变量，作为初始化。
    
- 4. let、const、var

|区别|var|let|const|
|---|---|---|---|
|是否有块级作用域||✅|✅|
|是否存在变量提升|✅|||
|是否添加全局属性|✅|||
|能否重复声明变量|✅|||
|是否存在暂时性死区||✅|✅|
|是否必须设置初始值|||✅|
|能否改变指针指向|✅|✅||

- 5. 数组操作
    
    - map
        
        遍历数组，返回回调函数返回的值组成的新数组
        
        [https://blog.csdn.net/web15870359587/article/details/124275372](https://blog.csdn.net/web15870359587/article/details/124275372)
        

```JavaScript
let a = [1,2,3,4]
let b = a.map(item => {
    return item+1
})
console.log(b)  //[2,3,4,5]
```

- forEach
    
    无法break，可以用try/catch中throw new Error来停止
    

```JavaScript
let a = [1,2,3,4]
let x = []
let b = a.forEach(item => {
    x.push(item)
})
console.log(x) // [1,2,3,4]
```

- filter
    
    过滤，创建一个新数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。
    

```JavaScript
let nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
 
let res = nums.filter((num) => {
  return num > 5;
});
 
console.log(res);  // [6, 7, 8, 9, 10]
```

- some
    
    some() 方法会依次执行[数组](https://so.csdn.net/so/search?q=%E6%95%B0%E7%BB%84&spm=1001.2101.3001.7020)的每个元素：
    
    如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测。
    
    如果没有满足条件的元素，则返回false。
    
    不改变元素组
    

```JavaScript
let a = [1,20,30,40]
let b = a.some(item => {
    return item > 8
})
console.log(b)   //true
```

- every
    
    与some方法相反，
    
    如果数组中检测到有一个元素不满足，则整个表达式返回 _false_ ，且剩余的元素不会再进行检测。
    
    如果所有元素都满足条件，则返回 true。
    

```JavaScript
let a = [1,20,30,40]
let b = a.every(item => {
    return item > 8
})
console.log(b) // false
```

- join
    
    将array数据中每个元素都转为[字符串](https://so.csdn.net/so/search?q=%E5%AD%97%E7%AC%A6%E4%B8%B2&spm=1001.2101.3001.7020)，用自定义的连接符分割
    

```JavaScript
let s = Array('a','p','p','l','e')
let b = s.join('')
console.log(b) // apple
```

- push / pop
    
    数组末尾添加和删除
    
    改变原数组
    

```JavaScript
let a = Array('a','p','p','l','e')
a.push('x')
console.log(a)  // ["a","p","p","l","e","x"]
let c = Array('a','p','p','l','e')
c.pop()
console.log(c) //  ["a","p","p","l"]
```

- unshift / shift
    
    头部添加和删除
    
    改变原数组
    

```JavaScript
let a = Array('a','p','p','l','e')
a.unshift('x')
console.log(a) // ["x","a","p","p","l","e"]
let c = Array('a','p','p','l','e')
c.shift()
console.log(c) // ["p","p","l","e"]
```

- sort / reverse
    
    排序与反转，改变原数组
    

```JavaScript
var a = ["a","e","d","b","c"];  //定义数组
a.sort();  //按字母顺序对元素进行排序
console.log(a);  //返回数组[a,b,c,d,e]

var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.reverse(); 
console.log(fruits); //["Mango","Apple","Orange","Banana"]

```

- concat
    
    连接数组，不影响原数组，浅拷贝
    
    返回一个新数组
    

```JavaScript
let a = [1,2]
let b = [3,4]
let c = a.concat(b)
console.log(c) //[1,2,3,4]
```

- slice(start, end)
    
    返回截断后的新数组，不改变原数组
    
    返回一个新数组
    

```JavaScript
let a = ['a','b','c','d']
let c = a.slice(1,2)
console.log(c) // ["b"]

console.log(a.slice(-2)) // ['c', 'd']
```

- splice(start, number, value...)
    
    对js中的[数组](https://so.csdn.net/so/search?q=%E6%95%B0%E7%BB%84&spm=1001.2101.3001.7020)进行操作，包括删除，添加，替换等。
    
    改变原数组
    

```JavaScript
//删除功能，第一个参数为第一项位置，第二个参数为要删除几个
let a = ['a','b','c','d']
let b = a.splice(1,2)
console.log(a) //["a","d"]
console.log(b) //["b","c"] 原数组被删除内容

//插入功能， 第一个参数（插入位置），第二个参数（0），第三个参数（插入的项）
a.splice(1,0,'x')
console.log(a) //["a","x","b","c","d"]

//.替换功能， 第一个参数（起始位置），第二个参数（删除的项数），第三个参数（插入任意数量的项）
let a = ['a','b','c','d']
let b = a.splice(1, 1, "x")
console.log(a) //["a","x","c","d"]
console.log(b) //["b"] 被替换项

```

- indexOf / lastIndexOf(value, fromIndex)
    
    查找数组项，返回对应的下标，第一次出现/最后出现的位置
    

```JavaScript
let a = ['a','b','c','d','b']
let x = a.indexOf('b')
console.log(x) //1

let y = a.lastIndexOf('b')
console.log(y) //4
```

- reduce / reduceRight(fn(prev, cur, index, arr)， init )
    
    参数：
    
    - prev 必需。累计器累计回调的返回值; 表示上一次调用回调时的返回值，或者初始值 init;
    - cur 必需。表示当前正在处理的数组元素；
    - index 可选。表示当前正在处理的数组元素的索引，若提供 init 值，则起始索引为- 0，否则起始索引为1；
    - arr 可选。表示原数组
    - init 可选。表示初始值。

```JavaScript
let arr = [1,2,3,4,5]
console.log(arr.reduce((a,b) => a + b))  // 15
console.log(arr.reduce((a,b) => a * b))  // 120

function getGeyao(total, num) {
    return total + num;
}
console.log(arr.reduceRight(getGeyao)) // 15
//reduceRight() 方法的功能和 reduce() 功能是一样的，不同的是
//reduceRight() 从数组的末尾向前将数组中的数组项做累加。


```

### 6. 闭包

概念：闭包是指有权访问另一个函数作用域中变量的函数

在js中，属于函数作用域的变量，在函数执行完之后，函数作用域就会被清理，内存也会被回收，但是闭包是建立在一个函数内部的子函数，由于可以访问上级作用域的原因，即使上级函数执行完了也不会随之销毁，这时子函数，也就是闭包，拥有访问上级作用域中变量的权力，即使上级函数执行完后作用域内的值也不会被销毁。

#### 优点：私有化数据，在私有化数据的基础上保持数据，

#### 缺点：使用不恰当会导致内存泄漏，在不需要用到的时候及时把变量置为null

#### 应用：**闭包的应用是非常广泛的，比方我们常见的节流，防抖**中也有用到

- 7. 作用域
    
    #### 简单来说，**作用域** 指程序中定义变量的区域，它决定了当前执行代码对变量的访问权限。
    
    - **全局作用域**：全局作用域为程序的最外层作用域，一直存在。
    - **函数作用域**：函数作用域只有函数被定义时才会创建，包含在父级函数作用域 / 全局作用域内。

### 8. 原型和原型链

- 1.关于原型对象prototype
    
    在js中，每个函数类型的数据都有一个属性prototype，这个属性指向一个对象 ,也就是我们说的原型对象，原型对象上存放了实例的公用的方法和属性
    
    而且对于原型对象来说，它有一个属性constructor,它指向它的构造函数
    
    ![](https://secure2.wostatic.cn/static/dkALHzeRvycbXov6KFPVDA/image.png)
    
- 2.关于原型链
    
    构造函数new出一个实例时，实例身上会有一个__proto__属性，__proto__属性指向自己构造函数的prototype
    
    ![](https://secure2.wostatic.cn/static/pho2cUgWAYt8GeTVLzva9g/image.png)
    
    原型对象也是一个对象，它自己也有一个__proto__属性，原型对象的构造函数是js内置的Object()函数，所以原型对象的__proto__指向Object().prototype，
    
    ![](https://secure2.wostatic.cn/static/28sh7vcRAnd8Fr5EsqqwG2/image.png)
    
    而Object().prototype也有自己的__proto__，只不过Object().prototype.__proto__指向的是null
    
    所以，如果某个对象查找属性，自己和原型对象prototype上都没有的话，它就会通过原型对象中__proto__属性，去自己的构造函数的原型对象prototype上去找，最深可以到Object()函数的原型对象prototype中去查找，要是还找不到的话，就没有更上一层了，因为更上一层的话是null，因此会返回undefined
    
    ![](https://secure2.wostatic.cn/static/eaaazfn9kmiCgccUk5AzNy/image.png)
    
- 3.函数也是对象
    
    在js中函数也是一种对象，所以函数都有一个__proto__属性，而且在js中所有函数可以看作是Function()的实例，所以函数的__proto__属性会指向Function().prototype，包括Obejct().**proto**，并且Function()函数不仅仅是这些函数的构造函数，也是自己的构造函数，也就是说，Function().**proto** = Function().prototype
    
    ![](https://secure2.wostatic.cn/static/eJMgFQypLTAFNESWSfF1My/image.png)
    

---

相关知识点： 1. new关键字

---

参考文章：

[https://blog.csdn.net/weixin_56505845/article/details/119683904](https://blog.csdn.net/weixin_56505845/article/details/119683904)

- 9. 防抖debounce，节流throttle
    
    [https://juejin.cn/post/7016502001911463950](https://juejin.cn/post/7016502001911463950)
    
    #### 防抖函数：多次点击，在一段时间内只有最后一次生效
    

```JavaScript
function debounce(fun, time){
    let timer
    return function() {
        clearTimeout(timer)        // 清除之前定时器
        let args = arguments       // 参数
        timer = setTimeout(() => { // 设置定时器，延迟回调
            fun.apply(this, args)  // 在定时器中this指向window，利用apply改变this指向
        }, time)
    }
}
```

#### 节流函数：在一段时间内只能触发一次

```JavaScript
function throttle(fun, time) {
    let t1 = 0                         // 设置初始时间
    return function () {
        let t2 = new Date()            // 获取当前时间
        if (t2 - t1 > time) {          // 如果经过时间大于设置时间，则执行
            fun.apply(this, arguments) // 在定时器中this指向window，利用apply改变this指向
        }
    }
} 
```

### 10. call, apply, bind

在js中改变this的指向有两种：

#### 相同点：

```
三者都是用来改变函数的上下文，也就是this指向的。
```

#### 不同点：

```
fn.bind： 不会立即调用，而是返回一个绑定后的新函数。
```

fn.call：立即调用，返回函数执行结果，this指向第一个参数，后面可有多个参数，并且这些都是fn函数的参数。

fn.apply：立即调用，返回函数的执行结果，this指向第一个参数，第二个参数是个数组，这个数组里内容是fn函数的参数。

- 11. Promise
    
    一个promise是对一个异步操作的封装，异步操作有等待完成、成功和失败三种可能的结果，对应了promise的三种状态。then的链式调用解决了回调地狱的问题。
    

### 12. new关键字

大概的内容： 1. 新建一个空对象 2. 获取构造函数 3. 建立原型链关系 4. 执行调用构造函数的方法 5. 返回对象

#### 1. 新建一个空对象

```JavaScript
let obj = {}
```

#### 2. 获取构造函数

```
构造函数和参数一起作为参数传入我们自己定义的函数中，所以通过argument去获取，但是我们需要获取argument中第一个参数，也就是构造函数
```

```JavaScript
let myFunction = [].shift.call(arguments)
```

#### 3. 建立原型链关系

```
让子函数的__proto__指向构造函数的原型对象prototype
```

```JavaScript
obj.__proto__ = myFunction.prototype
```

#### 4.执行调用构造函数的方法

```
使用call将构造函数的this指向obj，这样新对象obj可以访问构造函数中的方法和属性，并且执行，也就是说，在新对象obj的作用域中执行构造函数，将结果赋给res
```

```JavaScript
let res = myFunction.call(obj,arguments)
```

#### 5. 返回对象

```
如果结果res是一个对象，则直接返回res，否则就返回新对象obj
```

```JavaScript
return typeof res === 'object' ? res : obj 
```

#### 完整代码

```JavaScript
function myNew () {
  let obj = {}
  let myFunction = [].shift.call(arguments)
  obj.__proto__ = myFunction.prototype
  let res = myFunction.call(obj, arguments)
  return typeof res === 'object' ? res : obj
}
```

---

关联知识点： 1. call , apply, bind函数 2. 原型和原型链 3. this相关

### 13. for...in和for...of的区别

#### for...in:

```
会在在原型链上去查找，性能差

获取对象的键名
```

#### for...of:

```
只会遍历当前对象

获取对象的键值
```