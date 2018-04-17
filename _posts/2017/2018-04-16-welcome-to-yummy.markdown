---
layout: post
title:  "sublime text3 配置+++"
date:   2018-04-16 13:25:35 +0200
categories: Tool
tags: [Tool]
---

sublime text3 是一个轻量级的编辑器，在前端开发中我们经常使用它，接下来我们来配置一些比较常用的配置插件和主题!

## 下载地址: 
* [sublime text3 Download](https://www.sublimetext.com/3)

## 安装配置

### 1.`Package Control` 组件安装

```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())

```

### 2.下载完成之后重启Sublime Text 3

### 3.如果在Perferences->中看到package control这一项，则安装成功

### 4.用Package Control安装插件的方法

按下Ctrl+Shift+P调出命令面板,输入install 调出 `Install Package`选项并回车，然后在列表中选中要安装的插件。
注意: 安装插件时保持网络畅通，避免插件由于网络原因奔溃

## 插件配置

### 1.Emmet

* [Emmet指南](https://scotch.io/tutorials/write-html-crazy-fast-with-emmet-an-interactive-guide)

### 2.Alignment(代码对齐)

使用方法：选中要调整的行，然后按 Ctrl+ Alt + A

### 3.JsFormat

JS格式化

### 4.Colorsublime

允许您在Sublime Text中立即更改当前的颜色方案

## 主题配置

### 1.Boxy

自带多种主题风格，可以融合ihodevsublime-file-icons；切换主题风格不必改配置,个人推荐;

### 2.Seti_UI

非常好用的一款主题,个人推荐;

### 3.Agila

文件树中间距很大的文件夹，以便于阅读;

### 4.Lanzhou

边栏和编辑器之间的良好对比;

### 5.itg:Flat

一个扁平化设计风格主题,个人推荐

### 6.Spacegray

该主题在 UI 上没什么吸引人之处，但很适合编码;

### 7.Solarized

非常精确的颜色设置，这些颜色在不同的设备和不同的亮度环境下测试过;

### 8.Predawn

Predawn 非常漂亮，特别适合编写代码;

### 9.Tron Legacy

Tron 电影迷们可能会喜欢这一款主题，因为颜色相似;

### 10.Tomorrow Theme

Tomorrow 主题颜色丰富，有着强烈的对比,个人推荐;

### 11.Brogrammar

扁平而且性感的设计,个人推荐;

* [附上几款其他比较好的主题](https://scotch.io/bar-talk/best-sublime-text-3-themes-of-2015-and-2016)

## Less配置

### 1.下载安装nodejs

* [node.js](https://nodejs.org/en/)

### 2.安装lessc。可用npm包管理器直接安装的

```npm install less -g```

### 3.检查lessc是不是安装成功

`lessc -v`

### 4.安装submile的less2css插件

`Package Control`安装 `less2css`， less(高亮)

### 5.如果编译时submile报错

在cmd里安装 `less-plugin-clean-css` 插件
```npm install less-plugin-clean-css```

