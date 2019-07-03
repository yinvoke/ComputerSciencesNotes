# Vue学习笔记

该笔记用于做官方文档的学习中的辅助作用，记录一些要点、盲点，进行一些总结。一切以官方文档为准。

>官方技术文档：<https://cn.vuejs.org/v2/guide/>
>
>项目构建文档：<https://cli.vuejs.org/zh/guide/>



### 1.v-cloak

```html
<p id="app">{{message}}</p>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                message:"hello world"
            }
        })
    </script>
```

由于页面会先渲染html，加载js脚本需要时间，所以会出现{{message}}在加载页面时闪烁的情况，当网络状况不好时，这种情况尤为严重，所以采用v-cloak来使该标签在js未加载好前隐藏。

**解决方案：**

```html
<style>
    [v-cloak]{
        display: none;
    }
</style>
<p id="app" v-cloak>{{message}}</p>
    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                message:"hello world"
            }
        })
    </script>
```



### 2.v-text和插值表达式的区别

- 默认v-text无闪烁问题
- v-text会覆盖原有标签中的内容，插值表达式只替换本身的占位符
- 用户数据建议使用v-text来保护安全



### 3.v-on支持事件

<https://developer.mozilla.org/zh-CN/docs/Web/Events>



### 4.事件修饰符中self只会阻止单个冒泡，而stop会阻止所有冒泡

