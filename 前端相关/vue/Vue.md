# Vue

## Vue简介

Vue是一套构建用户界面的**渐进式框架**---（需要就用，不需要的vue部分不用），自底向上增量开发，目标是通过简单的 API 实现响应的数据绑定和组合的视图组件。

API：（Application Programming Interface）应用程序编程接口，预先定义的函数。

 ## Vue安装下载

### 1，NPM引入

```html
npm install vue@版本 --save
```

#### 1.1 --save和--save-dev的区别

发布时仍需要的：--save

dependencies是运行时依赖

devDependencies是开发时的依赖

--save 会把依赖包名称添加到 package.json 文件 dependencies 键下

--save-dev 则添加到 package.json 文件 devDependencies 键下

#### 1.2 全局安装和本地安装的区别

全局安装的包可提供直接执行的命令，一般在项目中需要用到该包定义的命令才需要全局安装

本地安装可以更灵活地在不同的项目使用不同版本的包，并避免全局包污染的问题

### 2，直接下载引入

下载vue，然后script便签引入

### 3，CND使用

就是把外部script标签引入

## Vue中的指令

### 1，Vue中bind的使用

v-bind：动态绑定一个或多个 attribute（属性），或一个组件 prop 到表达式。

语法糖：：

常见用法：绑定class和style，方法为数组绑定和对象绑定

- 对象语法

```html
<div v-bind:class="{active:isActive}"></div>
语法：{属性1:值1,属性2:值2}
值为boolea值，若为true，则添加属性
```

- 数组语法

```html
<div v-bind:class="[active,'isactive1']"></div>
将数组中的属性加入到class中，其中active是属性，isactive是字符串。修改active的值时可以动态修改class
```

#### 1，v-bind使用is和组件绑定使用

绑定is，在组件中使用，在data中找到is对应的属性，并将组件替换为对应的

```html
<component v-bind:is="current"></component>
//is绑定的是current对应的sub
//上述变成
<sub></sub>
```

### 2，Vue中slot的使用

v-slot：绑定插槽名，仅在template中使用。

语法糖：#

常见用法：用于提供具名插槽或需要接收 prop 的插槽

可以接受插槽传递的属性

### 3,	Vue中插值指令

#### 3.1 mustache语法---{{}}

支持简单的表达式，例如加减、？：，但不支持控制流

#### 3.2 v-once---只使用一次，修改不变

例如绑定按钮，改变某一属性，被v-once标记过的不改变

```html
<h1 v-once>{{message}}</h1>
```

#### 3.3 v-html---将元素编译成html

```html
<span v-html="rawHtml"></span>//将rawHtml编译成html文件
```

#### 3.4 v-text---将元素渲染到标签中

会覆盖原有的文本

#### 3.5 v-pre---不编译属性

```html
<h2 v-pre>{{message}}</h2>//输出{{message}}
```

#### 3.6 v-cloak---解析之前有v-cloak，渲染出来后自动消失

斗篷默认自带样式**[v-cloak] { display: none }**

### 4，Vue中on的使用

v-son：绑定事件，可在子组件，父组件中使用。

语法糖：@

修饰符：

- .stop - 阻止冒泡，调用 event.stopPropagation()。
- .prevent - 阻止默认事件，调用 event.preventDefault()。
- .capture - 添加事件侦听器时使用 capture 模式。
- .self - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
- .{keyCode | keyAlias} - 只当事件是从**特定键**触发时才触发回调。----例如：@keyup.13="onEnter"
- .native - 监听组件根元素的原生事件。
- .once - 只触发一次回调。
- .left - (2.2.0) 只当点击鼠标左键时触发。
- .right - (2.2.0) 只当点击鼠标右键时触发。
- .middle - (2.2.0) 只当点击鼠标中键时触发。
- .passive  - (2.3.0) 以 `{ passive: true }` 模式添加侦听器

#### 4.1 v-on传参问题

1，不需要传参

()可写可不写

2，需要传参

1，传一个参数

- fun---将事件本身$event作为参数传入

- fun()---将一个undefined空参数传入
- fun(123)---正常传参

2，传两个参数---第一个是参数，第二个是事件本身

- fun---==fun($event)，将事件本身作为参数传入，另一个为undefined

- fun()---两个都为undefined

- fun(123,event)---报错，将event当做变量
- fun(123,$event)---正常输出
- fun(123)/fun($event)---另一个参数为undefined



### 5，Vue中条件渲染的使用

条件渲染指的是被标记的内容，只在指令的表达式返回true值的时候被渲染，常见的有v-show和v-if。

#### 1，v-show和v-if的区别

v-show中，元素会被渲染，只是修改display：none

v-if中，根据表达式创建和销毁元素

1，当初始表达式为false时，v-show已经渲染了，但是v-if不会渲染

2，当修改表达式为false时，v-if销毁元素，v-show修改样式

因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好。

#### 2，v-if

v-if、v-else、v-else-if

### 6，Vue中for的使用

v-for可以遍历对象和数组

在数组中可以遍历item和index

在对象中可以遍历item和index和key

语法：(item,index) in movies

```html
<li v-for="item in letter" :key="item">{{item}}</li>
```

**key的作用**

数据变化时，DOM的改变：

真实DOM：重绘和重排----预期----Dom：只改变修改部分

diff算法：生成虚拟DOM，对比虚拟DOM和真实DOM，直接修改真实DOM

新值和旧值作比较，一层层比较，若不同直接替换，若同，比较子节点，直至有一方没有子节点

缺点：当删除数组中一个元素时，其后的每一个元素都有可能被改变

key的作用：如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 `key` attribute：

### 7，v-model的使用

作用：在表单控件或者组件上创建双向绑定。

**修饰符**：

- .lazy - 取代 input监听change事件
- .number - 输入字符串转为有效的数字
- .trim - 输入首尾空格过滤

表单控件：

- text和textarea中是input事件和value属性
- checkbox和radio是checked属性和change事件，其实就是click事件
- select中value属性作为props和change事件

#### 1，在自定义组件中实现v-model

