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



### 5.v-bind和v-model

v-bind只能提供单向绑定，无法实现双向绑定。但是v-model只能用于表单元素中。



### 6.动态样式

[^注]: 下列代码中，c1，c2，c3均为css样式表中的类

1.数组

```html
<h1 :class="['c1','c2']">
    test demo
</h1>
```

2.三元表达式

```html
<h1 :class="[isc1 ? 'c1' : 'c2']">
    test demo
</h1>
```

3.数组中嵌套对象

```html
<h1 :class="['c1',{'c2':isc2}]">
    test demo
</h1>
```

4.对象

```html
<h1 :class="{c1:true,c2:true,c3:true}">
    test demo
</h1>
```



### 7.属性

- 侦听属性

```html
<div id="demo">{{ fullName }}</div>
<script>
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
</script>
```



- 计算属性

  计算属性有缓存，而调用方法无缓存

```html
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
<script>
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})
</script>
```



### 8.数组方法

- some

```js
this.list.some((item, i) => {
                        if (item.id == id) {
                            this.list.splice(i, 1)
                            return true;
                        }
                    })
```

- findIndex

```js
this.list.findIndex(item => {
                        if (item.id == id) {
                            return true;
                        }
                    })
```

- foreach

```js
this.list.forEach(item => {
                            if (item.name.indexOf(keywords) != -1) {
                                tempList.push(item)
                            }
                        })
```

- filter

```js
this.list.filter(item => {
                            if (item.name.includes(keywords)) {
                                tempList.push(item)
                            }
                        })
```



### 9.前端路由与后端路由区别



