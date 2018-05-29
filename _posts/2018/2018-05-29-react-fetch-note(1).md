---
layout: post
title: react-fetch获取本地json文件问题
category: react
tags: [react]
---

## 笔记(1)

写这个博客主要目的是有必要警醒一下自己


问题很简单：上码（ header.jsx）
```
fetchSelData = () => {  
        fetch('../data/selectData.json')  
            .then((res) => {return res.json(); })  
            .then((data) => {alert(JSON.stringify(data));this.setState({selV:data.obj});})  
            .catch((e) => {console.log(e.message); });  
    }    

```

上面是我用fetch获取本地的一个json文件，声明代码是没问题的。然后我的本地文件是放在在这个：


![react-fetch-01.png](../../../../assets/images/react-fetch-01.png)


印象中“../”一直表示的是上一级，然而这里的上一级不是从header.jsx开始的。一直以为路径是没有问题的。故运行起来。但不幸的是报错了：


![react-fetch-02.png](../../../../assets/images/react-fetch-02.png)


上面报的是json数据格式的有问题，所以就去看是不是数据的问题，json数据测试来测试去都没问题呀……就这样花费几个小时浪费在json数据上还有fetch版本上，最后不得已找了个远程数据来测试，是可以显示的。那问题就很明显了，报错的原因是找不到路径从而解析数据出错。

经过网上一番好找终于找到答案了。


***原因就是这个里的“../”是相对你的首页index.html而言的。所以将json数据放在相对index.html上问题就解决了。***


![react-fetch-03.png](../../../../assets/images/react-fetch-03.png)