1，在组件中添加model属性

一是绑定的checked属性

二是绑定的change事件

model: {    prop: 'check2',    event: 'change'  }

2，接收父组件v-model传过来的值，需和上面保持一致

props:{

  check2:Boolean

 }

3，父组件通过v-model传入check的值，名字随意

<HelloWorld v-model="check1"/>

4，在子组件中使用model中的数据

v-bind绑定model中的prop属性，v-on绑定model中的event事件

<input type="checkbox" :checked="check2" @change="change2">哈哈哈

5，在子组件的change事件中，发送事件回父组件

change2(){

   this.$emit('change1',$event.target.checked)

  }

6，在父组件中操作子组件传回来的事件

 change1(){

   this.check1 = !this.check1

  }

### 8，自定义指令

指除了上述的指令，vue可以自行创建指令

1-1，全局注册自定义指令

```html
Vue.directive('指令名'，{触发指令时该干的事})
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {//钩子函数
    // 聚焦元素
    el.focus()
  }
})
```

1-2，注册局部自定义指令--组件中的属性

```html
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```

2，在模板中使用

v-focus

#### 1，自定义指令的钩子函数

当元素绑定指令时，会有几个钩子函数

- `bind`：只调一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。
- `unbind`：只调用一次，指令与元素解绑时调用。

钩子函数有以下几个参数

- `el`：指令所绑定的元素，可以用来直接操作 DOM。
- binding：一个对象，包含以下 property：
  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。
- `vnode`：Vue 编译生成的虚拟节点。
- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

## Vue中的属性options

### Vue中的el

用于挂载要管理的元素，例如：el:'#box'

可以使用this.$el访问组件

只有new实例才有此属性

### Vue中使用data

data:{}---数据：在组件中是函数，在main.js实例中是对象

### Vue中使用methods

methods:{}--方法：一个对象，在对象中定义函数

### Vue中使用computed

computed:{}---计算属性：常用来操作一个**数据**，此数据可以不用在在data中声明，也不用调用，直接在页面使用。响应式，当数据变化时，计算属性也会执行。

#### 1，计算属性和方法的区别：

缓存：计算属性有一个缓存的概念，即若数据没有发生响应式，再次调用时，他不会再次执行，而是直接返回刚才的结果。

而方法时每次调用都执行一次

计算属性和监听的区别：监听是监听某个数据，计算属性可以一次性监听多个数据，性能更好

#### 2，getter和setter属性

当只进行监听数据变化是，可省getter和setter，直接return。

```js
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```

### Vue中Watch使用

1，直接监听属性变化，属性变化时触发函数

```js
watch: {
    firstName(newName, oldName) {//监听fristName这个属性
      this.fullName = newName + ' ' + this.lastName;
    }
```

2，handler方法和immediate属性

immediate属性是Boolean值

当immediate为true时，立即触发handler方法

```js
watch:{
    fristName:{// 属性从函数变成对象
         handler(){},
         immediate:true
      }
  }
```

3，deep属性（深度监听，常用语对象下面属性的改变）：

一般是无法监听到对象的属性的变化的，需要deep监听

修改obj里面任何一个属性都会触发这个监听器里的 handler，弊端：可以只监听对象的某个属性变化

```html
'obj.a': {
    handler(newName, oldName) {
      console.log('obj.a changed');
    },
    immediate: true,
    deep: true
  }
```

##### 3，computed和watch和methods执行顺序

执行顺序为：默认加载的时候先computed再watch，不执行methods；等触发某一事件后，则是：先methods再watch。

其中computed必执行一次

## Vue中的周期函数

![](F:\图片资源\Vue生命周期函数.png)

周期函数也是一个vue实例中的options，分为四个部分：创建前后、挂载前后、更新前后、销毁前后。

生命周期钩子的 `this` 上下文指向调用它的 Vue 实例。可以用来操作DOM元素

一、创建前后（必走）--初始化一些属性、事件以及响应式数据

- beforeCreate
  
  初始化事件和周期函数
  
  **注意点**：在此时不能获取data中的数据，也就是说`this.msg`得到的是undefined
  
- created

  初始化数据和方法，实例已经创建好了，但是还没有渲染模板
  
  可以获取到data，但是页面还没有挂载

1，判断有无el

无则调用实例方法app.$mount创建一个el

2，判断有无template

​       no->Compile el's outerHtml as template: 如果实例里面没有tempalte这个属性，会把外部el挂载点的html当作模板

　　yes->Compile template into render functoin: 如果实例里面有tempalte，这个时候就会用template去渲染mounted

二、挂载前后（必走）

> - beforeMount
>
> ​      将编译完成的html挂载到虚拟dom中，页面无内容
>
> - mounted
>
>   将页面html代替el，页面加载完毕的时候就是此时

三、更新前后（元素或组件的变更操作）（可能走）

> - beforeUpdate
> - updated
>   - 可以`重复触发`的

四、销毁前后（销毁相关属性）（必走，例：关页面时）

> - beforeDestroy
> - destroyed

无、keep-alive组件特有周期函数

页面活跃与否

- activated
- deactivated

### 1，基于周期函数选择模板

当使用脚手架选择编译模板时，有两个选项

runtime-only和runtime-compiler

在main.js文件中区别

```html
//compiler中
new Vue({
  el:'#app'//简单使用el挂载
  template:'<App/>',//简单的将App组件注册写入模板
  components:{App}
})

new Vue({
  render: h => h(App),//没有模板和组件，调用render函数
}).$mount('#app')//使用$mount挂载el
```

周期函数的区别：上面是编译，下面是only

<img src="F:\图片资源\普通编译.png" style="zoom:25%;" />

<img src="F:\图片资源\only编译.png" style="zoom:25%;" />

template编译成dom：先被解析成ast，再被编译成一个render函数，这个render函数会构造一个virtual dom(虚拟dom)，最后virtual dom会转换为真实dom，进行页面展示。

![](F:\图片资源\template编译成dom.png)

