---
layout: post
title: CSS Grid Layout规范中的minmax()函数
category: CSS
tags: [css]
---

CSS Grid Layout规范中的minmax()函数是一个非常有用的新特性。这个函数能够让我们用最简单的CSS控制网格轨道的大小。这个函数包括一个最小值和最大值。

## minmax()函数

`minmax()`函数接受两个参数，一个最小值和一个最大值。

```
minmax(min, max)
```
如果定义的最大值小于最小值，它将会被忽略，函数会被视为只设置了一个最小值。

minmax()函数接受六种类型的值：

* 长度值<length>
* 百分比值
* 弹性值
* max-content
* min-content
* auto

## Length

`minmax()`函数使用长度（length）也许是最简单的值，就是一个基本的长度。例如，这有一个简单的一行三列的网格。


[default.png](../../../../assets/images/default.png)


使用`minmax()`函数，可以指定网格中黄色单元格宽度保持在100px至200px之间。随着浏览器窗口的大小改变，这绝对值将会改变，但总是在这两个范围之内变化。

```
.grid { 
	display: grid; 
	grid-template-columns: minmax(100px, 200px) 1fr 1fr; 
}

```
[length-1.gif](../../../../assets/images/length-1.gif)


网格的第二列和第三列的收缩和扩展会根据网格容器剩余空间进行填充，但网格的第一列总是保持在100px和200px之间。



## Percentage

`minmax()`函数除了可以使用length单位之外也可以使用百分比单位。如果我们把黄色网格设置了最大值为50%。表示黄色网格最大宽度是网格容器宽度的一半，但最大值不会有小于200px的值。


[percentage.gif](../../../../assets/images/percentage.gif)


无论浏览器视窗缩到多小，黄色网格宽度都不会小于200px。但是，当网格容器有足够的空间时，黄色网格宽度始终都会是容器宽度的一半。


## 弹性长度

弹性长度是一个新的单位，它类似于`minmax()`函数，也是`CSS Grid Layout`中的一个规范。这个长度使用的是fr单位，代表网格容器自由空间。例如，假设有一个`100px`宽的网格，这个网格有两个列。一列是固定宽度`20px`，另一列的宽度是`1fr`。那么第二列有效的宽度为`80px`，因为网格内可用的剩余空间是`80px`。


目前，`fr`单位只能作用于`minmax()`函数中的最大值（尽管规范中有提到过，在未来，它可能也可以用于`minmax()`函数的最小值）。回到我们的示例中来，可以指定黄色的网格单元格最小宽度为`200px`，如果最大值设置为`1fr`，当浏览器可用空间大于`200px`，那么最大宽度将会大于`200px`。同样的另外两列的宽度也可以用`1fr`。

>当另外两两也采用了`1fr`时，加上`minmax()`函数中最大值`1fr`，这样整个可用空间分成三等份，当其宽度大于`200px`时，那么其值才会用于黄色网格，如果其值小于`200px`时，那么黄色网格的宽度始终会是`200px`。前面也说到过，当`minmax()`函数中的最大值小于最小值时，它将会被忽略。


```
.grid { 
	display: grid; 
	grid-template-columns: minmax(200px, 1fr) 1fr 1fr; 
}

```


[fr.gif](../../../../assets/images.gif)

因为视窗有足够大的空间，所以使用`1fr`单位之后，将等分网格列。


## max-content

`max-content`关键词是一个特殊的值，它代表了单元格“最理想的大小”。网格单元格最小的宽度围绕它的内容。例如，如果单元格的的内容是一个句子，理想的单元格的宽度将是整个名子的长度，无论是什么长度，单元格内容的句子都不会换行。


把之前的示例中黄色的网格的最大值和最小值都设置为`max-content`。

```
.grid { 
	display: grid; 
	grid-template-columns: minmax(max-content, max-content) 1fr 1fr; 
}

```

[max-content.gif](../../../../assets/max-content.gif)


正如我们所见，列的尺寸扩大到整个内容字符串长度。因为最大和最小值都设置了`max-content`，所以列的宽度是一样的。


## min-content

`min-content`关键词和`max-content`一样，是一种特殊的值。它代表单元格最小宽度，可以不让内容溢出单元格，除非是不可避免的。

使用上面的示例，在`minmax()`函数中的最小值和最大值都设置`min-content`，这个示例可以说明`min-content`和`max-content`之间的区别。

```
.grid { 
	display: grid; 
	grid-template-columns: minmax(min-content, min-content) 1fr 1fr; 
}

```

[min-content.gif](../../../../assets/min-content.gif)


我们可以看到，单元格的内容使用了最小宽度，将可用空间转移给其他单元格，而且内容也不会引起任何的溢出。


## auto

最后介绍`auto`值。`minmax()`函数的最小值和最大值使用`auto`，将会有不同的含义，其含义也取决于`minmax()`函数的最小值和最大值。

如果用于最大值，那么`auto`值相当于`max-content`值；如果用于最小值，那么`auto`值相当于`min-content`。最大的最小尺寸不同于`min-content`，它通过`min-width`或`min-height`来指定。

为了说明这一点，下面的的示例中，黄色的网格单元格使用`minmax()`函数，并且最小值和最大值都设置`auto`。

```
.grid { 
	display: grid; 
	grid-template-columns: minmax(auto, auto) 1fr 1fr; 
}

```

[auto.gif](../../../../assets/auto.gif)


## 使用minmax()函数：不使用媒体查询实现响应式布局

正如我们所见，有几种情况下使用minmax()函数是最合适的。但也许最流行或有用的是在不使用任何媒体查询创建响应式网页设计。

来看一个网格示例：

[responsive.gif](../../../../assets/responsive.gif)

网格中的每个列的最小宽度为200px。根据浏览器视窗大小，网格数量会根据共最合理的宽度进行变化。这里使用了CSS的minmax()函数。只需要使用两行CSS代码就可以实现：

```
.grid { 
	display: grid; 
	grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); 
}

```

除了使用`minmax()`函数之外，还有两个关键部分：

* **`repeat()`**：这个函数允许我们给网格多个列指定相同的值。它也接受两个值：重复的次娄和重复的值
* **`auto-fit`**：给`repeat()`函数使用这个关键词，来替代重复次数。这可以根据每列的宽度灵活的改变网格的列数


首先，在我看来这很重要，它只会让每一列的宽度相等。我们必须在`repeat()`函数中使用`auto-fit`，因为它可以灵活的控制网格的列数。尽管如此，在正确的使用的情况下是非常有用的技术。


## 扩展阅读


> [CSS Grid Layout: The Repeat Notation](https://alligator.io/css/css-grid-layout-repeat-notation/)

> [CSS Grid Layout: The Fr Unit](https://alligator.io/css/css-grid-layout-fr-unit/)

> [Guide to CSS Grid Layout Fr Unit](https://www.hongkiat.com/blog/css-grid-layout-fr-unit/)
