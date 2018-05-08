---
layout: post
title: vue-cli项目打包出现空白页和路径错误问题
category: vue
tags: [vue]
---



vue-cli项目打包：


## 1. 命令行输入：`npm  run  build`

打包出来后项目中就会多了一个文件夹dist，这就是我们打包过后的项目。

![vue-cli-build-01.png](../../../../assets/images/vue-cli-build-01.png)

第一个问题，文件引用路径。我们直接运行打包后的文件夹中的`index.html`文件，会看到网页一片空白，f12调试，全是css，js路径引用错误的问题。

解决：到`config`文件夹中打开`index.js`文件。

文件里面有两个`assetsPublicPath`属性，更改第一个，也就是更改`build`里面的`assetsPublicPath`属性：


![vue-cli-build-02.png](../../../../assets/images/vue-cli-build-02.png)


assetsPublicPath属性作用是指定编译发布的根目录，***‘/’指的是项目的根目录 ，’./’指的是当前目录。改好之后重新打包项目，运行index.html文件，我们可以看到没有报错了。但是`router-view`里面的内容却出不来了。***




第二个问题：***`router-view`中的内容显示不出来。路由`history`模式***。

这个坑是当你使用了路由之后，***在没有后端配合的情况下就手贱打开路由`history`模式的时候***，打包出来的文件也会是一片空白的情况，

很多人踩这个坑的时候花了很多时间，网上的教程基本上都是说的第一个坑，这个坑很少有人提起。


![vue-cli-build-03.png](../../../../assets/images/vue-cli-build-03.png)


解决：`// mode: 'history'`,//将这个模式关闭就好

这里并不是说不能打开这个模式，这个模式需要后端设置的配合，详情可以看：[路由文档](https://router.vuejs.org/zh-cn/essentials/history-mode.html)



第三个问题

修改：

![vue-cli-build-04.png](../../../../assets/images/vue-cli-build-04.png)

![vue-cli-build-05.png](../../../../assets/images/vue-cli-build-05.png)



## 总结

1、npm run dev查看没有问题

2、npm run build打包

3、起一个服务（例如：python -m SimpleHTTPServer）然后查看index.html页面，发现路由会请求/first页面。

4、解决的办法：将路由配置中history改为hash，将链接中/first改为/#/first。问题解决。