**runtime-compiler的步骤：**
template -> ast -> render -> virtual dom -> 真实dom

**runtime-only的步骤**
render -> virtual dom -> 真实dom

### 2，Vue父子组件周期函数

父到子，子到父

渲染时：父：beforeCreate->created->beforeMount->子：beforeCreate->created->beforeMount->mounted->父：mounted

更新时：

销毁时:

## Vue中插槽的使用

原因：在父组件中使用子组件时，并不能在子组件中插入内容

插槽：在子组件中使用插槽标签slot，父组件在子组件中插入内容时替代子组件中的slot标签

### 1，简单使用

```html
//在子组件中
<template>
  <div class="hello">
   <slot >www</slot>
   hhh
   <slot >www</slot>
  </div>
</template>
//在父组件中
<template>
  <div id="app">
    <hello-world>
     <p>hhh1</p>
      <p>hhh2</p>
    </hello-world>
  </div>
</template>
//输出：hhh1 hhh2 hhh hhh1 hhh2
//如父组件不插入，输出：www hhh www
```

### 2，具名插槽

在子组件中slot标签添加name属性

1，父组件直接使用slot=‘center‘

2，使用v-slot--必须在template中使用

```html
<hello-world>
<template v-slot:head>//<template #head>
       <div style="background: blue;">网页头部</div>
        </template>
    <template v-slot:footer>
       <div style="background: blue;">网页底部</div>
        </template>
</hello-world>
```

### 3，作用域插槽

当父组件想使用子组件插槽的属性时，不能直接使用，因为属性只能在子组件作用域使用

- 在子组件绑定属性
- 父组件使用slot接受属性

```html
//子组件绑定
<slot :movie="item" :index="index">{{ item }}</slot>
//父组件接收
<template v-slot="{ movie, index }">
            <h1> {{ index }} -- {{ movie }}</h1>
        </template>
```

### 4，编译作用域

在父组件中使用子组件，绑定在子组件的东西，作用域在父组件，但是子组件

父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。

```html
<hello-world v-show="isShow">
 <p slot="right">{{message}}</p>
</hello-world>
在父组件作用域，根据isShow和message决定子组件内容
```

**注意：**和内联模板的区别，内联模板挂载的是子组件，所以无法访问message

## Vue组件化

**每个组件必须只有一个根元素**，组件独立且可复用，最后成为一颗组件树

### 1，定义组件

1，全局组件

Vue.component('组件名',{组件内容：data，template，props})

在全局中定义的组件，可以直接使用，任何 (通过 new Vue) 新创建的 Vue 根实例，也包括其组件树中的所有子组件的模板中

首先data是一个函数，返回一个对象

- 当在runtime-only时，不可以使用模板，所以传入一个组件吧！

2，局部组件

定义组件，在实例中挂载

components:{
 cpn:cpn//左边是命名，右边是注册了的组件
}

### 2，组件中使用

### 3，组件中传递数据

#### 1，父传子

父组件直接在子组件标签中写属性，若不在子组件**prop**没有接收该属性，则直接添加到子组件的根标签中，例如class

- 若不希望污染子组件根标签，则可以在子组件中设置

```html
inheritAttrs: false,
```

- inheritAttrs结合$attrs实现属性绑定在非根标签

```html
<label>//加了inheritAttrs不绑定在根label标签
 <input v-bind="$attrs" >//$attrs将它绑定在input标签
</label>
```

**但是：inheritAttrs不影响style和class**

##### prop

**类型**：数组或对象

数组：props: ['title', 'author']

对象：props: { title: String,  author: Object}

对象还可以包含对象，例如title:{type:String,default:'LYF'}

- 静态传值：如非字符串，也需加v-bind

- ```html
  <blog v-bind:likes="42"></blog>
  ```

- 传入一个对象的所有属性

- ```html
  <blog v-bind="post"></blog>
  <blog
    v-bind:id="post.id"
    v-bind:title="post.title"
  ></blog>
  ```

子组件接受prop时，不应直接修改prop的值，应再定义一个变量接收它，然后修改该变量

```html
props: ['Counter'],
data: function () {
  return {
    counter: this.Counter
  }
}
```

**prop验证**

对传入的值进行验证，如不合格，则警告Vue warn

参数：type，default，required

- type:参数类型--数组、对象、函数、基本类型、构造函数

- default：默认值，若没有传值，则默认为

- required：是否必须

 对象或数组默认值必须从一个工厂函数获取

```html
default: function () {
        return { message: 'hello' }
      }
```



#### 2，子传父

通过emit发送事件

##### .sync修饰符

实现子组件修改父组件传过来的属性，而父组件也相应修改

```html
<comp :foo.sync="bar"></comp>
当子组件修改foo时，bar也被修改
```

实际上的完整事件

```html
<comp :foo="bar" @update:foo="val => bar = val"></comp>
父组件通过v-bind传入数据A，再通过v-on执行子组件发送的事件，该事件修改的是自己的属性A
```

子组件发送事件---这个必须发送，不发送无法改变父组件

```html
this.$emit('update:foo', newValue)
//名字是固定的
```

### 4，函数式组件

函数就是组件，组件就是函数

特点是：没有内部状态、没有生命周期函数、没有this（不需要实例化的组件）

#### 1，函数式组件和普通组件的区别

- 声明时表明是functional
- 不需要实例化，所以没有`this`，`this`通过`render`函数的第二个参数来代替
- 没有生命周期钩子函数，不能使用计算属性，`watch`等等。
- 不能通过`$emit`对外暴露事件，调用事件只能通过`context.listeners.click`的方式调用外部传入的事件。
- 因为函数式组件是没有实例化的，所以在外部通过`ref`去引用组件时，实际引用的是`HTMLElement`。
- 函数式组件的`props`可以只声明一部分或者全都不声明，所有没有在`props`里面声明的属性都会被自动隐式解析为`prop`，而普通组件所有未声明的属性都被解析到`$attrs`里面，并自动挂载到组件根元素上面(可以通过`inheritAttrs`属性禁止)。

#### 2，函数式组件的写法

