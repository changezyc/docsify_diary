# css八股题

## 一、说说你对盒模型的理解？

当对一个文档进行布局（layout）的时候，浏览器的渲染引擎会根据标准之一的 CSS 基础框盒模型（CSS basic box model），将所有元素表示为一个个矩形的盒子（box）。一个盒子由4部分组成：

### 标准盒子模型

width/height 只是内容宽/高度，不包含 padding 和 border值

```css
box-sizing: content-box
```

### 怪异盒子模型

width/height 包含了 padding和 border值

```css
box-sizing: border-box
```

## 二、CSS选择器有哪些？优先级？哪些属性可以继承？

### 选择器有哪些？

1. id选择器（#box），选择id为box的元素

2. 类选择器（.one），选择类名为one的所有元素

3. 标签选择器（div），选择标签为div的所有元素

4. 通配选择器（*），选择所有标签

5. 属性选择器
   
   ```
   [attribute] 选择带有attribute属性的元素
   [attribute=value] 选择所有使用attribute=value的元素
   [attribute~=value] 选择attribute属性包含value的元素
   [attribute|=value]：选择attribute属性以value开头的元素
   ```

6. 伪类选择器
   
   ```
   a:visited
   ```

7. 伪元素选择器
   
   ```
   p::after
   ```

8. 后代选择器（#box div），选择id为box元素内部所有的div元素

9. 直接子选择器（.one>one_1），选择父元素为.one的所有直接子代为.one_1的元素

10. 相邻兄弟选择器（.one+.two），选择紧接在.one之后的.two元素

11. 通用兄弟选择器（div ~ p），选择div后的所有p元素

12. 分组选择器（div, span），会同时选择div 或 span元素

### 优先级的计算

- 千位： 如果声明在 style 的属性（内联样式）则该位得一分。这样的声明没有选择器，所以它得分总是1000。

- 百位： 选择器中包含ID选择器则该位得一分。

- 十位： 选择器中包含类选择器、属性选择器或者伪类则该位得一分。

- 个位：选择器中包含元素（标签）、伪元素选择器则该位得一分。

`!important`可以直接提高到最高优先级

”important>内联 >ID>类|伪类|属性>标签|伪元素 >继承 >通配符”

### 属性继承

在`css`中，继承是指的是给父元素设置一些属性，后代元素会自动拥有这些属性。而且当子元素有这些属性时，则不会继承父元素的属性。

可以继承的有：

- 字体系列属性

```css
font:组合字体
font-family:规定元素的字体系列
font-weight:设置字体的粗细
font-size:设置字体的尺寸
font-style:定义字体的风格
font-variant:偏大或偏小的字体
```

- 文本系列属性

```css
text-indent:文本缩进
text-align:文本水平对齐
line-height:行高
word-spacing:增加或减少单词间的空白
letter-spacing:增加或减少字符间的空白
text-transform:控制文本大小写
direction:规定文本的书写方向
color:文本颜色
```

- 表格布局属性

```css
caption-side:定位表格标题位置
border-collapse:合并表格边框
border-spacing:设置相邻单元格的边框间的距离
empty-cells:单元格的边框的出现与消失
table-layout:表格的宽度由什么决定
```

- 列表属性

```css
list-style-type:文字前面的小点点样式
list-style-position:小点点位置
list-style:以上的属性可通过这属性集合
```

- 元素可见性、引用、光标属性

```css
visibility:
quotes:设置嵌套引用的引号类型
cursor:箭头可以变成需要的形状,比如手型
```

继承中比较特殊的点：

- a 标签的字体颜色不能被继承（因为a自带默认样式里有字体颜色）

### 无继承的属性

- display

- 文本属性：vertical-align、text-decoration

- 盒子模型的属性：宽度、高度、内外边距、边框等

- 背景属性：背景图片、颜色、位置等

- 定位属性：浮动、清除浮动、定位position等

- 生成内容属性：content、counter-reset、counter-increment

- 轮廓样式属性：outline-style、outline-width、outline-color、outline

