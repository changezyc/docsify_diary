# CSS场景题

## 一、元素水平垂直居中的方法有哪些？如果元素不定宽高呢？

### 块级元素居中布局

实现元素水平垂直居中的方式：

1. 利用定位+margin:auto

2. 利用定位+margin:负值

3. 利用定位+transform

4. flex布局

5. grid布局

其中，不知道元素宽高大小仍能实现水平垂直居中的方法有：

1. 利用定位+margin:auto

2. 利用定位+transform

3. flex布局

4. grid布局

而且根据元素标签的性质，可以分为：内联元素居中布局、块级元素居中布局，总结如下：

### 内联元素居中布局

- 水平居中
1. 行内元素可设置：text-align: center

2. flex布局设置父元素：display: flex; justify-content: center
- 垂直居中
1. 单行文本父元素确认高度：line-height设为height一样

2. 多行文本父元素确认高度：disaply: table-cell; vertical-align: middle

具体方法如下：

#### 1.利用定位+margin:auto

```html
<style>
    .father{
        width:500px;
        height:300px;
        border:1px solid #0a3b98;
        position: relative;
    }
    .son{
        width:100px;
        height:40px;
        background: #f0a238;
        position: absolute;
        top:0;
        left:0;
        right:0;
        bottom:0;
        margin:auto;
    }
</style>
<div class="father">
    <div class="son"></div>
</div>
```

分析：父级设置为相对定位，子级绝对定位 ，并且四个定位属性的值都设置了0，那么这时候如果子级没有设置宽高，则会被拉开到和父级一样宽高。这里子元素设置了宽高，所以宽高会按照我们的设置来显示，但是实际上子级的虚拟占位已经撑满了整个父级，这时候再给它一个`margin：auto`它就可以上下左右都居中了。

#### 2. 利用定位+margin:负值/transform属性的translate值

```html
<style>
      .father {
        position: relative;
        width: 200px;
        height: 200px;
        background: skyblue;
      }

      .son {
        position: absolute;
        top: 50%;
        left: 50%;
        /* margin-left: -50px;
        margin-top: -50px; 
        这两句和下一句作用一样*/
        transform: translate(-50%, -50%);
        width: 100px;
        height: 100px;
        background: red;
      }
</style>
<div class="father">
    <div class="son"></div>
</div>
```

### 3.flex布局

```html
<style>
    .father {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 200px;
        height: 200px;
        background: skyblue;
    }
    .son {
        width: 100px;
        height: 100px;
        background: red;
    }
</style>
<div class="father">
    <div class="son"></div>
</div>
```

### 4.grid布局

```html
<style>
       .father {
            display: grid;
            align-items:center;
            justify-content: center;
            width: 200px;
            height: 200px;
            background: skyblue;

        }
        .son {
            width: 10px;
            height: 10px;
            border: 1px solid red
        }
</style>
<div class="father">
    <div class="son"></div>
</div>
```

## 二、如何实现两栏布局，右侧自适应？三栏布局中间自适应呢？

#### 两栏布局

两栏布局实现效果就是将页面分割成左右宽度不等的两列，宽度较小的列设置为固定宽度，剩余宽度由另一列撑满。

#### 三栏布局

三栏布局按照左中右的顺序进行排列，通常中间列最宽，左右两列次之。（如github网站）

### 两栏：

双栏布局非常常见，往往是以一个定宽栏和一个自适应的栏并排展示存在，实现思路也非常的简单：

首先假设body内容中有：

```html
<div class="box">
    <div class="left">左边</div>
    <div class="right">右边</div>
</div>
```

#### 1.使用浮动float

左侧浮动 float: left，右侧可以是margin-left，float: left和calc。

```css
.left {
    float: left;
    width: 200px;
    background-color: gray;
    height: 400px;
}
.right {
    margin-left: 200px;
    background-color: lightgray;
    height: 200px;
}
```

#### 2.使用flex布局

```css
      .box {
        display: flex;
      }

      .left {
        width: 200px;
        background-color: gray;
        height: 400px;
      }

      .right {
        background-color: lightgray;
        flex: 1;
      }
```

#### 3.使用calc

```css
      .left {
        display: inline-block;
        width: 200px;
        background-color: gray;
        height: 400px;
      }

      .right {
        display: inline-block;
        background-color: lightgray;
        width: calc(100% - 205px);
      }


```

#### 4.使用grid布局

```css
      .box {
        display: grid;
        grid-template-columns: 200px 1fr;
      }

      .left {
        background-color: gray;
        height: 300px;
      }

      .right {
        background-color: lightgray;
      }
```

### 三栏布局

接下来将从这几点将实现三栏布局：（都有缺陷，所以建议记住flex就好）

1. 两边使用 float，中间使用calc

2. 定位方式

3. flex实现

4. grid实现

上面4种方式都有缺陷，有一种比较完美的解决方案可以实现所有浏览器的三栏布局（也称这种方案为圣杯布局或者双飞翼布局）。

### 圣杯布局

为了方便理解，圣杯布局的body内容也写在下方，因为从理解上它是先写mid部分的：

```html
    <style>
      html,
      body,
      .outer {
        height: 100%;
        margin: 0;
      }

      .outer {
        background-color: #333;
        margin: 0 200px 0 150px;
      }

      .inner {
        position: relative;
        float: left;
        height: 100%;
      }

      .mid {
        width: 100%;
        background-color: green;
      }

      .left {
        width: 150px;
        left: -150px;
        margin-left: -100%;
        background-color: orange;
      }

      .right {
        width: 200px;
        margin-left: -200px;
        right: -200px;
        background-color: red;
      }
    </style>
    <div class="outer">
      <div class="inner mid"></div>
      <div class="inner left"></div>
      <div class="inner right"></div>
    </div>
```

