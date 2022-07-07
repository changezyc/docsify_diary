# JavaScript面试题

## 一、你知道哪些数组常用方法？你说的这些方法，哪些方法不影响原数组，哪些影响？

- 增，下面前三种是对原数组产生影响的增添方法，第四种则不会对原数组产生影响

push()

unshift()

splice()

concat() 不影响原数组

- 删，下面三种都会影响原数组，最后一项不影响原数组：

pop()

shift()

splice()

slice() 不影响原数组

- 改，即修改原来数组的内容，常用splice()

- 查，即查找元素，返回元素坐标或者元素值，所以都不会改变原数组

indexOf() 不影响原数组

includes() 不影响原数组

find() 不影响原数组

- 排序方法，数组有两个方法可以用来对元素重新排序，都会改变原数组

reverse()

sort()

- 转换方法

join() 不影响原数组

- 迭代方法，常用来迭代数组的方法（都不改变原数组）有如下：

map() 不影响原数组 

forEach() 不影响原数组

filter() 不影响原数组

some() 不影响原数组

every() 不影响原数组

- 静态方法

Array.from()   对一个类数组或可迭代对象创建一个新的，非深拷贝的数组实例

Array.isArray()   用来判断某个变量是否是一个数组对象

Array.of()   根据一组参数来创建新的数组实例，支持任意的参数数量和类型。注意：`Array.of()` 和 `Array` 构造函数之间的区别在于处理整数参数：`Array.of(7)` 创建一个具有单个元素 7 的数组，而 `Array(7)` 创建一个长度为 7 的空数组。

Array()和new Array()其实是一个意思

创建一个x * y全部为0的二维数组的方法：

!> 这个1是错的，因为第二维指向同一个引用

1. new Array(x).fill(new Array(y).fill(0))   

2. new Array(x).fill().map(() => new Array(y).fill(0))

3. Array.from(new Array(x), () => new Array(y).fill(0))
- 很重要的方法

reduce()

它和迭代方法（map、fliter、forEach）一样，会遍历数组；reduce()方法会遍历数组中的每一个元素，每遍历一次就会执行一次回调函数。当遍历完之后会将最后的结果返回出去。

reduce( )方法有两个参数，第一个参数是累加函数，第二个是函数的previousValue的初始值，有時候叫initialValue。累加函数有第四个参数分别是：previousValue，nowValue，nowIndex，arr，后两个参数为可选参数。

```js
reduce方法的示例
const arr=[1,2,3,4,5]
const newarr=arr.reduce(function(previousValue,current){ // reduce的特殊之处就在于它方法里面的形参
    console.log(previousValue+'-----'+current);
    return previousValue + current
});
console.log(newarr); //输出 15
// ----------------------------------------------------------------------------- 
const newarr1=arr.reduce(function(previousValue,current){ // reduce的特殊之处就在于它方法里面的形参
    console.log(previousValue+'-----'+current);
    return previousValue + current
},2);  // 这里的reduce有两个参数，第一个是函数、第二个是2，这里的2表示的是previousValue初始值为2,如果没有则默认为数组的第一个元素
console.log(newarr1); //输出 17
// -----------------------------------------------------------------------------
const newarr2=arr.reduce(function(previousValue,current){ // reduce的特殊之处就在于它方法里面的形参
    return previousValue * current
});
console.log(newarr2); //输出 120
// -----------------------------------------------------------------------------
let arr1 = ['name','age','long','short','long','name','name'] // 计算数组中元素出现的次数
let arrResult = arr1.reduce((pre,cur) =>{
    console.log(pre,cur)
    if(cur in pre) {
    pre[cur]++  // 理解一下为什么不可以使用pre.crr ++的形式,因为pre.crr的.crr默认表示为pre对象中一个的crr属性，且其值不可以更换  
    } else {
    pre[cur] = 1  // 这里意思是往pre对象中添加了name属性并且赋值为1
}
    return pre
},{});
console.log(arrResult) //输出{name: 3, age: 1, long: 2, short: 1} 重点理解
console.log(arrResult['name']); // 输出 3
```

## 二、字符串常用方法？