模板语法写法

```html
<template functional>
  <p>{{props.text ? props.text : '哈哈'}}</p>
</template>
```

JSX写法---需学习jsx

不与模板共存，且优先级小于模板

```html
<script>
export default {
  functional: true,
  props: {
    text: {
      type: String
    }
  },
  /**
   * 渲染函数
   * @param {*} h
   * @param {*} context 函数式组件没有this, props, slots等都在context上面挂着
   */
  render(h, context) {
    console.log(context);
    const { props } = context
    if (props.text) {
      return <p>{props.text}</p>
    }
    return <p>哈哈嗝</p>
  }
}
</script>
```

template和jsx的区别和本质

本质：都只是创建节点createElement的语法糖

Jsx---{this.mes}

template---{{mes}}

在逻辑复杂时，可以使用JSX，但是逻辑简单时使用template

根据属性动态修改标签，但是template是根据属性动态选择标签

### 5，自定义事件的补充

绑定原生事件到组件

.native会把事件直接绑定到组件**根标签**

$listeners，一个对象，储存组件 (不含 .native 修饰器的)绑定的所有事件，例如：

```html
<child v-bind="$attrs" v-on="$listeners"></child>
该组件拿到父组件传来的属性（props没定义的）和事件，并可以传给自己的子组件，实现将爷孙传值
```

```html
inputListeners: function () {
      var vm = this
        // Object.assign将所有的对象合并为一个新对象
      return Object.assign({},
        //我们从父级添加所有的监听器
        this.$listeners,
        // 然后我们添加自定义监听器，
        {
             //监听输入
          input: function (event) {
            vm.$emit('input', event.target.value)
          }
        }
      )
    }
```

### 6，动态组件

v-bind和使用keep-alive包裹，使得组件保持状态

```html
<keep-alive>  <component v-bind:is="currentTabComponent"></component> </keep-alive>
```

### 7，异步组件

当进入页面时，没有加载组件，使用时才加载，将组件定义为一个工厂函数，渲染时触发工厂函数---和路由懒加载类似

```html
1，components: {
    myComponent: () => import('./my-async-component')
  }
2，工厂函数
传入vue
const later2 = Vue.component('later2', function (resolve) {
    require(['./later2.vue'], resolve)
});
```

### 8，组件间相互访问

根组件（main.js）--依赖-- 组件实例（App.vue）--依赖--子组件（other.vue）

组件间可以通过指令相互访问并**操作**对方组件的元素

#### 1，根据实例属性操作组件

1，访问根元素$root

根组件指的是main.js，这才是最开始vue实例的地方

```html
new Vue({
  router,
  render: h => h(App),
  data: { name: 'apps name' },
}).$mount('#app')
```

2，访问子组件$refs

在子组件中定义ref属性指定名称，通过this.$refs.指定的子组件名称，即可获得对该子组件的操作（包括data中定义的数据和methods中定义的方法）

3，访问父组件$parent
 可以直接操作当前组件的父组件

4，访问孩子组件$children
返回该组件的所有组件，并封装为一个数组

按照组件使用顺序决定数组排序

this.$children[0].message = 'hahah'

#### 2，根据Vue高级属性provide

vue中options中的高级属性provide/inject，实现跨层级访问组件

祖先组件设置provide：一个函数，**返回**子组件需要接收的数据

后代组件inject：一个数组/对象，获取provide暴露出来的数据

```html
祖先组件
provide: function () {
  return {
    getMap: this.getMap
  }
}

后代组件
inject: ['getMap']
```

**解决无法响应问题**

祖先组件暴露出来的属性发生变化，而后代组件使用时，无法实时响应，但若为一个对象时，可以监听到其的变化

1，在祖先组件中暴露出一个this，后代组件调用父组件的特定属性

```html
//祖先组件
provide(){
    return {
      main:this
    }
  }

//后代组件
inject:['main']//引入
<p :style="{color:main.color}">hh</p>//和祖先组件绑定

缺点：把祖先组件的所有属性都暴露了！
```

**2**，祖先组件将属性作为函数，而数据值作为返回值返回，每次调用都是最新的数据，后代组件将元素在计算属性中执行---**常用**

```html
//父组件
provide(){
    return {
      main:()=> this.main
    }
  }

//子组件
inject:['main']
computed: {
  mainFromParent () {
   return this.main()
  }
 }
```

3，在祖先组件中使用计算属性监听

```html
provide(){
    return {
      main:Vue.computed(()=>this.message)//貌似不行的样子
    }
  }
```

#### 3，祖先后代组件相互传值

祖先组件：使用this.$on确定事件和接收的参数

后代组件：使用this.dispatch分派事件

```html
监听组件：在祖先组件的created中创建
this.$on('app-has-header', ({ type, fixed }) => {
            this.headerInfo.type = type;
            this.headerInfo.fixed = fixed;
            console.log('wo shixianl ',type,fixed)
        });

触发组件：在后代的beforeMount中分派
 this.dispatch('AppPage', {
            event: 'app-has-header',
            params: {
                type: this.type,
                fixed: this.fixed
            }
        });
```

父子组件生命周期：

```html
父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted
```







### 9，组件循环引用

当组件A引用组件B时，组件B又反过来引用组件A时，就是循环组件。循环组件会出现问题，因为系统在编译A时因为用了B就去找B，找到B后又找A，无法跳出来

解决方法1：全局注册组件

```html
Vue.component('组件名',{})
```

解决方法2：异步组件----找一个组件为主组件，在引入另外一个组件时异步加载

```html
components: {
  Children: () => import('./Children.vue')
}
```

### 10，内联模板

在子组件中使用inline-template属性

```html
<tree-folder inline-template>
    //内联模板：最终渲染
    <div>//根标签包裹
    <li>{{fristName}}</li>//父组件data，无法访问
    <li>{{lastName}}</li>//父组件data,无法访问
    <li>{{mes}}</li>//子组件data，可以访问
    </div>
 </tree-folder>
```

