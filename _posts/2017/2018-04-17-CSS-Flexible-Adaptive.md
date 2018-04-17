---
layout: post
title: 使用Flexible实现手淘H5页面的终端适配
category: CSS
tags: [css]
---

实现手机端移动端适配.

## lib-flexible

[lib-flexible](https://github.com/amfe/lib-flexible)是一个制作H5适配的开源库，可以[点击这里](https://github.com/amfe/lib-flexible/archive/master.zip)下载相关文件，获取需要的JavaScript和CSS文件。


也可以直接CDN

```
<script src="http://g.tbcdn.cn/mtb/lib-flexible/{{version}}/??flexible_css.js,flexible.js"></script>
```
将代码中的{{version}}换成对应的版本号0.3.4


## 网易做法

* 1 视口要如下设置

```
 <meta name="viewport" content="initial-scale=1,maximum-scale=1, minimum-scale=1">
```
 
* 2 当`deviceWidth`大于设计稿的横向分辨率时，html的`font-size`始终等于横向分辨率/body元素宽：



```
var deviceWidth = document.documentElement.clientWidth;
if(deviceWidth > 640) deviceWidth = 640;
document.documentElement.style.fontSize = deviceWidth / 6.4 + 'px';
```



## 淘宝的做法

淘宝的效果跟网易的效果其实是类似的，随着分辨率的变化，页面元素的尺寸和间距都相应变化，这是因为淘宝的尺寸也是使用了rem的原因。在介绍它的做法之前，先来了解一点关于viewport的知识，通常我们采用如下代码设置viewport:

```
<meta name="viewport"   content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
```

devicePixelRatio称为设备像素比，每款设备的devicePixelRatio都是已知，并且不变的，目前高清屏，普遍都是2，不过还有更高的，比如2.5, 3 等，我魅族note的手机的devicePixelRatio就是3。淘宝触屏版布局的前提就是viewport的scale根据devicePixelRatio动态设置：

```
var scale = 1 / devicePixelRatio;
document.querySelector('meta[name="viewport"]').setAttribute('content','initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
```

淘宝布局的第二个要点，就是html元素的font-size的计算公式，`font-size = deviceWidth / 10`

接下来要解决的问题是，元素的尺寸该如何计算，比如说设计稿上某一个元素的宽为150px，换算成rem应该怎么算呢？这个值等于设计稿标注尺寸/该设计稿对应的html的font-size。拿淘宝来说的，他们用的设计稿是750的，所以html的font-size就是75，如果某个元素时150px的宽，换算成rem就是150 / 75 = 2rem。总结下淘宝的这些做法：

* 1 动态设置viewport的scale

```
var scale = 1 / devicePixelRatio;
document.querySelector('meta[name="viewport"]').setAttribute('content','initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
```

* 2 动态计算html的font-size

```
document.documentElement.style.fontSize = document.documentElement.clientWidth / 10 + 'px';
```

* 3 布局的时候，各元素的css尺寸=设计稿标注尺寸/设计稿横向分辨率/10

* 4 font-size可能需要额外的媒介查询，并且font-size不使用rem，这一点跟网易是一样的


## 比较网易与淘宝的做法

网易的做法，rem值很好计算，淘宝的做法肯定得用计算器才能用好了 。不过要是你使用了less和sass这样的css处理器，就好办多了，以淘宝跟less举例，我们可以这样编写less：

```
//定义一个变量和一个mixin
@baseFontSize: 75;//基于视觉稿横屏尺寸/100得出的基准font-size
.px2rem(@name, @px){
    @{name}: @px / @baseFontSize * 1rem;
}

//使用示例：
.container {
    .px2rem(height, 240);
}

//less翻译结果：
.container {
    height: 3.2rem;
}

```

> [参考原文: https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html](https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html)

> [参考原文: http://www.cnblogs.com/axl234/p/5156956.html](http://www.cnblogs.com/axl234/p/5156956.html)