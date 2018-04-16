---
layout: post
title:  "sublime text3 配置!"
date:   2018-04-16 13:25:35 +0200
categories: Tool
tags: [Tool]
---

sublime text3 是一个轻量级的编辑器，在前端开发中我们经常使用它，接下来我们来配置一些比较常用的配置插件和主题!
## 下载地址: 
* [sublime text3 Download](https://www.sublimetext.com/3)

## 安装配置

### 1.'Package Control' 组件安装

'''
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
'''