将组件下的内容作为模板，而不是组件中定义的东西，且仍然属于子组件作用域，无法访问父组件的data，且也需要根标签包裹

### 11，render函数

使用render函数写组件，省去**template**的部分，在script中书写render，若有template部分，则**优先级**是template高于render函数

```html
<script>
    export default{
		render(h){},
        data(){
            return{}
            },
        methods:{},
        components:{}
}
</script>
<style></style>
```

1，普通render的写法

```javascript
render(h){ return h('dom元素名称',{dom元素属性},[dom元素子元素])}
//@params字符串 @params对象 @params数组
render(h) {
        return h(
            "div",
            {
                class: "info-list"
            },
            ['hhhhhhh']
        );
    }
```

2，当在render中调用methods函数进行子组件的复用

```javascript
render(h) {
        return h(
            "div",
            {
                class: "info-list"
            },
            [
                (() => {
                    return this.children(h, this.arr);
                })()//匿名箭头函数自调用，返回methods函数调用结果，进行子组件渲染
            ]
        );
    },
```

## Vue中的动画的过渡

vue自定义组件transition可以为元素添加过渡效果

transition提供六个class来提供过渡效果：v表示组件名字

v-enter：进入

v-enter-active：过渡阶段

v-enter-to：完整进入

v-leave：离开

v-leave-active：过渡阶段

v-leave-to：完整离开

```html
<transition name = "fade">
    <p v-show = "show" v-bind:style = "styleobj">动画实例</p>
</transition>
```

## Vue中使用mixin混入

定义一个类vue混入实例

```html
var mixin = {
data(){
  return{
      mes:'abc'
        }
     }
}
```

在组件中使用混入对象

```html
mixins: [mixin],
```

当混入对象和组件都存在某个属性时，采用合并的原则

```html
混入对象有data为message：1和information
组件也有message:2
最终组件中data{ message: 2, information: 'yes'}
```

常见使用场景：例如几个组件在某钩子函数中调用同一个事件，则可以抽取mixin

## Vue中路由

将组件映射到路由中，然后告诉 Vue Router 在哪里渲染它们

### 1，简单路由配置

#### 1，配置路由文件

1，下载路由--npm或添加依赖

2，路由一般放在src同级文件夹下的router文件夹中，一般叫index.js

3，导入路由和vue

import Vue from 'vue'
import VueRouter from 'vur-router'

4，安装路由

Vue.use(VueRouter)

5，创建路由对象

```html
import Home  from './Home.vue';
1,const routes = []//一般需要引入组件
2,const router = new VueRouter({
routes,
mode:'history'
})
```

- 配置路由对象

  { 

  path: '/',

   redirect: '/home' 
  //重定向

  },{

  path:'/home',

  component:Home

  }]

6，导出路由

```html
export default router
```

7，在main.js文件中引入路由

```html
import router from './router'
```

8，在main.js中挂载路由

```html
new Vue({
el:'#app',
router,
render:h=>h(App)
})
```

#### 2，使用路由页面跳转

1，标签导航

router-link标签实现路由导航，默认渲染为a标签

to代表指定的链接

router-view显示路由内容

```html
<router-link to="/foo">Go to Foo</router-link>
<router-view></router-view>
```

2，编程式导航

```javascript
this.$router.[push/replace]('/xxx')
```

#### 3，路由对象配置参数

- path：跳转路径
- component：路径相对于的组件
- name：命名路由
- children：子路由的配置参数（路由嵌套）
- props：路由解耦
- redirect：重定向路由
- alias：别名

### 2，动态路由

动态路径参数 以冒号开头

path:'/user/:id'

参数会被设置到路由参数中this.$route.params中

### 3，命名路由

配置路由对象的参数name

```html
 name:'home'
```

配置了name后，可以通过一个对象进行路由跳转

必须加冒号：动态路由传递params，所以在 this.$router.push() 方法中path不能和params一起使用，否则params将无效。需要用name来指定页面。但是可以使用path和query

```html
:to="{path:'/home',query:{id:12344}}" //合法
:to="{path:'/home',params:{id:12344}}" //params不会显示
```

### 3，路由对象：this.$route

哪个路由被激活，路由对象就是哪个

路由：路由路径/路由参数？查询条件=参数

**属性**

**$route.path**：当前路由的路径

**$route.params**：当前路由的参数

**$route.query**：查询路由参数：this.$route.query.user

**$route.hash**：路由哈希值

**$route.fullPath**：完整路径

### 4，路由懒加载

当使用到路由时再加载

const Home = () => import('../components/Home')

### 5，路由嵌套

在路由A中嵌套一个路由B，路由B的路径必须声明在组件A的孩子中，然后就可以在路由A中直接使用router-link和router-view实现嵌套

```html
//路由A中的子路由
children:[{
path:'/home/home',
component:HelloWorld,
           },
           {
path:'/home/home',
component:HelloWorld,
            }]
```

## VueAPI之事件监听

- $emit('事件名',['参数1'，‘参数2] )发送事件

- `$on('事件名',回调函数)` 侦听一个事件
- 通过 `$once('事件名',回调函数)` 一次性侦听一个事件，下次再发送此事件时，无法侦听
- 通过 `$off('事件名',回调函数)` 停止侦听一个事件

父子组件一般直接监听子组件传过来的事件，以上API一般在bus事件中使用

如何实现bus总事件

```html
一、创建bus事件导出并在使用时导入bus
1，在main.j文件中创建一个bus
const Bus = new Vue()
export default Bus
2，import Bus from './Bus'
3，Bus.$once()

二、利用原型变量接收bus免去导入导出
Vue.prototype.$bus = new Vue()
使用时直接this.$bus
```

## Vue中的渲染函数

渲染函数就是render函数--render函数会将template组件编译成可视化的东西

template是将组件的内容动态化，但是渲染函数可以动态修改骨架（标签）

在组件中使用渲染函数，可以不写template，因为会覆盖。render函数的参数会带上createElement函数的引用，返回的也是createElement

```html
render:function(createElement){
return createElement()
}
```

createElement函数