- 页面样式属性：size、page-break-before、page-break-after

## 三、谈谈你对BFC的理解？

`BFC`（Block Formatting Context），即块级格式化上下文，它是页面中的一块渲染区域，并且有一套属于自己的渲染规则：

`BFC`目的是形成一个相对于外界完全独立的空间，让内部的子元素不会影响到外部的元素:

- 内部的盒子会在垂直方向上一个接一个的放置。

- 对于同一个BFC的俩个相邻的盒子的margin会发生重叠，与方向无关。(因为每个BFC是形成一个独立的空间)

- 默认每个元素的左外边距与包含块(containing block)的左边界相接触（从左到右），即使浮动元素也是如此。(因为每个BFC是形成一个独立的空间)

- BFC的区域不会与float的元素区域重叠。

- 计算BFC的高度时，浮动子元素也参与计算。

- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然。

### 触发BFC的条件：

有很多，只列举一些常见的：

- 浮动元素，`float`不是`none`。

- 绝对定位元素，`position`是`absolute`或者`fixed`。

- 块级元素的`overflow`不是`visible`。（是auto、scroll、hidden）

- `flex`、`grid`元素。

- `inline-block`元素。

应用场景：

清除内部浮动(解决高度塌陷)、防止margin重叠等。

无论如何，需记住`BFC`实际就是页面一个独立的容器，里面的子元素不影响外面的元素。

### BFC、IFC、GFC 和 FFC 的区别？（了解）

我们知道元素有内联元素、块级元素、行内块级元素，在页面上渲染时它们的定位，排列方式等都有所不同，就是因为它们根据内部的格式化上下文进行不同的渲染，即 BFC 和 IFC。

后面 css3 新增了 grid 布局以及 flex 布局，所以也迎来了 GFC、FFC。

符合以下条件即会生成一个IFC：

- 块级元素中仅包含内联级别元素。

形成条件非常简单，需要注意的是当IFC中有块级元素插入时，会产生两个匿名块将父元素分割开来，产生两个IFC。

##### IFC渲染规则

- 子元素水平方向横向排列，并且垂直方向起点为元素顶部。

- 子元素只会计算横向样式空间，包括【padding、border、margin】，垂直方向样式空间不会被计算，包括【padding、border、margin】。

- 在垂直方向上，子元素会以不同形式来对齐（vertical-align）。

- 能把在一行上的框都完全包含进去的一个矩形区域，被称为该行的行框（line box）。行框的宽度是由包含块（containing box）和与其中的浮动来决定。

- IFC中的“line box”一般左右边贴紧其包含块，但 float 元素会优先排列。

- IFC中的“line box”高度由 CSS 行高计算规则来确定，同个IFC下的多个 line box 高度可能会不同。

- 当 inline-level boxes 的总宽度少于包含它们的 line box 时，其水平渲染规则由 text-align属性值来决定。

- 当一个“inline box”超过父元素的宽度时，它会被分割成多个 boxes，这些 boxes 分布在多个“line box”中。如果子元素未设置强制换行的情况下，“inline box”将不可被分割，将会溢出父元素。

## 四、说说em/px/rem/vh/vw区别?

### px

px，表示像素，所谓像素就是呈现在我们显示器上的一个个小点，每个像素点都是大小等同的，所以像素为计量单位被分在了绝对长度单位中

有些人会把px认为是相对长度，原因在于在移动端中存在设备像素比，px实际显示的大小是不确定的。

这里之所以认为px为绝对单位，在于px的大小和元素的其他属性无关。

### em

em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸（`1em = 16px`）

为了简化`font-size`的换算，我们需要在css中的 body 选择器中声明`font-size=62.5%`，这就使 em 值变为`16px*62.5% = 10px`

这样`12px = 1.2em`, `10px = 1em`, 也就是说只需要将你的原来的px 数值除以 10，然后换上 em作为单位就行了

特点：

- em 的值并不是固定的.

- em 会继承父级元素的字体大小.