## 三、Node JS和浏览器JS的事件循环区别？

1. 浏览器端,执行宏任务前,会先去看看微任务列表里面是否有内容,如果有的话,优先把微任务列表的内容先全部执行完。
2. 接着前面的,如果微任务列表内容已经全部执行完了,还会尝试DOM渲染,也就是说如果检测到DOM树发生过变化,就去做DOM渲染,否则不做。
3. 接着前面的,如果DOM渲染完成或者无需做DOM渲染,此时才去做一这个宏任务。
   总的来说,下一个宏任务可以开始执行的必要条件是: 1. 微任务队列为空 2. DOM树没有检测到更新

微任务在下一轮页面渲染之前触发，宏任务在之后触发。

浏览器环境下，microtask 的任务队列是每个 macrotask 执行完之后执行。而在 Node.js 中，microtask 会在事件循环的各个阶段之间执行，也就是一个阶段执行完毕，就会去执行 microtask 队列的任务。可以理解成每个类别的宏任务有着对应的优先级。

而且，NodeJS中每个类别的宏微任务也有着对应的优先级。其中process.nextTick优先级最高。

macro-task(宏任务)：包括整体代码script，setTimeout，setInterval

micro-task(微任务)：Promise，process.nextTick

```js
浏览器下：
setTimeout(function() {
    console.log('setTimeout');
})
new Promise(function(resolve) {
    console.log('promise');
}).then(function() {
    console.log('then');
})
console.log('console');

//结果(没有resolve的Promise所有不打印then)
promise
console
setTimeout
```

1. 这段代码作为宏任务，进入主线程

2. 先遇到setTimeout，那么将其回调函数注册后分发到宏任务Event Queue

3. 接下来遇到了Promise，new Promise立即执行，then函数分发到微任务Event Queue

4. 遇到console.log()同步任务，立即执行

5. 好啦，整体代码script作为第一个宏任务执行结束，看看有哪些微任务？我们发现了then在微任务Event Queue里面，执行

6. ok，第一轮事件循环结束了，我们开始第二轮循环，当然要从宏任务Event Queue开始。我们发现了宏任务Event Queue
   
   setTimeout对应的回调函数，立即执行

7. 结束

### node中的事件循环

```js
setTimeout(()=>{
    console.log('timer1')
    Promise.resolve().then(function() {
        console.log('promise1')
    })
}, 0)

setTimeout(()=>{
    console.log('timer2')
    Promise.resolve().then(function() {
        console.log('promise2')
    })
}, 0)
浏览器下：timer1 promise1 timer2 promise2
Node下：timer1 timer2 promise1 promise2
```

Node.js采用V8作为js的解析引擎，而I/O处理方面使用自己设计的libuv,libuv是一个基于事件驱动的跨平台抽象层，封装了不同操作系统的一些底层特性，对外提供统一的API，事件循环机制也是它里面的实现。

