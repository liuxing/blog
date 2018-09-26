---
title: CSS Grid 布局快速教程
date: 2018-08-21
---

# CSS Grid 布局快速教程

CSS Grid 布局是 CSS 中最强大的布局系统（没有之一）。说起布局，另一个方便好用的Flex布局是避不开的，与 Flex 的一维布局系统不同，CSS Grid 布局是一个二维布局系统，也就意味着它可以同时处理列和行。你可以把它想象成一个Table。本文不是一个大而全的教程，而是一个快速入门。

## 使用Grid 布局实现一个九宫格

与Flex 布局类似，Grid 布局由 **wrapper**（父元素）和 **items**（子元素）两部分组成。在介绍它的详细语法之前先来个例子: 九宫格 https://codepen.io/ogilhinn/pen/mGdQZq

![屏幕快照 2018-08-21 15.21.03](/Users/lx/Desktop/屏幕快照 2018-08-21 15.21.03.png)

代码如下：

```html
<div class="wrapper">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
  <div class="item">7</div>
  <div class="item">8</div>
  <div class="item">9</div>
</div>
```

```css
.item {
  padding: 20px;
  background: #ddd;
  text-align: center;
}

.wrapper {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;  
  grid-column-gap: 2px;
  grid-row-gap: 2px;
}
```

现在我们就得到了一个3X3的九宫格。

这儿用到了 `grid-template-columns` `grid-template-rows` 属性，这两个属性用于创建列(columns)和行(rows)。`grid-template` 是 `grid-template-rows` 和 `grid-template-columns` 的缩写形式。上面的CSS可以缩写为：

```scss
.wrapper {
  display: grid;
  grid-template: 100px 100px 100px / 100px 100px 100px;
  // 指定一些具有相同宽度的网格项会变得很乏味。repeat函数可以帮助我们。
  // grid-template: repeat(3, 100px) / repeat(3, 100px);
}
```

`grid-column-gap` `grid-row-gap`指定网格线(grid lines)的大小。你可以把它想象为设置列/行之间间距的宽度。

这些几个属性都用于网格容器即父元素。

##设置网格项（子元素）

与 Flex 一样，子元素也是可设置的，现在我们想把第一元素占据整行，修改CSS，让第一个元素从第一个网格线开始到第四的网格线结束。

```css
...
.item:first-child {
  background: #f00;
  grid-column-start: 1;
  grid-column-end: 4;
}
```

如果你不明白我们设置的只有 3 列，为什么有4条网格线呢？看下面

```diff
+-------+-------+-------+
+       +       +       +
+       +       +       + 
+-------+-------+-------+
1       2       3       4
```

当第一格占满后，剩下子元素将被挤到下一行（这儿为了好看，我们删除3个元素）。  `grid-column-start` 与 `grid-column-end` 可以缩写为``grid-column`

```css
...
.item:first-child {
  background: #f00;
  grid-column: 1 / 4;
}
```

`grid-row` 与 `grid-column` 差不多，只是行与列的差别。为了加深印象，我们来让第二个元素占满第一列，如图
![屏幕快照 2018-08-21 16.02.27](/Users/lx/Desktop/屏幕快照 2018-08-21 16.02.27.png)

```css
...
.item:nth-child(2) {
  background: #0f0;
  grid-row-start: 2;
  grid-row-end: 4;
}
```

同样，可以缩写为

```css
grid-row: 2 / 4
```

我还希望把3号元素占满剩下的灰色区域，通过上面学习几个属性我们可以很快实现这个小需求。（还是为了好看，我们再删除3个元素）

![屏幕快照 2018-08-21 16.09.32](/Users/lx/Desktop/屏幕快照 2018-08-21 16.09.32.png)

修改CSS，让3元素的行和列都设置为从第二个网格线到第四个网格线即可
```css
...
.item:nth-child(3) {
  grid-column: 2 / 4;
  grid-row: 2 / 4;
}
```

如果你觉得这样写有点麻烦，我们还有另一种缩写 `grid-area` `grid-area`属性接受4个由'/'分开的值：`grid-row-start`, `grid-column-start`, `grid-row-end`, 最后是`grid-column-end`。上例可修改为：

```css
...
.item:nth-child(3) {
  grid-area: 2 / 2 / 4 / 4;
}
```

上面的这个结构，在实际中很常见 Header, Sidebar, Main。我们可以使用 `grid-template-areas` 属性 通过引用 `grid-area` 属性指定的 网格区域(Grid Area) 名称来定义网格模板。重复网格区域的名称导致内容跨越这些单元格。一个点号（`.`）代表一个空的网格单元。这个语法本身可视作网格的可视化结构。代码如下

```html
<div class="wrapper">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```scss
.item {
  background: #ddd;
  text-align: center;
  padding: 20px;
}

.wrapper {
  width: 300px;
  height: 300px;
  display: grid;
  grid-gap: 2px;
  // 很直观的网格区域划分
  grid-template-areas: 
    "header header header"
    "sidebar main main"
    "sidebar main main";
}

.item:first-child {
  grid-area: header;
  background: #f00;
}
.item:nth-child(2) { 
  grid-area: sidebar; 
  background: #0f0;
}
.item:nth-child(3) { 
  grid-area: main; 
}
```

网格模板区域（grid-template-areas）属性提供了一个可视化的网格结构，使网格容器的整体布局更容易被理解。

除了上文介绍的网格布局外  还有一些`justify-items` `align-items` `justify-content` 之类的属性设置对齐方式，这儿就不一一举例了。