在h函数中使用的数据是data和props，和普通组件一样，在组件中使用组件，传入的数据使用props传入

参数

一、标签名，必填

二、对象，一般放置属性值，例如class

```html
attrs: {
  设置name，id，style等属性
        }
domProps: {
    不可随意，是标签本有的属性，定义后会挂载在子组件dom上
	//title、innerHTML
  }
props: {
    传给子组件的参数
  }
on: {
   监听事件
  }
```

三、数组或对象，一般放置子节点的相关内容

this.$slots.default ---不修改，按照默认的

```html
[
    '先写一些文字',
    createElement('h1', '一则头条'),
    createElement(MyComponent, {
      props: {
        someProp: 'foobar'
      }
    })
  ]
```

其返回的并不是一个真实DOM，只是会告诉 Vue 页面上需要渲染什么样的节点，包括及其子节点的描述信息。这样的节点为“虚拟节点 (virtual node)”，也常简写它为“**VNode**”。“虚拟 DOM”是我们对由 Vue 组件树建立起来的整个 VNode 树的称呼

JSX：将render函数组件化

```html
render: function (h) {
    return (
      <AnchoredHeading level={1}>
        <span>Hello</span> world!
      </AnchoredHeading>
    )
  }
```

## Vue过滤器

使用场景：mastache语法和v-bind

```html
{{message | filterA}}
<div v-bind:id="message | filterA"></div>
代表message作为参数传给过滤器
```

可以串联使用过滤器，{{message | filterA|filterB}}，多重操作，将message传给filterA，然后filterA**返回值**传给filterB

1、filters也是vue实例中的一个options，可以在组件中定义

```html
filters: {
  capitalize: function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
```

2、也有全局的过滤器

```html
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})

new Vue({
  // ...
})
```

如果同时定义了全局过滤器和局部过滤器，会优先采用局部过滤器

## Vue SSR

服务器渲染：jsp = 前端 + java在一个页面

客户端渲染和服务器渲染（SSR）

客户端渲染优缺点：

优点：前后端分离。

缺点：前端响应较慢、不利于SEO

服务器端渲染：
优点：使前端耗时少、有利于SEO、解析模板的工作交给后端，客户端只需要解析HTML页面
缺点：不利于前后端分离，开发效率低，占用服务器资源。

SEO（Search Engine Optimization）搜索引擎优化，简单来说就是在搜索时提高本页面在专业领域上的排名。

优化途径：让自己的页面更可读更快可读，让浏览器认识它。

### 前端提高seo

1，标签语义化

2，减少嵌套

3，优化css选择器

4，减少http请求



服务器渲染（jsp，ssr，seo），swiper，viewport、压缩、x倍图。async异步请求调用promise

上次：图片精灵、bootspa命名规范、jq方法实现、icon命名、

# Vuex

## 1，Vuex简介

状态管理器，实际上是一个store仓库，响应式的修改state状态，包括三部分

- **state**，数据；
- **view**，以声明方式将 **state** 映射到视图；
- **actions**，响应在 **view** 上的用户输入导致的状态变化。

vuex将数据抽取出来，使得可以在任一使用到他的地方更改数据，并且在vuex中也会更新状态

在vue组件里面，通过dispatch（派遣）来触发actions提交修改数据的操作。

然后再通过actions的commit来触发mutations来修改数据。

mutations接收到commit的请求，就会自动通过Mutate来修改state（数据中心里面的数据状态）里面的数据。

最后由store（仓库）触发每一个调用它的组件的更新

## 2，Vue安装启动

1，下载vuex

```html
npm install vuex --save
```

2，引入vuex

```html
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
```

3，简单使用

```html
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
```

4，将仓库导出

```html
export default store;
```

5，在组件中使用--main.js引入

```html
import store from './store/store.js';
在vue实例中挂载store
```

6，在组件中使用

this.$store就可以拿到仓库

## 3，Vuex五种核心属性

vuex是单一状态树，一个单一组件树对应一个单一状态树

### 1，state

用于定义公共状态，数据在Vuex中并不是完全响应式的,当修改的属性在对象中不存在时,或使用 delete state.obj.address 删除对象的某个属性时，均不会响应.故使用 Vue.set(state.obj,'key','value') 和 Vue.delete(state.obj,'key') 进行删除/设置未定义属性.在Vue实例中使用计算属性监听,若在他处只是获取当时的state,并不会监听到实时响应

```js
computed:{
    count(){
        return this.$store.state.count
    }
}
```

#####  辅助函数：mapState

```js
// 引入辅助函数
import { mapState } from 'vuex'
// mapState参数为对象/数组，返回一个对象,供给computed
// 传对象时，可以修改属性名,混入普通属性
computed:mapState({
    count: 'count', // 直接拿到state中的数据
    Number: state => state.number, // 方法默认参数是 state
    fullName(){ // 正常的计算属性,不影响其他属性
      return this.fristName + this.lastName
    }
})
// 传数组时,不能修改属性名
computed:mapState(['count','number'])
// mapState混入computed
computed:{
	...mapState({}) // 一样
    ...mapState([]) // 一样
    fullName(){ // 正常的计算属性,不影响其他属性
      return this.fristName + this.lastName
    }
}
```

### 2，getters

类似于Vuex中的计算属性，操作过滤state，当返回值发生了改变才会被重新计算.因为也是实时响应的,在Vue实例中用计算属性监听,getters以获取属性的形式访问,默认有1|2|4个参数,顺序为 (state,getters,rootState,rootGetters),表示本模块的 state和getters,根store的state和getters

```js
getters: {
    doneTodos: state => { // 默认参数是 state
      return state.todos.filter(todo => todo.done)
    },
    showTodos: (state,getters) => { // 默认参数是state,也可以接受 getters 作为第二个参数
      return getters.doneTodos.length
    },
    showTodos: (state) => (id) => { // 返回一个函数,故获取一个函数,可以调用并传参
      return state.todos.find(todo => todo.id == id)
    }
}

// 访问
computed:{
    todo(){
        return this.$store.getters.doneTodes // 获取属性的方式
    },
    showTodo(){
        return this.$store.getters.showTodos('lyf') // 获取属性的方式
    }
}
```

