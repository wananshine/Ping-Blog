---
layout: post
title: 使用Promise封装简单Ajax方法
category: js
tags: [js]
---


一直都很喜欢使用原生的JavaScript，特别是不需要考虑兼容性的场景（虽然少得可怜）。可惜ECMAScript并没有封装好的Ajax方法（其实也没什么必要有），自己动手使用Promise撸一个吧！



## GET

```
function getJSON (url) {

    return new Promise( (resolve, reject) => {
        var xhr = new XMLHttpRequest()
        xhr.open('GET', url, true)

        xhr.onreadystatechange = function () {
            if (this.readyState === 4) {
                if (this.status === 200) {
                    resolve(this.responseText, this)
                } else {
                    var resJson = { code: this.status, response: this.response }
                    reject(resJson, this)
                }
            }
        }

        xhr.send()
    })

}

```


## POST

```
function postJSON(url, data) {
    return new Promise( (resolve, reject) => {
        var xhr = new XMLHttpRequest()
        xhr.open("POST", url, true)
        xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

        xhr.onreadystatechange = function () {
            if (this.readyState === 4) {
                if (this.status === 200) {
                    resolve(JSON.parse(this.responseText), this)
                } else {
                    var resJson = { code: this.status, response: this.response }
                    reject(resJson, this)
                }
            }
        }

        xhr.send(JSON.stringify(data))
    })
}

```


## 总结

其实	`Promise`这家伙就是一个天然的`try...catch`

```
getJSON('/api/v1/xxx')    // => 这里面是就try
.catch( error => {
  // dosomething          // => 这里就是catch到了error，如果处理error以及返还合适的值
})
.then( value => {
  // dosomething          // 这里就是final
})

```


不过有的朋友喜欢把`catch`方法放在`then`方法的后面，这样就也可以监听到`then`的错误。不过我不是特别喜欢这一做法，逻辑错误和网络请求错误怎么能混为一谈呢？