- em 是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸，任意浏览器的默认字体高都是 16px.

### rem

rem，相对单位，相对的只是HTML根元素font-size的值.

同理，如果想要简化font-size的转化，我们可以在根元素html中加入font-size: 62.5%.

```css
html {font-size: 62.5%;  } /*  公式16px*62.5%=10px  */ 
```

特点：

- rem单位可谓集相对大小和绝对大小的优点于一身.

- 和em不同的是rem总是相对于根元素，而不像em一样使用级联的方式来计算尺寸

### vh、vw

vw ，就是根据窗口的宽度，分成100等份，100vw就表示满宽，50vw就表示一半宽。（vw 始终是针对窗口的宽），同理，vh则为窗口的高度

这里的窗口分成几种情况：

- 在桌面端，指的是浏览器的可视区域.

- 移动端指的就是布局视口.

像vw、vh，比较容易混淆的一个单位是%，百分比宽泛的讲是相对于父元素：

- 对于普通定位元素就是我们理解的父元素.

- 对于`position: absolute;`的元素是相对于已定位的父元素.

- 对于`position: fixed;`的元素是相对于 ViewPort（可视窗口）

### 总结

- px：绝对单位，页面按精确像素展示

- em：相对单位，基准点为父节点字体的大小，如果自身定义了font-size按自身来计算，整个页面内1em不是一个固定的值

- rem：相对单位，可理解为root em, 相对根节点html的字体大小来计算

- vh、vw：主要用于页面视口大小布局，在页面布局上更加方便简单

## 五、css中，有哪些方式可以隐藏页面元素？区别?

通过css实现隐藏元素方法有如下：

- display:none

元素本身占有的空间就会被其他元素占有，也就是说它会导致浏览器的重排和重绘

消失后，自身绑定的事件不会触发，也不会有过渡效果

特点：元素不可见，不占据空间，无法响应点击事件

- visibility:hidden

从页面上仅仅是隐藏该元素，DOM结果均会存在，只是当时在一个不可见的状态，不会触发重排，但是会触发重绘。

给人的效果是隐藏了，所以他自身的事件不会触发

特点：元素不可见，占据页面空间，无法响应点击事件

- opacity:0

`opacity`属性表示元素的透明度，将元素的透明度设置为0后，在我们用户眼中，元素也是隐藏的

不会引发重排，一般情况下也会引发重绘。opacity在0和1的变化中会引起render层的生成和销毁，因此会引发一次回流（重排），从而引发重绘。如果opacity在0-0.9间变化则只会引发重绘。

*如果利用 animation 动画，对 opacity 做变化（animation会默认触发GPU加速），则只会触发 GPU 层面的 composite，不会触发重绘*

由于其仍然是存在于页面上的，所以他自身的的事件仍然是可以触发的，但被他遮挡的元素是不能触发其事件的

需要注意的是：其子元素不能设置opacity来达到显示的效果

特点：改变元素透明度，元素不可见，占据页面空间，可以响应点击事件

- 设置height、width模型属性为0

将元素的`margin`，`border`，`padding`，`height`和`width`等影响元素盒模型的属性设置成0，如果元素内有子元素或内容，还应该设置其`overflow:hidden`来隐藏其子元素.特点：元素不可见，不占据页面空间，无法响应点击事件

```css
.hiddenBox {
    margin:0;     
    border:0;
    padding:0;
    height:0;
    width:0;
    overflow:hidden;
}
```

- position:absolute

将元素移出可视区域，特点：元素不可见，不影响页面布局

```css
.hide {
   position: absolute;
   top: -9999px;
   left: -9999px;
}
```

- clip-path

通过裁剪的形式，特点：元素不可见，占据页面空间，无法响应点击事件

```css
.hide {
  clip-path: polygon(0px 0px,0px 0px,0px 0px,0px 0px);
}
```

最常用的还是display:none和visibility:hidden，其他的方式只能认为是奇招，它们的真正用途并不是用于隐藏元素，所以并不推荐使用它们。

