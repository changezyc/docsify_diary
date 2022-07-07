## 一、Vue的原地复用是什么？

原地复用”是指Vue会尽可能复用DOM，尽可能不发生DOM的移动。Vue在判断更新前后指针是否指向同一个节点，其实不要求它们真实引用同一个DOM节点，实际上它仅判断指向的是否是同类节点（比如2个不同的div，在DOM上它们是不一样的，但是它们属于同类节点），如果是同类节点，那么Vue会直接复用DOM，这样的好处是不需要移动DOM。再看上面的diff实例，假如10个节点都是div，那么整个diff过程中就没有移动DOM的操作了。

接下来讲diff的过程：

## 二、路由守卫的原理。

## 三、computed和watch区别？

场景不同

- computed用于计算产生新的数据

- watch用于监听现有数据

另外，computed有缓存，method没有缓存，所以数据的计算多用computed而不是放在method里面。

## 四、vue的通讯方式？

- props和$emit

- 自定义事件(事件总线)

- provide/inject

- Vuex

- $attrs

- $parent

- $refs

## 五、vuex的mutation和action的区别？

mutation:是原子操作，必须同步代码

action:可包含多个mutation，可包含异步代码

## 六、vdom真的很快吗？

vdom并不快，JS直接操作理论上更快。

使用vdom因为“数据驱动视图”要有合适的技术方案，不能全部DOM重建。

所以vdom是目前比较合适的技术解决方案。

## 七、vue每个生命周期都做了什么？（不要眼高手低）

### beforeCreate

创建一个空白的vue实例，data、method尚未被初始化。

### created

vue实例初始化完成，完成响应式绑定，data、method已经初始化完成，可调用。但是尚未开始渲染模板。

### beforeMount

编译模板，调用render生成vdom，但还没有把vdom转化成dom，就是还没有渲染DOM。

### mounted

完成DOM渲染，组件创建完成，开始由“创建阶段”进入“运行阶段”

### beforeUpdate

### updated

### beforeUnmount

### unmounted
