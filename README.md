## FOR INTERVIEW



### React

#### 1. React / Vue 项目时为什么要在列表组件中写 key，其作用是什么？

​	key 帮助 React 识别哪些元素改变了，比如被添加或删除，通常，我们使用数据中的 id 来作为元素的 key。如果你选择不指定显式的 key 值，那么 React 将默认使用索引用作为列表项目的 key 值。

[如果你选择不指定显式的 key 值，那么 React 将默认使用索引用作为列表项目的 key 值。](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)

### 2.React 中 setState 什么时候是同步的，什么时候是异步的

1、由 React 控制的事件处理程序，以及生命周期函数调用 setState 不会同步更 新 state 。 2、React 控制之外的事件中调用 setState 是同步更新的。比如原生 js 绑定的事 件，setTimeout/setInterval 等。

准确的说都是同步的 只是在 react 处理的事件中 做了类似assign 的事情 ，导致看上去像是异步。



### JS

#### 1.什么是防抖和节流？有什么区别？如何实现？

```
防抖——触发高频事件后 n 秒后函数只会执行一次，如果 n 秒内高频事件再次被触发，则重新计算时间
```

```javascript
// 防抖 3s

function debounce(fn) {
    let timer

    return function() {
        clearTimeout(timer)
        timer =  setTimeout(() => {
            fn.apply(this, arguments)
        }, 3 * 1000);
    }
}

function hello(){
    console.log('say hello')
}

let debounced = debounce(hello)

setInterval(()=>{
    debounced()
}, 1000)
```

```text
节流——高频事件触发，但在 n 秒内只会执行一次，所以节流会稀释函数的执行频率。
```

```javascript
// 节流 3s

function throttle(fn) {
    let open = true
    return function() {
        if(!open){
            return
        }
        open = false
        setTimeout(() => {
            fn.apply(this, arguments)
            open = true
        }, 3 * 1000);
    }
}

function hello(){
    console.log('say hello')
}

let throttled = throttle(hello)

setInterval(()=>{
    throttled()
}, 1000)
```

## 基础

### 1.介绍下 Set、Map、WeakSet 和 WeakMap 的区别？

Set——对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用 WeakSet——成员都是对象；成员都是弱引用，可以被垃圾回收机制回收，可以 用来保存 DOM 节点，不容易造成内存泄漏； Map——本质上是键值对的集合，类似集合；可以遍历，方法很多，可以跟各 种数据格式转换。 WeakMap——只接受对象最为键名（null 除外），不接受其他类型的值作为键 名；键名是弱引用，键值可以是任意的，键名所指向的对象可以被垃圾回收， 此时键名是无效的；不能遍历，方法有 get、set、has、delete。

### 2.es6/ es5 继承的区别

### 3.从输入url到获得页面经历的所有事情

[详细内容](https://zhuanlan.zhihu.com/p/133906695)



## 算法

### 1.深度优先遍历

```javascript
function deepTraversal(node , nodeList){

    if(node){
        nodeList.push(node)
        const children = node.children

        for (let index = 0; index < children.length; index++) {
            const element = children[index];
            deepTraversal(element, nodeList)
        }
    }
    return nodeList
}
```

### 2.广度优先遍历

```javascript
function wideTraversal(node){
    let result = []
    let queue = []

    if(node){
        queue.push(node)

        while(queue.length){
            const item = queue.shift()
            result.push(item)
            for (let index = 0; index < item.children.length; index++) {
                const element = item.children[index];
                queue.push(element)
            }
        }
    }

    return  result
}

```

### 3.请分别用深度优先思想和广度优先思想实现一个拷贝函数？