根据Node.js官方介绍，每次事件循环都包含了6个阶段，对应到 libuv 源码中的实现，如下图所示：
![](https://img-blog.csdnimg.cn/5656ca7c5b954b3294b79263e47a6e29.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGlhbmdob25nX3lhbmc=,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

- timers阶段：这个阶段执行timer（setTimeOut, setInterval）的回调

- I/O callbacks阶段：执行一些系统调用错误，比如网络通信的错误回调

- idle, prepare阶段：仅node内部使用

- poll阶段：获取新的I/O事件，适当的条件下node将阻塞在这里

- check阶段：执行setImmediate()的回调

- colse callback阶段：执行socket的close事件回调

接下来我们重点看timers，poll，check这三个阶段，因为日常开发中的绝大部分任务都是在这三个阶段中处理的。

#### timers阶段

timers 是事件循环的第一个阶段，Node 会去检查有无已过期的timer，如果有则把它的回调压入timer的任务队列中等待执行，事实上，Node 并不能保证timer在预设时间到了就会立即执行，因为Node对timer的过期检查不一定靠谱，它会受机器上其它运行程序影响，或者那个时间点主线程不空闲。

#### poll阶段

poll 阶段主要有2个功能：

1. 处理 poll 队列的事件

2. 当有已超时的 timer，执行它的回调函数

even loop将同步执行poll队列里的回调，直到队列为空或执行的回调达到系统上限（上限具体多少未详），接下来even loop会去检查有无预设的setImmediate()，分两种情况：

1. 若有预设的setImmediate(), event loop将结束poll阶段进入check阶段，并执行check阶段的任务队列

2. 若没有预设的setImmediate()，event loop将阻塞在该阶段等待

注意一个细节，没有setImmediate()会导致event loop阻塞在poll阶段，这样之前设置的timer岂不是执行不了了？所以咧，在poll阶段event loop会有一个检查机制，检查timer队列是否为空，如果timer队列非空，event loop就开始下一轮事件循环，即重新进入到timer阶段。

#### check阶段

setImmediate()的回调会被加入check队列中， 从event loop的阶段图可以知道，check阶段的执行顺序在poll阶段之后。

接下来举个例子：

```js
setTimeout(()=>{
    console.log('timer1')
    Promise.resolve().then(function() {
        consle.log('promise1')
    })
}, 0)

setTimeout(()=>{
    console.log('timer2')
    Promise.resolve().then(function() {
        console.log('promise2')
    })
}, 0)

1. 全局脚本（main()）执行，将 2 个 timer 依次放入 timer 队列，main()执行完毕，调用栈空闲，任务队列开始执行；
2. 首先进入 timers 阶段，执行 timer1 的回调函数，打印 timer1，并将 promise1.then 回调放入 microtask 队列，同样的步骤执行 timer2，打印 timer2，并将 promise2.then 回调放入 microtask 队列
3. 至此，timer 阶段执行结束，event loop 进入下一个阶段之前，执行 microtask 队列的所有任务，依次打印 promise1、promise2
```

再来看一个例子加深一下理解：

```js
console.log('start')
setTimeout(() => {
  console.log('timer1')
  Promise.resolve().then(function() {
    console.log('promise1')
  })
}, 0)
setTimeout(() => {
  console.log('timer2')
  Promise.resolve().then(function() {
    console.log('promise2')
  })
}, 0)
Promise.resolve().then(function() {
  console.log('promise3')
})
console.log('end')
Node: start - end - promise3 - timer1 - timer2 - promise1 - promise2
浏览器: start - end - promise3 - timer1 - promise1 - timer2 - promise2
```

1. 一开始执行栈的同步任务（这属于宏任务）执行完毕后（依次打印出 start end，并将 2 个 timer 依次放入 timer 队列）,会先去执行微任务（这点跟浏览器端的一样），所以打印出 promise3

2. 然后进入 timers 阶段，执行 timer1 的回调函数，打印 timer1，并将 promise.then 回调放入 microtask 队列，同样的步骤执行 timer2，打印 timer2；这点跟浏览器端相差比较大，timers 阶段有几个 setTimeout/setInterval 都会依次执行，并不像浏览器端，每执行一个宏任务后就去执行一个微任务

总结NodeJS事件循环：

- 执行同步代码

- 执行微任务

- 按顺序执行那6个类型的宏任务（每个开始之前都执行当前的微任务）

## 四、JS严格模式有什么特点？

答上几个就行

全局变量必须先声明

禁止用with

创建eval作用域

禁止this指向window

函数参数不能重名

## 五、JS内存泄露如何检测？场景有哪些？

开发者工具的performance勾上memory测试。

场景：

比如Vue开发中，

被全局变量、函数引用，组件销毁时未清除。

被全局事件、定时器引用，组件销毁时未清除。

被自定义事件引用，组件销毁时未清除。

## 六、js开启多进程的方法？

浏览器JS是用WebWorker

NodeJS采用fork或者cluster,使用send和on方法来进行进程间的通信。

## 七、JS-bridge的实现原理？

url-scheme

## 八、requestIdleCallback和requestAnimationFrame有什么区别?

requestIdleCallback:空闲时才执行，低优

requestAnimationFrame:每次渲染完都会执行，高优

两个都是宏任务，因为都是要等待DOM渲染完之后才执行。
