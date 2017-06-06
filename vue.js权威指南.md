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

## 指令

### 内部指令
1. v-show
1. v-else
1. v-model
1. v-repeat
1. v-for
1. v-text
1. v-el
1. v-html
1. v-on
1. v-bind
1. v-ref
1. v-pre
1. v-cloak
1. v-if

#### v-if
根据表达式的值在DOM中生成或移除一个元素，如果复制为false,那么对应的元素就会从DOM中移除，否则，对应元素的一个克隆将重新插入DOM中

#### v-show
根据表达式的值来显示或隐藏HTML元素，当为false，元素上多了一个内联样式style='display:none'
>>v-show不支持<template>语法
在切换v-if模块时，vue.js有一个局部编译、卸载过程。因为v-if中的模板可能包括数据绑定或子组件。v-if是真实的条件渲染，因为它会确保条件块在切换时合适的销毁与重建条件块内的事物监听器和子组件
v-if是惰性的——如果初始渲染时条件为假，则什么也不做，在第一个条件为真时局部编译（编译会被缓存起来）
v-show则简单的多——元素始终呗编译并保留，只是简单的基于css切换
>> 如果需要频繁的切换，则用v-show，否则用v-if

#### v-else
必须跟v-if或v-show，

#### v-model
用来在input,select,text,checkbox,radio等表单控件上创建双向数据绑定。根据控件类型v-model自动选取正确的方法更新元素。
v-model指令后面还可以添加多个参数(number,lazy,debounce)

##### number
如果想将用户的输入自动转换为Number类型，则可添加number特性(如果原值的转换结果为NaN,则返回原值)

##### lazy
默认情况下，v-model在input事件中同步输入框的值与数据，我们可以添加一个lazy特性，从而将数据改到在change事件中发生

##### debounce
设置一个最小的延时，在每次敲击之后延时同步输入框的值与数据

#### v-for
基于源数据渲染元素。也可以使用$index来呈现相对应的数组索引
v-for需要特殊的别名，形式为item in items 
>>1.0.17后支持of分隔符

#### v-text
可更新元素的textContent,在内部，{{Mustache}}插值也被编译为textNode的一个v-text指令。
<span v-text='msg'></span><br />
<!-- same as -->
<span>{{msg}}</span>

#### v-html
更新元素的innerHTML
<div v-html="html"></div>
<div {{{html}}}</div>

#### v-bind
响应更新HTML特性，将 一个或多个attribute，或者一个组件prop动态绑定到表达式
在绑定prop时，prop必须在子组件中声明。可以用修饰符指定不同的绑定类型。修饰符为：
+ .sync 双向绑定，只能用于prop绑定
+ .once 单项绑定，只能用于prop绑定
+ .camel 将绑定的特性名称转换为驼峰命名。只能用于普通的HTML特性的绑定，通常用于绑定用驼峰命名的SVG特性，比如viewBox


#### v-on
只能监听原生DOM事件，如果定义在子组件上，也可以监听组件触发的自定义事件
+ .stop 调用event.stopPropagation
+ .prevent 调用event.preventDefault
+ .capture 添加事件监听器时使用capture模式
+ .self 只当事件是从监听器绑定的元素本身触发才触发回调
+ .{keyCode|keyAlias} 只在制定按键上触发回调
>> vue.js提供的键值有[esc:27、tab:9、enter:13、space:32、'delete':[8,46]、up:38、left:37、right:39、down:40]

#### v-ref
在父组件上注册一个子组件的索引，便于直接访问，不需要表达式，必须提供参数id,可以通过父组件的$refs对象访问子组件。
>> 当v-ref和v-for一起使用时，注册的值将是一个数组，包含所有的子组件，对应于绑定数组；如果v-for使用在一个对象上，注册的值将是一个对象，包含所有的子组件，对应于对象。

#### v-el
为dom元素注册一个索引，方便通过所属实例的$els访问这个元素。可用v-el:some-el设置this.$els.someEL

#### v-pre
编译时跳过当前元素和它的子元素。可以用来显示原始Mustache标签。跳过大量没有指令的节点会加快编译

#### v-cloak
保持在元素上直到关联实例结束编译。


### 自定义指令

#### 基础
vue.js用vue.directive(id,definiton)方法注册一个全局自定义指令。他接收指令ID和定义对象。也可以用组件的directive选项注册一个局部自定义指令

#### 钩子函数
+ bind 只调用一次，在指令第一次绑定到元素上时调用
+ update 在bind之后立即以初始值为参数第一次调用，之后每当绑定值变化时调用，参数为新值与旧值
+ unbind 只调用一次，在指定从元素上解绑时调用

#### 指令实例属性
所有的钩子函数都将呗复制到实际的指令对象中，在钩子内this指向这个指令对象。这个对象暴露了一些有用的属性
+ el——指令绑定的元素
+ vm——拥有该指令的上下文ViewModel
+ expression——指令的表达式，不包含参数和过滤器
+ arg——指令的参数
+ name——指令的名字，不包含前缀
+ modifiers——一个对象，包含指令的修饰符
+ descriptor——一个对象，包含指令的解析结果

>> 我们应当将这些属性视为只读，不要修改他们。我们也可以给指令对象添加自定义属性，但是注意不要覆盖已有的内部属性。