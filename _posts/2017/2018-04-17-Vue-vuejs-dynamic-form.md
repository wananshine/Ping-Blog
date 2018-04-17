---
layout: post
title: vuejs动态表单
category: Vue
tags: [Vue]
---

最近有接触到一个项目，app里边的内嵌H5页面，一些入职的资料填写的。以及问卷调查的。

[vue-form-01.png](../../../../assets/images/vue-form-01.png)

然后给的需求是，这些值，有的选填，有的必填等等，都是后台配出来的，也就是页面打开的时候，根据字段进行判断是否必填，判断是`input`还是单选框。然后因为是移动端，我这边用了`mint-ui`的框架，然后用的是`cdn`方式引入的。具体框架怎么玩的，大家自己去看文档，我就不说了。

这边直接上页面代码，相关注释，我会写在代码里边

首先，页面加载的时候，会执行一个请求，获取这个页面需要填的项的一个信息。

```
data:[
  {
    checkDesc:"姓名"，//字段title
    is_required:"0"，,//是否必填
    nType:"0",//字段类型，0为input,1为单选框
    value:""
  },
  {
    checkDesc:"性别"，
    is_required:"0"，
    nType:"0",
    value:""
  },
]

```

然后页面上直接用for循环进行处理


```
<div id="app" style="background: none">
  <div v-for="(item,index) in dataList">
    <div v-if = "item.nType == '0'">
     <!--首先nType来判断输入框的类别，因为这边有一个else里边是一个时间选择器，先忽略-->
     <!--format是一个过滤器，主要是给必填项后边加一个*，然后对lable值进行处理-->
     <!--change时间，就是我们把发生改变的值，例如填入值，给绑定到data的数组里边-->
     <mt-field :label="item.checkDesc | format(item.is_required)" placeholder="请输入" :value="item.value" @change="inputMes($event,index)"></mt-field>
    </div>

    <div v-else-if = "item.nType == '1'">
       <mt-field :label="item.checkDesc | format(item.is_required)" placeholder="请选择" :value="item.value" @change="inputMes($event,index)"></mt-field>
    </div>
    <div v-else>
       <mt-radio :title="item.checkDesc | format(item.is_required)" :value="item.value" :options="handoverStatus" @change="inputMes($event,index)"></mt-radio>
   </div>
</div>
<mt-button type="primary" @click="submit(pageNum)">提交</mt-button>
<div style="width: 100%;text-align: center;color: #999;margin: 10px 0;font-size: 13px;">注意带 * 为必填项，请仔细检查！</div>
</div>

<script>
    new Vue({
        el: '#app',
        data:{
            dataList:[
            {
              checkDesc:"姓名"，//字段title
              is_required:"0"，,//是否必填
              nType:"0",//字段类型，0为input,1为单选框
              value:''
            },
            {
              checkDesc:"性别"，
              is_required:"0"，
              nType:"0",
              value:''
            }
          ]
        },
        created(){
            //axios获取到对应的data，然后是内嵌的h5,所以会有参数
             var url = window.location.search; 
             //获取url中"?"符后的字串
            var theRequest = new Object();
            if (url.indexOf("?") != -1) {
                var str = url.substr(1);
                strs = str.split("&");
                for(var i = 0; i < strs.length; i ++) {
                    theRequest[strs[i].split("=")[0]]=unescape(strs[i].split("=")[1]);
                }
            }
            //上边的这个函数，将url里边？后边的值给处理成data的值
        },
        methods:{
            inputMes(val,index){
              //index为索引值，用来给制定的data的value赋值的
                this.dataList[index].value = val;
            }，
            submil(){
                console.log(this.dataList);
            }
        }
    })


```


好了，基本上的表单的过程，以及获取值的过程都在这里了。大家可以看一下，然后自己根据相关要求，写一写非空判断就好了