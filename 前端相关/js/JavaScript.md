# JavaScript

#### js执行

1，defer

推迟执行脚本：诉浏览器立即下载，但延迟执行，按照它们出现的顺序执行。

2，async

异步执行脚本：不必等脚本下载和执行完后再加载页面，同样也不必等到该异步脚本下载和执行后再加载其他脚本。异步脚本保证会在页面的 load 事件前执行。

3，动态加载脚本

只要创建一个 script 元素并将其添加到 DOM 即可。

```html
let script = document.createElement('script');
script.src = 'gibberish.js';
document.head.appendChild(script); 
```

### 工厂函数

工厂函数，就是指这些内建函数都是类对象，当你调用他们时，实际上是创建了一个类实例

自我理解：函数创造对象，对象都像工业品一样有一样的品质（属性）

```html
常见的工厂函数
function fun(name,age){
var obj = Object();
obj.name = name;
obj.age = age;
obj.sayName = function(){
	console.log(this.name)//this指的是调用函数的那个对象
};
return obj;
}

var obj1 = fun("罗雨凤",20)
```

## Promise函数

实现js代码多线程和异步编程

基本结构

```html
const promise = new Promise(function(resolve,reject){//参数是传入一个函数，函数中有两个参数，分别也是函数,用于回调
  if(条件){
    resolve(value)//需要自己定义
   }
   else{
    reject(error)//需要自己定义
}
})
```

如一旦调用了resolve函数，就是已完成的状态，就不会再调用reject函数了，同理，调用reject后也不回调用resolve

.then和.catch函数

用于给Promise对象调用，分别是resolve和reject函数的化身

1，.then函数

```html
1,定义resolve和reject函数
promise.then(resolve=>{},reject=>{})
2，定义resolve函数
promise.then(resolve=>{})
```







&&和||的使用

||可以代替if-else

&&可以代替验证

```
 var status=orderArray[i].status== 0 && "待支付" ||orderArray[i].status== 1 && "已支付" ||orderArray[i].status== 2 && "已收货" ||orderArray[i].status== 3 && "其它"
                td4.html(status); 
//                if(orderArray[i].status==0){
//                    td4.html("待支付")
//                }else if(orderArray[i].status==1){
//                    td4.html("已支付")
//                }else if(orderArray[i].status==2){
//                    td4.html("已收货");
//                }else{
//                    td4.html("其它")
//                }
```

## 对象的指针问题

对象保存的是地址，当修改一个对象时，其实修改的该地址保存的东西，当一个对象变成另一个对象时，地址也改变

```html
var obj //地址0*1000
var test = obj //地址同为0*1000
var obj.dom = { num: 1 };//修改地址0*1000内指向1*1000的东西
此时：obj和test都修改
obj = obj.dom//将obj的地址变成1*1000，此时和test已经不是一体的了
obj.dom = {XXX}//此时修改的是1*1000指向2*1000的东西，因为tset中包含1*1000,所以他也会修改
test->obj（0*1000）->obj.dom（1*2000）->obj.dom.dom（2*1000）
形成节点链表
```

形成链表---链表写法

```html
function ListNode(val) {
      this.val = val
      this.next = null;
  }
list = new ListNode(i);(0*1000)
returnList = list;
for(let i = 1;i<length;i++){
list.next = new ListNode()//（i*1000）
list = list.next
}
```

修改对象的方式：只能通过取属性，不然其实**不是**一个对象

```html
var obj = { num : 1}
obj.num = 2//修改属性
console.log(obj == test);//true
obj = { num : 2 }//修改对象本质
console.log(obj == test);//false
```

## 发送网络请求

### 一、原生ajax：

**ajax：异步javascript和xml**

1，判断是否有XMLhttpRequest对象

```html
if(window.XMLHttpRequest){
 var XMLHttp = new XMLHttpRequest()
}else{
var XMLHttp = new ActiveXObiect("Microsoft.XMLHTTP")
}
```

2，发送请求

XMLHttpRequest对象的方法和属性

- open-规定请求内容
- send-发送请求

```html
http.open(请求方式,url,是否异步)
当请求携带参数时，拼接在url后
http.open(
        "GET",    "https://api.apiopen.top/getWangYiNews?page=1&count=5",
        true
      );
此处的参数为：page=1&count=5
若写为json数据
{ "page": 1, "count": 5 }
```

3，监听状态变化

当异步请求时，需要监听

使用onreadystatechange监听请求状态，当**状态（readyState）**发生改变时，就调用此函数

可在内部根据请求返回的状态码确定是否请求成功

```html
http.onreadystatechange = function(){
   //这是成功的状态
if(http.readyState == 4 && http.status == 200){}
else{}
}
```

readyState状态

- 0：未请求
- 1：已连接
- 2：已接收请求
- 3：请求处理中
- 4：请求已完成

status：状态码

- 200：请求成功
- 404：未找到

4，请求成功后，接收返回的数据

```html
http.responseText
```

### 二、jquery和ajax

$.ajax(ulr,setting)

$.get()和$,post()，参数为url，data，和callback

```html
$(function(){
    $('#send').click(function(){
         $.ajax({
             type: "GET",
             url: "test.json",
             data: {username:$("#username").val(), content:$("#content").val()},
             dataType: "json",
             success: function(data){
                         $('#resText').empty();   //清空resText里面的所有内容
                         var html = ''; 
                         $.each(data, function(commentIndex, comment){
                               html += '<div class="comment"><h6>' + comment['username']
                                         + ':</h6><p class="para"' + comment['content']
                                         + '</p></div>';
                         });
                         $('#resText').html(html);
                      }
         });
    });
});
```

拓展：content-type的区别

- application/json
- application/x-www-from-urlencoded

json时将请求不处理，而from表单时处理成键值对?data1=value1&data2=value2，jq和ajax都是，且get时放置在url后，post则是放置在http body

## new的作用

调用一个函数时，不使用new，有无返回值取决于函数，而new，相当于返回了一个对象，里面包含了函数的this和原型

## 默认事件和冒泡事件

默认事件：不是我定义的事件，但它发生了。例如a链接点击变色跳转，input的enter，form表单的button（默认type="button"）即触发提交

冒泡事件：当触发元素时，也触发了祖先元素的同类事件。

阻止默认事件和冒泡事件的方法

1，原生js

在事件中传入e，判断是否有默认事件，有则取消

```html
function (e) {
          e.preventDefault();
        }

a标签阻止默认事件
<a href="javascript:void(0);">链接</a>
```

取消冒泡

```ht
e.stopPropagation()
e.cancelBubble()
```

2，vue

- @click.stop
- @clicl.prevent

## new的本质

实例化一个构造函数，new语法改变了我们调用函数时候的**this指向**，并返回了执行后的**this对象**

1，创建对象var obj = {}

2，对象的原型对象 指向 函数的原型 obj.__proto_= fun.prototype

3， 

4，将新对象返回
