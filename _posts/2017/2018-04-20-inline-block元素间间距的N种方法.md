---
layout: post
title: 去除inline-block元素间间距的N种方法
category: CSS
tags: [css]
---


## 现象描述

真正意义上的inline-block水平呈现的元素间，换行显示或空格分隔的情况下会有间距，很简单的个例子：

`<input /> <input type="submit" />`

我们使用CSS更改非inline-block水平元素为inline-block水平，也会有该问题


### 使用word-spacing
```
.space {
    word-spacing: -6px;
}
.space a {
    word-spacing: 0;
}
```
ps: 如果您使用Chrome浏览器，可能看到的是间距依旧存在。确实是有该问题，原因我是不清楚，不过我知道，可以添加`display: table`;或`display:inline-table`;让Chrome浏览器也变得乖巧。

```
.space {
    display: inline-table;
    word-spacing: -6px;
}
```


### 使用font-size:0

```
.space {
    font-size: 0;
}
.space a {
    font-size: 12px;
}
```
这个方法，基本上可以解决大部分浏览器下`inline-block`元素之间的间距(IE7等浏览器有时候会有1像素的间距)。不过有个浏览器，就是Chrome, 其默认有最小字体大小限制，因为，考虑到兼容性，我们还需要添加：
类似下面的代码：

```
.space {
    font-size: 0;
    -webkit-text-size-adjust:none;
}
```



### 使用letter-spacing

```
.space {
    letter-spacing: -3px;
}
.space a {
    letter-spacing: 0;
}
```



### 使用word-spacing
```
.space {
    word-spacing: -6px;
}
.space a {
    word-spacing: 0;
}
```


### 使用margin负值

```
.space a {
    display: inline-block;
    margin-right: -3px;
}
```



### 其他成品方法(1)

下面展示的是YUI 3 CSS Grids 使用`letter-spacing`和`word-spacing`去除格栅单元见间隔方法（注意，其针对的是`block`水平的元素，因此对IE8-浏览器做了hack处理）：

```
.yui3-g {
    letter-spacing: -0.31em; /* webkit */
    *letter-spacing: normal; /* IE < 8 重置 */
    word-spacing: -0.43em; /* IE < 8 && gecko */
}

.yui3-u {
    display: inline-block;
    zoom: 1; *display: inline; /* IE < 8: 伪造 inline-block */
    letter-spacing: normal;
    word-spacing: normal;
    vertical-align: top;
}
```



### 其他成品方法(2)

以下是一个名叫RayM的人提供的方法：
```
li {
    display:inline-block;
    background: orange;
    padding:10px;
    word-spacing:0;
    }
ul {
    width:100%;
    display:table;  /* 调教webkit*/
    word-spacing:-1em;
}

.nav li { *display:inline;}
```



