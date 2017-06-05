# Vue.js权威指南

## 预见Vue.js

### Vue.js是什么
1. 轻量
1. 数据绑定
1. 指令
1. 插件化

1. 渲染一次数据，可以通过“*”实现

### 表达式
Mustache标签也接收表达式形式的值

{{lat/100}}
{{true?1:0}}
{{example.split(",")}}

vue.js允许在表达式后添加过滤器(本质是一个函数)

{{example|toUpperCase}}
{{example|filterA|filterB}}
{{example|filter a b}}

### 指令
指令是带有特殊V-前缀的特殊特性，其值限定为绑定表达式，也就是js表达式和过滤器。指令的作用是表达式的值发生变化时，这个变化也反映在dom上，代码如下：
<div v-if='show'>DDFE</div>
当show为true时，展示DDFE，否则不展示

### 分隔符
vue.js中的数据绑定的语法被设计为可配置的。如果不习惯Mustache风格的语法，则可以自己设置。
可以在vue.config中配置绑定的语法。
vue.config是一个对象，包含了所有vue的所有全局配置，可以在vue实例化前修改其中的属性。