##### getters辅助函数：mapGetters 

貌似无法传参数

```js
// 引入辅助函数,貌似使用mapGetters获取getters,无法进行传参
import { mapGetters } from 'vuex'
// mapState参数为对象/数组，返回一个对象,供给computed
// 对象时
computed:mapGetters({
    nameGetter_1:'nameGetter'
    nameGetter:'moduleA/nameGetter'
})
// 数组时
computed:mapGetters(['nameGetter'])
// 混入计算属性
computed: {  
    ...mapGetters([])
    ...mapGetters({})
}
```

### 3，mutations

mutations 类似于vue中的methods,一般来说,state只能在mutations中被修改,mutations也只能修改,他无法获取根store或者兄弟模块的getters，mutations，actions等,一般在vue的methods中使用

```js
mutations: {
    increment (state,name,age) { // 第一个参数是state,最多可以传两个参数,其余的无法接收,此处age永远为undefined
      state.count.name = name
    },
    increment (state,payload) { // 参数2为一个荷载,承载了所有属性
      state.count.name = name
    }
}

// 访问
methods:{
    handle(){
        this.$store.commit('increment','lyf') // 若传入多个参数,无法接收
        this.$store.commit('increment',obj) // 故传一个对象
        this.$store.commit('increment') // 不传参
        this.$store.commit({
            type:'increment', // 提交的事件名
            amount:10 // 附带的参数
            })
    }
}
```

mapMutations

不可以在辅助函数中传参数

```
methods:{
     ...mapMutations(['moduleAMutation']),
     ...mapMutations({
     paramMapMutation:'moduleAMutation'
     // 若想传参，只能绑定在事件上 <button @click="paramMapMutation({id:996,name:'Mr.Liu'})"><button>
     })
}
```

##### 常量代替mutation

即mutation事件名为一个常量,而不是一个字符串,将此类常量保存在同一文件夹中,以此进行管理

1，创建一个专门存储mutation事件名的文件：mutation-types.js

2，导出所有mutation事件

```html
export const SOME_MUTATION1 = 'SOME_MUTATION1'
```

3，在store中导入

```html
import * as mutationTypes from './mutation-types.js'
```

4，使用mutation

```html
mutations:{
   [mutationTypes.SOME_MUTATION1] (state){}
   }
```

5，发送事件时直接使用

```html
this.$store.commit(mutationTypes.SOME_MUTATION1)
```

### 4，actions

在mutation上进行异步操作，commit触发mutations事件,vue-devtools 能即时获取到事件,但此时数据仍在异步中不会变化，即无法响应state真实状态,actions就是用于解决此问题的.actions接收一个参数context,类似于store

```js
// context
context = {
    state,   等同于store.$state，若在模块中则为局部状态
    rootState,   等同于store.$state,只存在模块中
    commit,   等同于store.$commit
    dispatch,   等同于store.$dispatch
    getters   等同于store.$getters
}

// 使用actions
actions:{
increment(context){ // context类似于store，拥有commit方法
     context.commit('increment')
   },
increment({commit}){ // 解构出context的 commit
	 commit('increment')
   },
increment({commit},payload){ // 外界传入的荷载
	 commit('increment',payload.money)
   }
}

// 访问
methods:{
   this.$store.dispatch('increment')
   this.$store.dispatch('increment',{money:20})
   this.$store.dispatch({type:'increment',money:20}) // 传参数
   this.$store.dispatch({type:'moduleA/increment',money:20}) // 传参数
}
```

##### 辅助函数：mapActions

和mutations一样,也是只能将参数放在html事件绑定上

```js
import {mapActions} from 'vuex'
    methods:{
    ...mapActions(['increment','moduleA/increment'] //映射发送事件
    ...mapActions({
        addIncrement:'increment' // 修改事件名
    })
}
```

##### 组合actions

若在actions中进行异步操作,可以在一个actions完成后在触发另一个actions,实现调用依赖和顺序

```js
// 在vue中
this.$store.dispatch('moduleA/actionA').then(()=>{
    this.$store.dispatch('moduleB/actionB')
})

// 在其他actions中
actionB ({ dispatch, commit }) {
    return dispatch('actionA').then(() => {
        commit('mutations')
    })
```

### 5，module

虽然是单一状态树，但是可以将一个状态划分模块（module），每一个模块实现state、mutation、actions、getter

1，定义局部状态

```js
定义一个module
const moduleA = {
state:()=>({}), // state:{} // ?区别
mutations:{},
}
```

2，在仓库中挂载状态

```html
const store = new Vuex.Store({
 modules:{
   modeluA
   }
})
```

3，访问某个模块

```js
this.$store.state.moduleA.count
this.$store.commit('moduleA/count')
this.$store.dispatch('moduleA/count')
```

### 命名空间

为module取名字,当不使用**命名空间**时，发送commit和dispatch事件时,module中的action和mutation同名事件也会被触发.在有命名空间的模块中,访问以'模块名/事件'的形式,若没有使用命名空间,此种访问方式也会出错.

```js
// moduleA中
increment(state, payload) {
        console.log('我是moduleA的increment');
        state.count += payload.count // 未触发前 $store.moduleA.count 为 10
    },
        
// rootMutation        
mutations: {
    increment(state, payload) {
      state.count += payload.money; // 未触发前 $store.count 为 1
    },
  },
      
this.$store.commit("increment", { count: 10, str: "10" }) // 触发 increment 事件
this.$store.commit("moduleA/increment", { count: 10, str: "10" }) // error:unknown mutation type: moduleA/increment

this.$store.count // 11
this.$stroe.moduleA.count // 21
```

#### namespaced

为一个Boolean值,为 true 时表示为一个命名空间

```js
namespaced: true
```

在命名空间下挂载事件

