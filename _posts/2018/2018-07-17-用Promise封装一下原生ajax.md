---
layout: post
title: 用Promise封装一下原生ajax
category: js
tags: [js]
---

```
function ajaxMise(url, method, data, async, timeout) {
    var xhr = new XMLHttpRequest()
    return new Promise(function (resolve, reject) {
        xhr.open(method, url, async);
        xhr.timeout = options.timeout;
        xhr.onloadend = function () {
            if ((xhr.status >= 200 && xhr.status < 300) || xhr.status === 304)
                resolve(xhr);
            else
                reject({
                    errorType: 'status_error',
                    xhr: xhr
                })
        }
        xhr.send(data);
        //错误处理
        xhr.onabort = function () {
            reject(new Error({
                errorType: 'abort_error',
                xhr: xhr
            }));
        }
        xhr.ontimeout = function () {
            reject({
                errorType: 'timeout_error',
                xhr: xhr
            });
        }
        xhr.onerror = function () {
            reject({
                errorType: 'onerror',
                xhr: xhr
            })
        }
    })
}
```