#### 关于display: none、visibility: hidden、opacity: 0的区别，如下表所示：

|             | display: none | visibility: hidden | opacity: 0 |
| ----------- | ------------- | ------------------ | ---------- |
| 页面中         | 不存在           | 存在                 | 存在         |
| 重排          | 会             | 不会                 | 不会         |
| 重绘          | 会             | 会                  | 不一定        |
| 自身绑定事件      | 不触发           | 不触发                | 可触发        |
| transition  | 不支持           | 支持                 | 支持         |
| 子元素可复原      | 不能            | 能                  | 不能         |
| 被遮挡的元素可触发事件 | 能             | 能                  | 不能         |

## 六、怎么理解回流（重排）跟重绘？什么场景下会触发？

在HTML中，每个元素都可以理解成一个盒子，在浏览器解析过程中，会涉及到回流与重绘：

回流(重排)：布局引擎会根据各种样式计算每个盒子在页面上的大小与位置

重绘：当计算好盒模型的位置、大小及其他属性后，浏览器根据每个盒子特性进行绘制

![](https://static.vue-js.com/2b56a950-9cdc-11eb-ab90-d9ae814b240d.png)

具体的浏览器解析渲染机制如上图所示：

- 解析HTML，生成DOM树，解析CSS，生成CSSOM树

- 将DOM树和CSSOM树结合，生成渲染树(Render Tree)

- Layout(回流/重排):根据生成的渲染树，进行回流(Layout)，得到节点的几何信息（位置，大小）

- Painting(重绘):根据渲染树以及回流得到的几何信息，得到节点的绝对像素

- Display:将像素发送给GPU，展示在页面上

在页面初始渲染阶段，回流不可避免的触发，可以理解成页面一开始是空白的元素，后面添加了新的元素使页面布局发生改变

当我们对 DOM 的修改引发了 DOM几何尺寸的变化（比如修改元素的宽、高或隐藏元素等）时，浏览器需要重新计算元素的几何属性，然后再将计算的结果绘制出来。

当我们对 DOM的修改导致了样式的变化（color或background-color），却并未影响其几何属性时，浏览器不需重新计算元素的几何属性、直接为该元素绘制新的样式，这里就仅仅触发了回流。

### 回流触发时机

回流这一阶段主要是计算节点的位置和几何信息，那么当页面布局和几何信息发生变化的时候，就需要回流，如下面情况：

- 添加或删除可见的DOM元素

- 元素的位置发生变化

- 元素的尺寸发生变化（包括外边距、内边框、边框大小、高度和宽度等）

- 内容发生变化，比如文本变化或图片被另一个不同尺寸的图片所替代

- 页面一开始渲染的时候（这避免不了）

- 浏览器的窗口尺寸变化（因为回流是根据视口的大小来计算元素的位置和大小的）

还有一些容易被忽略的操作：获取一些特定属性的值

?> `offsetTop、offsetLeft、 offsetWidth、offsetHeight、scrollTop、scrollLeft、scrollWidth、scrollHeight、clientTop、clientLeft、clientWidth、clientHeight`

### 重绘触发时机

触发回流一定会触发重绘

可以把页面理解为一个黑板，黑板上有一朵画好的小花。现在我们要把这朵从左边移到了右边，那我们要先确定好右边的具体位置，画好形状（回流），再画上它原有的颜色（重绘）。

除此之外还有一些其他引起重绘行为：

- 颜色的修改

- 文本方向的修改

- 阴影的修改

### 如何减少?

我们了解了如何触发回流和重绘的场景，下面给出避免回流的经验：

- 如果想设定元素的样式，通过改变元素的 class 类名 (尽可能在 DOM 树的最里层)

- 避免设置多项内联样式

- 应用元素的动画，使用 `position` 属性的 `fixed` 值或 `absolute` 值(如前文示例所提)

- 避免使用 `table` 布局，`table` 中每个元素的大小以及内容的改动，都会导致整个 `table` 的重新计算

- 对于那些复杂的动画，对其设置 `position: fixed/absolute`，尽可能地使元素脱离文档流，从而减少对其他元素的影响

- 使用css3硬件加速，可以让`transform、opacity、filters`这些动画不会引起回流重绘

- 避免使用 CSS 的 `JavaScript` 表达式

在使用`JavaScript`动态插入多个节点时, 可以使用`DocumentFragment` 创建后一次插入. 就能避免多次的渲染性能

## 七、flex布局知识点

关于flex常用的属性，我们可以划分为容器属性和容器成员属性

容器属性有：

- flex-direction

- flex-wrap

- flex-flow(是flex-direction和flex-wrap的简写形式)

- justify-content

- align-items

- align-content

容器成员属性有：

- order

- flex-grow

- flex-shrink

- flex-basis

- flex(是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto)

- align-self

容器中默认存在两条轴，主轴和交叉轴，呈90度关系。项目默认沿主轴排列，通过flex-direction来决定主轴的方向

每根轴都有起点和终点，这对于元素的对齐非常重要。

![](https://static.vue-js.com/fbc5f590-9837-11eb-ab90-d9ae814b240d.png)

### flex-direction(容器属性)

决定主轴的方向(即项目的排列方向)

```css
.container {   
    flex-direction: row | row-reverse | column | column-reverse;  
} 
```

- row（默认值）：主轴为水平方向，起点在左端

- row-reverse：主轴为水平方向，起点在右端

- column：主轴为垂直方向，起点在上沿。

- column-reverse：主轴为垂直方向，起点在下沿

![](https://static.vue-js.com/0c9abc70-9838-11eb-ab90-d9ae814b240d.png)

### flex-wrap(容器属性)

弹性元素永远沿主轴排列，那么如果主轴排不下，通过flex-wrap决定容器内项目是否可换行

- nowrap（默认值）：不换行

- wrap：换行，第一行在下方

- wrap-reverse：换行，第一行在上方（反着的）

### flex-flow(容器属性)

是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`

```css
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

### justify-content(容器属性)

定义了项目在主轴上的对齐方式

```css
.box {
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

- flex-start（默认值）：左对齐

- flex-end：右对齐

- center：居中

- space-between：两端对齐，项目之间的间隔都相等

- space-around：两个项目两侧间隔相等

- space-evenly：每个元素间隔相等

### align-items(容器属性)

定义项目在交叉轴上如何对齐

```css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

- flex-start：交叉轴的起点对齐

- flex-end：交叉轴的终点对齐

- center：交叉轴的中点对齐

- baseline: 项目的第一行文字的基线对齐

- stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度

### align-content(容器属性)

即该属性对单行弹性盒子模型无效。（即：带有 flex-wrap: nowrap）。

```css
.box {
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

- flex-start：与交叉轴的起点对齐

- flex-end：与交叉轴的终点对齐

- center：与交叉轴的中点对齐

- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布

- space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍

- stretch（默认值）：轴线占满整个交叉轴

![](https://static.vue-js.com/39bcb0f0-9838-11eb-ab90-d9ae814b240d.png)

### order(容器元素属性)

定义项目的排列顺序。数值越小，排列越靠前，默认为0。

```css
.item {
    order: <integer>;
}
```

### flex-grow(容器元素属性)

上面讲到当容器设为`flex-wrap: nowrap`，不换行的时候，容器宽度有不够分的情况，弹性元素会根据`flex-grow`来决定

定义项目的放大比例（容器宽度>元素总宽度时如何伸展）

默认为0，即如果存在剩余空间，也不放大

```css
.item {
    flex-grow: <number>;
}
```

如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）

![](https://static.vue-js.com/48c8c5c0-9838-11eb-ab90-d9ae814b240d.png)

如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍

![](https://static.vue-js.com/5b822b20-9838-11eb-ab90-d9ae814b240d.png)

弹性容器的宽度正好等于元素宽度总和，无多余宽度，此时无论`flex-grow`是什么值都不会生效

### flex-shrink(容器元素属性)

定义了项目的缩小比例（容器宽度<元素总宽度时如何收缩），默认为1，即如果空间不足，该项目将缩小

```css
.item {
    flex-shrink: <number>; /* default 1 */
}
```

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小

如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小

### flex-basis(容器元素属性)

设置的是元素在主轴上的初始尺寸，所谓的初始尺寸就是元素在`flex-grow`和`flex-shrink`生效前的尺寸

浏览器根据这个属性，计算主轴是否有多余空间，默认值为`auto`，即项目的本来大小，如设置了`width`则元素尺寸由`width/height`决定（主轴方向），没有设置则由内容决定

```css
.item {
   flex-basis: <length> | auto; /* default auto */
}
```

当设置为0的是，会根据内容撑开

它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间

?>Note: 当一个元素同时被设置了 `flex-basis` (除值为`auto`外) 和 `width` (或者在`flex-direction: column`情况下设置了`height`) , `flex-basis`具有更高的优先级。

### flex(容器元素属性)

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto

常用的有：

- flex: 1 = flex: 1 1 0%

- flex: 2 = flex: 2 1 0%

- flex: auto = flex: 1 1 auto

- flex: none = flex: 0 0 auto，常用于固定尺寸不伸缩

`flex:1` 和 `flex:auto` 的区别，可以归结于`flex-basis:0`和`flex-basis:auto`的区别

当设置为0时（绝对弹性元素），此时相当于告诉`flex-grow`和`flex-shrink`在伸缩的时候不需要考虑我的尺寸

当设置为`auto`时（相对弹性元素），此时则需要在伸缩时将元素尺寸纳入考虑

注意：建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值

### align-self(容器元素属性)

允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性

默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`

```css
.item {
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

## 八、grid布局知识点（内容太多了，考前选一两个常用的记一记就行）

```css
<div class="container">
    <div class="item item-1">
        <p class="sub-item"></p >
 </div>
    <div class="item item-2"></div>
    <div class="item item-3"></div>
</div> 
```

上述代码实例中，`.container`元素就是网格布局容器，`.item`元素就是网格的项目，由于网格元素只能是容器的顶层子元素，所以`p`元素并不是网格元素

这里提一下，网格线概念，有助于下面对`grid-column`系列属性的理解

网格线，即划分网格的线，如下图所示：

![](https://static.vue-js.com/61be7080-9a94-11eb-ab90-d9ae814b240d.png)

上图是一个 2 x 3 的网格，共有3根水平网格线和4根垂直网格线。

### 属性

关于grid常用的属性，我们可以划分为容器属性和容器成员属性

容器属性有：

容器成员属性有：

## 九、如果要做优化，CSS提高性能的方法有哪些？

面试的时候先说一句话：

#### css实现性能的方式可以从选择器嵌套、属性特性、减少http这三面考虑，同时还要注意css代码的加载顺序。具体的方法稍微记一记就行了。

实现方式有很多种，主要有如下：

- 内联首屏关键CSS

- 异步加载CSS

- 资源压缩

- 合理使用选择器

- 减少使用昂贵的属性

- 不要使用@import

### 内联首屏关键CSS

在打开一个页面，页面首要内容出现在屏幕的时间影响着用户的体验，而通过内联css关键代码能够使浏览器在下载完html后就能立刻渲染

而如果外部引用css代码，在解析html结构过程中遇到外部css文件，才会开始下载css代码，再渲染

所以，CSS内联使用使渲染时间提前

注意：但是较大的css代码并不合适内联（初始拥塞窗口、没有缓存），而其余代码则采取外部引用方式

### 异步加载CSS

在CSS文件请求、下载、解析完成之前，CSS会阻塞渲染，浏览器将不会渲染任何已处理的内容

前面加载内联代码后，后面的外部引用css则没必要阻塞浏览器渲染。这时候就可以采取异步加载的方案，主要有如下：

- 使用javascript将link标签插到head标签最后

```js
// 创建link标签
const myCSS = document.createElement( "link" );
myCSS.rel = "stylesheet";
myCSS.href = "mystyles.css";
// 插入到header的最后位置
document.head.insertBefore( myCSS, documen
t.head.childNodes[ document.head.childNodes.length - 1 ].nextSibling );
```

- 设置link标签media属性为noexis，浏览器会认为当前样式表不适用当前类型，会在不阻塞页面渲染的情况下再进行下载。加载完成后，将media的值设为screen或all，从而让浏览器开始解析CSS

```html
<link rel="stylesheet" href="mystyles.css" media="noexist" onload="this.media='all'">
```

- 通过rel属性将link元素标记为alternate可选样式表，也能实现浏览器异步加载。同样别忘了加载完成之后，将rel设回stylesheet

```html
<link rel="alternate stylesheet" href="mystyles.css" onload="this.rel='stylesheet'">
```

### 资源压缩

利用`webpack`、`gulp/grunt`、`rollup`等模块化工具，将css代码进行压缩，使文件变小，大大降低了浏览器的加载时间

### 合理使用选择器

- 不要嵌套使用过多复杂选择器，最好不要三层以上

- 使用id选择器就没必要再进行嵌套

- 通配符和属性选择器效率最低，避免使用

### 减少使用昂贵的属性

在页面发生重绘的时候，昂贵属性如`box-shadow/border-radius/filter/`透明度`/:nth-child`等，会降低浏览器的渲染性能

### 不要使用@import

`@import`会影响浏览器的并行下载，使得页面在加载时增加额外的延迟，增添了额外的往返耗时

而且多个`@import`可能会导致下载顺序紊乱

比如一个css文件`index.css`包含了以下内容：`@import url("reset.css")`

那么浏览器就必须先把`index.css`下载、解析和执行后，才下载、解析和执行第二个文件`reset.css`

### 其他

- 减少重排操作，以及减少不必要的重绘

- 了解哪些属性可以继承而来，避免对这些属性重复编写

- cssSprite，合成所有icon图片，用宽高加上backgroud-position的背景图方式显现出我们要的icon图，减少了http请求

- 把小的icon图片转成base64编码

- CSS3动画或者过渡尽量使用transform和opacity来实现动画，不要使用left和top属性

## 十、彻底搞懂clientHeight、offsetHeight、scrollHeight的区别。

图片描述：

![offset.jpeg](https://s2.loli.net/2022/07/05/CMiRqgOyJWwKTQ2.jpg)

### 1.定义说明

### clientHeight

含义：元素的像素高度，包含元素的高度+内边距，不包含水平滚动条，边框和外边距

### offsetHeight

含义：元素的像素高度 包含元素的垂直内边距和边框，水平滚动条的高度，且是一个整数

### scrollHeight

含义：元素内容的高度，包括溢出的不可见内容

### offsetLeft

含义：返回元素左上角相对于offsetParent的左边界的偏移像素值

### 注意点

1.对块级元素来说，offsetTop、offsetLeft、offsetWidth 及 offsetHeight 描述了元素相对于 offsetParent 的边界框。但是文本框不是如此.文本框的offsetLeft和offsetTop是第一个文本框的左偏移和上偏移.

2.offsetParent元素指该元素的定位元素以及最近的table,td,th,body. 可见，offsetParent和position属性的包含块概念类似.大部分场景下可以通用.

3.offsetTop和offsetLeft都是相对于其内边距边界的.

### offsetLeft和left属性的区别

**1.position为fixed时值不同** 当position为fixed的时候，offsetLeft的值将会是null,而left此时一般有确定的数字值.**2.相对边距不同** offerset的是相对于offsetParent的内边距边界，left是相对于包含块的外边距边界.**3.包含块有区别** offerset相对于定位的祖先元素或者 table/td/th/body等祖先元素,left仅仅是相对于定位祖先元素+body

### clientHeight与offsetHeight的区别

clientHeight仅仅包含内边距+高度，offsetHeight包含内边距+滚动条+边框 所以可以这样说： clientHeight+滚动条高度+边框 = offsetHeight