```js
this.$store.state.login.useName
this.$store.getters["login/localJobTitle"]
this.$store.dispatch("login/alertName")

...mapState('test1',['increment'])
...mapGetters("login", ["localJobTitle"])
...mapActions('模块名字1',['increment'])
...mapActions('模块名字2',['increment'])
```

 #### 在模块中使用全局

模块中的 getters 和 actions 可以访问到全局的 state 和 getters .

- getters

```js
someGetter(state, getters, rootState, rootGetters){ // 作为参数3和4
   getters.Getter // 这是局部的getters
   rootGetters.Getter // 全局的getters
}
```

- actions

```js
someActions(context){
    // context 包含 {dispatch,state,commit,getters,rootState} // 貌似只能访问全局的state
}

// 解构写法
someActions({dispatch,state,commit,getters,rootState}){}
```

#### 发送全局事件

因为在context中,只能获取全局rootState,但是也能发送全局事件的,将dispatch属性的参数3设置为对象,包含root属性,既能

```js
// moduleA
actions:{
    someActions({dispatch}){
        commit('someMutations',{}) // 实际触发 moduleA/someMutations
        commit('someMutations',{},{root:true}) // 实际触发 someMutations
        dispatch('someActions',{}) // 实际触发 moduleA/someActions
        dispatch('someActions',{},{root:true}) // 实际触发 someActions
    }
}
```

#### 在模块中注册全局actions

actions事件为对象,并设置root属性,将actions放置在handler中

```js
// moduleA
actions: {
    someAction: {
        root: true, // Boolean值,表示为全局action
        handler (namespacedContext, payload) { ... } // 调用someAction时的函数体
    }
}
```

## 4，严格模式

即在Vuex.store({})的参数中设置strict属性,添加此属性后，不是由mutation发出的状态改变，会抛出错误

```js
strict: true
```

## 5，vuex实现双向绑定

在计算属性中设置

```js
<input v-model="message">

computed:{
    message:{
        get(){
          rerurn this.$store.state.message
            }
        set(value){
            this.$store.commit('updateMessage',value)
        }
    }
}
```

## 6，热重载

什么是热重载：不需要刷新页面，就进行重新加载



# Vue ui

1，启动vue ui

在终端输入 vue ui

2，

# Vue组件库

## 1，ELement UI

## 2，iview

在脚手架3中不需要按需加载

## 3，ant-design-vue

npm install ant-design-vue moment

在main.js文件中使用

import {Button} from "ant-design-vue";

在vue.config.js中添加

```html
module.exports = {
  css: {
    loaderOptions: {
            less:{
                javascriptEnabled:true
            }
        }
    },
  };
```

在babel.config.js添加

```html
module.exports = {
  presets: ["@vue/cli-plugin-babel/preset"],
  plugins: [
    [
      "import",
      {
        libraryName: "ant-design-vue",
        libraryDirectory: "es",
        style: true,
      },
    ],
  ],
};
```

# Vue/cli

## 脚手架安装

```html
npm install @vue/cli@版本 -g
```

#### 静态文件的区别

1、static中的文件不会经过编译的，打包后会生成dist文件夹，只是复制一遍。因此，static中建议放一些外部的第三方文件，而自己的文件放在assets。

2、assets中的文件会经过webpack打包，重新编译，因为webpack使用的是 commenJS 规范，所以才必须使用require。
3，static最好放不会变动的文件，assets放可能会变动的文件。

## 单元测试



# 缓存和网络请求

## axios

1，安装axios

npm install axios

2，使用axios

导入axios

在工具文件加创建axios.js文件

import axios from 'axios';

3，简单请求

- get

axios.get('路径名称+参数').then().catch()

axios.get('路径名称',{参数}).then().catch()

```html
axios.get('/user?id=123')
.then(function(){})
.catch(function(){})

axios.get('/user',{
params:{
id = 123
    }
})
.then(function(){})
.catch(function(){})
```

- post

axios.post('路径名称+参数').then().catch()

axios.post('路径名称',{参数}).then().catch()

```html
axios.post('/user?id=123')
.then(function(){})
.catch(function(){})

axios.post('/user',{
params:{
id = 123
    }
})
.then(function(){})
.catch(function(){})
```

4，并发请求

将请求封装为函数，作为数组的item

axios.all([请求1,请求2]).then(axios.spread((res1,res2)=>{两个请求现在都执行完成}))

##### axios.all()

##### axios.spread(回调函数)

```html
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
  }));
```

5，根据配置发送请求

```html
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
```

### axios拦截器

拦截请求，并进行相应的处理，尤其是登录

创建axios实例

常见属性：timeout、headers、baseURL

```html
let instance = axios.create({
headers:{
    baseURL: 'https://some-domain.com/api/',
    'content-type':'application/x-www-from-urlencoded',
    timeout:5000
   }
})
```

实现拦截器

1，添加请求拦截器---请求前

```html
axios.interceptors.request.use(function(config){
   //发送请求前的操作
    return config;
},function(error){
    //请求错误的操作
    return Promise.reject(err)
})
```

2，添加相应拦截器---也就是响应后

```html
axios.interceptors.response.use(function(response){
//对响应数据的操作
   },function(error){
//对响应错误的操作
})
```

3，发送网络请求

```html
return instance(config)
```

4，完整代码

```html
import axios from 'axios'

export function request(config) {
  // 1.创建axios的实例
  const instance = axios.create({
    baseURL: 'http://152.136.185.210:7878/api/m5',
    timeout: 5000
  })

  // 2.axios的拦截器
  // 2.1.请求拦截的作用
  instance.interceptors.request.use(config => {
    return config
  }, err => {
    // console.log(err);
  })

  // 2.2.响应拦截
  instance.interceptors.response.use(res => {
    return res.data
  }, err => {
    console.log(err);
  })

  // 3.发送真正的网络请求
  return instance(config)
}
```

6，发送请求

```html
import { request } from "./request";
export function getHomeMultidata(){
    return request({
        url: '/home/multidata'
    })
}

export function getHomeGoods(type,page){
    return request({
        url: '/home/data',
        params:{
            type,
            page
        }
    })
}
```

## localStorage