### 其他方式的三栏布局(推荐记忆第一种和第三种)

首先我们定义body内容为：

```html
<div class="outer">
  <div class="left inner">左边固定宽度</div>
  <div class="mid inner">中间自适应</div>
  <div class="right inner">右边固定宽度</div>
</div>
```

#### 1.两边使用float，中间使用 calc

```css
  .left {
    width: 200px;
    height: 200px;
    float: left;
    background: coral;
  }
  .right {
    width: 120px;
    height: 200px;
    float: right;
    background: lightblue;
  }
  .mid {
    float: left;
    height: 200px;
    width: calc(100% - 320px);
    background: lightpink;
  }
```

#### 2.定位方式

```css
  .outer {
    position: relative;
  }
  .inner {
    position: absolute;
    top: 0;
    height: 300px;
    background-color: orange;
  }
  .left {
    left: 0;
    width: 300px;
  }
  .right {
    right: 0;
    width: 300px;
  }
  .mid {
    left: 300px;
    right: 300px;
    background-color: skyblue;
  }
```

#### 3.flex方式

```css
  .outer {
    display: flex;
  }
  .inner {
    width: 300px;
    height: 300px;
    background-color: orange;
  }
  .mid {
    flex: 1;
    background-color: skyblue;
  }
```

#### 4.grid方式

```css
  .outer {
    display: grid;
    grid-template-rows: 300px;
    grid-template-columns: 300px auto 300px;
  }
  .inner {
    background-color: orange;
  }
  .mid {
    background-color: skyblue;
  }


```

## 三、如何实现单行/多行文本溢出的省略样式？

### 单行文本：

较为简单，实现如下：

```html
<style>
  p {
    width: 200px;
    border: 1px solid #000;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
</style>
<p>
  文本溢出，呈现小圆点样式。
  文本溢出，呈现小圆点样式。
  文本溢出，呈现小圆点样式。
  文本溢出，呈现小圆点样式。
  文本溢出，呈现小圆点样式。
</p>
```

分析：`overflow`设为`hidden`，普通情况用在块级元素的外层隐藏内部溢出元素，或者配合下面两个属性实现文本溢出省略。
`white-space:nowrap`，作用是设置文本不换行，一般来说这个属性只用得到`nowrap`这个值，所以只需要记住就行，这个属性其他的值不用知道。

`text-overflow`属性值有如下：

- `clip`：当对象内文本溢出部分裁切掉

- `ellipsis`：当对象内文本溢出时显示省略标记（...）

### 多行文本：

#### 解法一：

首先`white-space:nowrap`明显不适用于多行文本，所以`text-overflow`也不适用。那么思路如下：

注意，`background-image`和`background`都可，因为浏览器默认这个小圆点是img，透明度越小那么看起来就越白。实现原理很好理解，就是通过伪元素绝对定位到行尾并遮住文字，再通过`overflow: hidden`隐藏多余文字。这种实现具有以下优点：

- 兼容性好，对各大主流浏览器有好的支持

- 响应式截断，根据不同宽度做出调整

而且一般文本存在英文的时候，可以设置`word-break: break-all`使一个单词能够在换行时进行拆分。

CSS `linear-gradient()` 函数用于创建一个表示两种或多种颜色线性渐变的图片。其结果属于`<gradient>`数据类型，是一种特别的`<image>`数据类型。

```css
p {
    position: relative;
    width: 200px;
    height: 210px;
    line-height: 70px;
    border: 1px solid #000;
    overflow: hidden;
}
p::after {
    position: absolute;
    bottom: 0;
    right: 0;
    padding: 0 20px 0 10px;
    content: ". . .";
    background-image: linear-gradient(to right, transparent, #fff );
    或者简单一点就是写成：
    background: #fff;
}
```

#### 解法二：

原理如下：

1.-webkit-line-clamp: 2是用来限制在一个块元素显示的文本的行数，为了实现该效果，它需要组合其他的WebKit属性

2.display: -webkit-box：和1结合使用，将对象作为弹性伸缩盒子模型显示

3.-webkit-box-orient: vertical：和1结合使用 ，设置或检索伸缩盒对象的子元素的排列方式

4.overflow: hidden：文本溢出限定的宽度就隐藏内容

5.text-overflow: ellipsis：多行文本的情况下，用省略号"…"隐藏溢出范围的文本

```css
p {
    width: 400px;
    border-radius: 1px solid red;
    -webkit-line-clamp: 2;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

是不是很简单？但是这种方法使用了webkit的CSS属性扩展，所以兼容浏览器范围是PC端的webkit内核的浏览器，由于移动端大多数是使用webkit，所以移动端常用该形式。PC端基于webkit内核的常见浏览器有：Google Chrome，Safari等。注意火狐浏览器不是，Firefox是基于Gecko内核的。

## 四、CSS如何画一个三角形？原理是什么？

```css
  .div1 {
    width: 0;
    height: 0;
    margin: auto;
    border: 100px solid transparent;
    border-top: 100px solid #f6d375;
    /* border-left: 100px solid #a4d7e1; */
    /* border-bottom: 100px solid #ed1250; */
    /* border-right: 100px solid #414141; */
  }
```

需要哪个方向就把哪个方向的三角形解注释就行，上面的例子就把上方的三角形留下了。


