# ES6

## 1，var和let

### 1，作用域

作用域的区别：全局作用域和块级作用域

全局作用域的变量都是window的变量

var a == window.a

ES5：全局作用域和函数作用域

ES6：全局作用域、块级作用域、函数作用域

块级作用域：{}，for中都是单独的作用域

在非全局作用域定义的变量，在作用域外不可访问

```html
{
 const a = 1;//作用域外无法访问
 var b = 2//可以访问
}
```

作用域链：变量的作用域构造作用域链，能否使用变量，使用同一变量的哪个，依靠作用域链决定

### 2，变量提升

#### 变量

ES5：所有被定义的变量，都会提升到作用域顶部

```html
var a = 1;
var b = 2
//等价于
var a,b
a = 1,
b = 2
```

故访问一个还未声明的变量是不会有错的

```html
console.log(a)//undefined
var a
```

ES6：不会提升变量

在作用域链上根据变量声明访问数据

```html
var v = 'Hello World';//如无再来全局作用域
(function(){
    alert(v);
    var v='I love you';//先在自己的作用域里找
})()
输出undefined，因为在自己的作用域里找到v，声明提前为undefined
```

#### 函数

只有函数声明式的函数才会提升

定义函数：function fun(){}/var fun = function(){}

形参与全局变量

当形参与全局变量命名相同时，在函数作用域修改的是形参，不改变全局变量

```html
var a = 100
function fun(a){
   console.log(a)
   a = 10
}

fun(1)//输出1
console.log(a)//输出100
```

#### var的缺陷

在for中，变量被提升至全局，当通过循环把变量赋值给btn[i]时成功，但是真正点击按钮触发事件时，循环早已完成，调用的i是全局的，也就是5

```html
var btn =document.getElementsByTagName('button');
       for(var i = 0; i&lt;btn.length;i++)  
       {
        alert('i = '+i)//页面加载后，会弹出来五个框，分别是0-4
         btn[i].addEventListener('click',function(){
           alert('i = '+i)//响应函数执行后，弹出来一个框，无论点谁都是5
           console.log('第'+ i +'个按钮被点击了!');
         })
       }
```

### 3，变量声明方式

let、var、import，class，function，const

## 2，数组解构赋值

1，数组解构

- 简单解构--左右皆为数组

```html
let [a,b,c] = [1,2,3]
```

- 模式匹配---当使用...赋值时，解构为一个数组

```html
let [head, ...tail] = [1, 2, 3, 4];
head:1
tail:[2,3,4]
let [x, y, ...z] = ['a'];
x:'a'
y:undefined
z:[]
```

允许设置默认值，当赋值解构不为undefined时，采用默认值

```html
var [x = 1] = []
x = 1
var [x = 1] = [null]
x = null
```

2，对象解构

不受位置限制，受属性名限制

```html
let { bar, foo } = { foo: 'aaa', bar: 'bbb' };
bar:'bbb',foo:'aaa'
```

- 取出变量的属性

```html
let {num,age,sex} = person
```

- 对象解构的实质---赋值给对应变量，如无指定则默认同名

```html
let {name:name,age:age,sex:sex} = {name:'LYF',age:18,sex:'female'}
//故若想拿出对象的值并赋给新变量
{name:Name} = {name:'LYF'}
//Name:'LYF'
```

- 对象嵌套解构

1，和数组嵌套

```html
var {people:[sex,{age}]} = {people:['LYF',{age:10}]}
//sex:'LYF'
//age:10，此时people为undefined
var {people,people:[sex,{age}]} = {people:['LYF',{age:10}]}
//此时people为一个数组
```

- 字符串解构

可以转化为数组

```html
var [a,b,c] = 'hello'
a = 'h'
b = 'e'
c = 'l'
```

对象的话是length

```html
let {length : len } = 'hello'
len:5
```

## 3，字符串新增方法

关于unicode：ES6使用'\u{编码}'

1，String.fromCharCode()

ES5：String.fromCharCode()

用法：将unicode字符转为字符

缺点：无法识别大于0xFFFF的字符

ES6：String.fromCodePoint()

可以传入多个参数，将第一个参数转义，并且和后面的参数合并成一个字符串

2，String.raw()

将\转义为双\，则浏览器就会显示这个\

3，string.repeat()

返回一个新字符串，根据传入的参数决定原字符串重复n次，若传入非整数，向下取整，传入负数或NAN，也出错

```html
'xixi'.repeat(-0.9)//''
"xixi".repeat(NaN)//''
"xixi".repeat('xixi')//''
"xixi".repeat('3')//'xixixixixixi'
```

4，padStart()，padEnd()

自动补全长度，第一个参数指定长度，第二个参数指定补全的代码，多删少重

Start从头开始补，End从尾巴开始补，若第一个参数小于原字符长度，不改变；若第二个字符不传，则是空格

"xixi".padStart(6,'abcd')//abxixi

5，trimStart()，trimEnd()

ES5：trim函数，去除字符串首尾空格

ES6：trimStart()，去除首，trimEnd()，去除尾

7，replaceAll()

ES5：replace()

用法：替换字符，第一个参数是要在原字符串中匹配的字符，第二参数是要替换的字符

ES6：replaceAll()

用法：将所有匹配的都替换掉

```html
'aaaaabdejhbb'.replace('b','c')//'aaaaacdejhbb'
'aaaaabdejhbb'.replace(/b/g,'c')//'aaaaacdejhcc'
'aaaaabdejhbb'.replaceAll('b','c')//'aaaaacdejhcc'
```

8，includes()，startsWith()，endsWith()

皆返回布尔值，判断是否包含在字符串中，第二个参数表示开始搜索的位置

- includes()---是否找到字符串
- startsWith()---字符串是否在头部
- endsWith()---字符串是否在尾部，第二个参数表示前n个字符

## 4，数值新增方法

八进制和二进制----0b(B)和0o(O)表示

```html
Number('0b111')  // 7
Number('0o10')  // 8
```

1，Number.isFinite()

无限则返回false，有限返回true

例如：NaN，-+Infinity，字符串，boolean

2，Number.isNaN()

检查是不是为NaN，若是，则返回true，不是，则返回false

3，Number.parseInt()

ES5：parseInt(12.3)

ES6：Number.parseInt(12.3)

4，Number.isInteger()

判断一个数值是否是一个整数，但是20和20.0都是整数

5，最小精度

Number.EPSILON === Math.pow(2,-52)

等价于2的负52次方，如有需求：例如不小于2的负10次方，就直接Number.EPSILON * Math.pow(2,-42)

6，安全整数

精准整数的范围为：-2^53-2^53

超过则不精准

Math.pow(2,53) + 1 == Math.pow(2,53)

Number.MAX_SAFE_INTEGER 和 Number.MIN_SAFE_INTEGER

表示精准整数的边界，即2^53-1和-2^53+1

Number.isSafeInteger()

判断是否在精准整数范围内

7，Math对象

1，Math.trunc()

返回数的整数部分，不是数就转成数字，无法转成数字的，就返回NaN

Math.trunc('foo') //NaN

2，Math.sign()

判断正负零非数值，也是先转成数字

- 当参数为 正数时，返回+1
- 参数为负数时，返回-1
- 参数为0，返回0
- 参数为-0，返回-0
- 其他值，返回NaN

Math.sign('foo')//NaN

3，Math.cbrt()

计算立方根

Math.cbrt('foo')//NaN

## 5，函数新增

1，参数默认值

function log(x , y = 1){}

当不传参数时，y默认为1

2，length属性

返回没有指定默认值的参数个数，需设置在尾参数

```ht
(function(a,b){}).length// 2
(function(a,b = 1){}).length //1
(function(a = 1,b){}).length// 0
(function(a, b = 1, c){}).length //1
```

3，作用域

当参数设置默认值后，就会有单独的作用域，首先指向参数作用域

```html
var x = 1
function fun(x,y = x){//默认y指向的x是**参数x**，如参数x不存在，则指向全局的x，若找不到报错,
var x = 2// 如没定义全局，同样报错
 console.log(y)
}
```

当参数默认是一个函数时，可以和另一个参数结合，修改另一个参数

```html
var x = 1
function fun(x,y = () => { x = 2}){
    console.log(x)//输出2
    }
fun()
```

4，rest参数

将多余变量放入数组中，可以传入不限的参数，也是最后的参数

```html
function add(...values){
 let sum = 0;
 for(var val of values)
   {
     sum +=val
   }
}
add(1,3,6,728)
```

5，严格模式

'use strict'  不能使用未声明的变量

当使用ES6的参数默认值、解构赋值、rest扩展运算，都不能使用严格模式

6，箭头函数

```html
(num1, num2)  => num1 + num2
 简单的传入数据，并返回数据
```

注意点：

1，没有this对象

2，不可以使用new

3，不使用arguments

4，不使用yield

调用栈：当函数被调用时，会形成一个调用记录，保存调用位置和内部变量，如调用A函数时，A函数内部还有B函数被调用，那么在A调用记录上方还有B调用记录，直到B将返回解构返回给A，B调用记录消失，也就是出栈，形成调用栈

尾递归优化调用栈---在return时调用自己，调用栈保存的永远是本身函数，而不会保存多次自己

7，使用toString()---将函数作为字符串返回

ES5 省略注释和空格

ES6 原本返回

## 6，正则新增

正则表达式：

```html
var reg = /表达式/修饰符
var reg = new RegExp('字符串','i')
var reg = new RegExp(/表达式/修饰符)//一个参数
var reg = new RegExp(/表达式/,'i')//报错
```

ES6：

```html
var reg = new RegExp(/abc/ig,'i')//变成/abc/i
```

修饰符：

i：不区分大小写

g：全局匹配，如不加则找到第一个就停止

字符串方法：

search()搜索--返回下标

replace()替换---传入需替换和被替换的字符串

```html
var str = 'the best famiy is who'
str.search(/bes/,g)  //5
str.search('bes')  //5

str.replace(/bes/,'mos')//'the most famiy is who'
str.replace('bes','mos')//'the most famiy is who'
```

test()检测---返回true和false

```html
用正则表达式来匹配字符串
var reg = /bes/
reg.test("the best famiy is who")//true
```

## 7，数组新增

1，扩展运算符

reset将参数转为数组，扩展运算符将数组转为参数

```html
...[1,2,3]//1,2,3
```

在调用函数时使用作为参数使用，rest是一个在函数定义时作为参数传入使用

和reset不同的是：可以和正常参数结合使用

```html
fun(1,..[3,5],-10,...[55,10])
```

扩展运算符的作用：

1，复制数组

```html
var b = [...a]
```

2，合并数组

```html
b.push(...a)
var b = [...a1,...a2]//浅拷贝
```

2，数组新增方法

1,Array.from()

将对象转为数组---Array.from(arrayLike)

第二个参数---将转化为数组的数据进行处理

- 1，类数组的对象---arguments/nodeList对象

```html
var arrayLike = {//这是类数组的对象，因为它的属性名很像数组下标
'0':'a',
'1':'b',
length:2
}

var p = document.querySelectorAll('p')
```

2，Array.of()

将参数转为数组---弥补了array方法中只传一个参数时，将参数作为数组长度

```html
Array.of(3) // [3]
Array(3) // [,,,]
```

3，copyWithin()

将指定位置的成员**复制**到其他位置中，会修改原来的数组

数组.copyWithin(target,start,end)

- target：从该位置开始替换数据
- start：从该位置开始读取数据
- end：到该位置前停止读取数据

第一位决定从哪里开始替换，后两位决定替换内容和长度

```html
[1,2,3,4,5,6].copyWithin(0,3,5)
//[4,5,3,4,5,6]
[1,2,3,4,5,6].copyWithin(0,-3,-1)//负数从后往前
//[4,5,3,4,5,6]，截取的仍然是[4,5],不会倒序
```

4，find()和findIndex()

arr.find(参数一，参数二)

参数一：传入一个回调函数，找出符合该回调函数的第一个返回值为true的值，如无返回-1。

参数二：用于绑定回调函数的this

**回调函数的参数**

- 当前的值

- 当前的位置
- 原数组

```html
var arr = [1,4,7,10,2,0,11]
arr.find((value) => {
    return value > 10
})//11

function f(v){
  return v > this.age;
}
let person = {name: 'John', age: 20};
[10, 12, 26, 15].find(f, person)// 26
```

5，fill()

用于填充调用它的数组

arr.fill(参数一、参数二、参数三)

参数一：需要填充的东西

参数二：填充的起始位置

参数三：填充的结束位置，到这之前

```html
[1,4,6].fill(7,1,2)//[1,7,6]
```

若是使用对象给数组填充，实际上是浅拷贝，填充的几个位置都是指向同一个地址，一改则全部更改

6，遍历新增

entries()---对键值对的遍历

keys()---对键名的遍历

values()---对键值的遍历，相当于上述之和

```html
var arr = ['a','b']
let index of arr.keys()//0,1
let value of arr.values()//'a','b'
let [index,value] of arr,entries()//0 'a' 1 'b'
```

7，includes

判断数组是否包含某个值

参数一，需匹配的值

参数二，开始匹配的位置

8，flat()和flatMap()

flat()----将n维数组拉平，变成n-1维数组，可以传入一个参数，表示需要降的维数，传入Infinity时，不论多少层，都可以降成一维

```html
[[[1,2],4],2，,90].flat()
//[[1,2],4,2,90]//会自动忽略空格
[[[1,2],4],2，,90].flat(2)
//[1,2,4,2,90]
```

flatMap()---对数组的每一位进行操作，然后将返回值组成的数组执行flat()，**不改变原数组**，flat只能执行一层，同样可以找一个绑定this

```html
var arr = ['b','v','t']
arr.flatMap((val) = >{
   [val,val+val]
})
首先返回：[['b','bb'],['v','vv'],['t','tt']]
然后执行flat:['b','bb','v','vv','t','tt']
```

## 8，对象新增

1，简写

属性：{x:x,y:y}  == {x,y}

方法：add:function(){} == add(){}

2，name属性--返回函数名

3，属性的可枚举性

Object.getOwnPropertyDescriptor(obj,'foo')

获取一个对象的某个属性的所有信息

4，Object.is()

比较两个值是否严格相等

```html
NaN == NaN //false
+0 === -0 //true
{} == {} //false
Object.is(NaN,NaN)//true
Obect.is({},{})//false
Object.is(-0,+0)//false
```

5，Object.assign()

用于合并对象到第一个参数中

```html
var obj = {}
var obj1 = {a:1,b:2}
var obj2 = {b:3,c:5}
Object.assign(obj,obj1,obj2)
//obj = {a:1,b:3,c:5}
```

6，__proto__属性

当前对象的原型对象

7，Object.setPrototypeOf()

设置对象的原型变量，修改此变量时，对象也可以取到

```html
Object.setPrototypeOf(obj, proto);
proto.name = 'lyf'
//obj.name = 'lyf'
```

8，Object.getPrototypeOf()

用于读取一个对象的原型对象

## 9，symbol

类字符串的数据类型，不能使用new构造，每一个symbol都是唯一的

```html
let s1 = Symbol()
let s2 = Symbol()
let s2 = Symbol('str')
s1 != s2
console.log(s1) //'Symbol('str')'
```

当传入对象时，调用对象中的toString方法，将其转化为字符串，再生成Symnol值

1，不能和其他类型值一起使用

```html
let s = Symbol()
s + 'i am a roport'//报错
```

2，避免显示打印整个表达式

```html
s.description //'str'
```

## 10，Set和Map

set是一个集合，和数组的区别是没有重复

var s = new Set()

s.size//类似于数组长度

```html
[...new Set(array)]//数组去重
[...new Set('ababbc')].join('')//字符串去重
```

- add()方法
- has()方法
- delete()方法

map是一个对象，看接收一个数组作为参数，然后每个键值对作为参数

```html
const map = new Map([['name','罗雨凤'],['age','18']])
```

当键为数组或对象时，不认为是同一个键，因为都是对象的不同实例

```html
map.set(['a'], 555);
map.get(['a']) // undefined
```

map的遍历

1，.keys()----返回键

2，.values()---返回值

3，.entries()---返回成员

4，.forEach()---遍历成员

## 11，class类

```html
class num {
age = 18
 constructor(name){//构造函数，当实例化类时，会执行这个构造函数，传入的属性也会传入构造器
this.name = name//this指向实例对象
}
name(){}//定义在类的原型上，实例化并不会显示，但可以使用
this//指向实例化对象
this.age//不能直接拿，要使用this
}
```

类的方法定义在prototype上

```html
class Point{
constructor(){}
}
等价于
Ponit.prototype = {
constructor(){}//且不可枚举
}
```

每一个类都有隐式的constructor()方法。默认返回this

在调用时，必须使用new关键字

```html
var person = new Person()
```

存值和取值函数：默认存在get和set方法

静态方法 修饰符：static，实例不继承该方法，只能通过类名调用，不能通过实例对象调用，可以与非静态方法同名，其this指向类，而不是实例，且静态方法不能访问类内非static成员变量和方法，同理，共有方法也不能访问静态变量

```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```

原型方法：在原型或类上定义的方法只能通过实例对象调用，不能使用类名调用

类的继承

通过extends关键字，可以继承父类的静态方法，共有属性

```html
class Person(){}
class Student extends Person()
```

super关键字实现继承，继承时必须在构造函数中使用super()。

```javascript
class superNum {
  constructor(name) {
    this.name = name;
    this.height = 1.88;
  }
  fullName() {
    console.log("name:" + this.name);
  }
}

class subNum extends superNum {
  constructor(name, age) {
    super(name);//可以修改继承的name
    this.age = age;
  }
}
```



私有属性和方法

只有在实例中可以访问，而且可以定义同名的私有属性和公共属性

1，在方法上加_

- 或将私有方法封装到外部中

```html
class Widget {
  foo (baz) {//在公共方法中调用call，将bar成为类中私有方法
    bar.call(this, baz);
  }
}

function bar(baz) {
  return this.snaf = baz;
}
```

- 或使用symbol的唯一性定义方法名

```html

```

2，在属性上加#

- 

## 12，promise函数

解决回调地狱，自动回调下一层then，知道最后一层，当一层有return时，作为参数传入下一层then，当没有return时，传入undefined，不论是resolve还是reject都自动到下一层的resolve

```html
var p = new Promise((resolve,reject) =>{resolve()|| reject()})
```

1，若reslove的参数是一个promise，那么，根据参数中promise的状态决定调用resolve还是reject

2，then函数和catch函数

- then函数可以调用resolve和reject函数，或只包含resolve函数
- 在resolve函数中返回的是promise对象
- then会函数队列中，而且根据层排队执行

```html
p.then(resolve=>{},reject=>{})
p.then(resolve=>{})

p.then(resolve=>{
return 'bbb' 
//等价于 new Promise.resolve('bbb')，执行后面的then的resolve函数
}).then(resolve =>{
return 'ccc'//等价于 new Promise.resolve('ccc')
})

 p.then(
        (res) => {
          console.log("第一次打印：" + res);
          return "bbb";
        }
      ).then(
          (res) => {
            console.log("第二次打印：" + res);
            return "ccc";
          },
        )
//如果按照这个调用两次，则会输出：
第一次打印：aaa
第一次打印：aaa
第二次打印：bbb
第二次打印：bbb
```

- catch函数
- 可以包括reject函数，也可以抛出异常、
- 当链式promise对象产生错误时，不论是第几个then，总会catch按顺序被调用

```ht
catch(error=>{})//等价于then(null,reject=>{})
then(res =>{ throw new Error('test')}).catch(error =>{console.log(error)})//'test'
```

3，all()和race()和allSettled()和any()

all()类似于axios中的all，传入数组，item都是promise对象，当数组中的所有都返回resolve时，all执行resolve，res也是promise数组返回的数组，当出现reject时，就立即执行reject，结果就是reject那个

race()也传入数组，检测谁变化，就参考谁，可能reject也可能resolve

allSettled()不会相all一样出现reject就短路，而是执行完输出结果

```html
all()输出：
['a','b','c']
allSettled()输出：
[0:{status:'fulfilled',value:'a'},
1:{status:'fulfilled',value:'b'},
2:{status:'rejected',value:'c'}]
```

any()，当有完成resolve的，就执行完成，当全是reject时，执行reject

4，promise吞掉错误

当promise出现错误时，会抛出，但程序仍然进行，不影响后续进程

5，finally()

不管catch还是then，都会执行这个方法

## 13，Iterator

遍历器：可以遍历不同的数据结构，本质是一个指针，创建时指针指向起始位置，每调用一次next()，就向后指，并返回所指成员的信息，最return也是一个next。

属性为value和done，value表示遍历的值，done表示是否遍历完成，无则false，完成则true

```html
for...of遍历   for...in遍历
```

在for..in中，遍历键，在for..of中，遍历键值

## 14，Generator函数

- yield关键词定义变量

- *号连接function和函数名
- 使用实例时不能使用new构造

使用Generaotr时，需要使用next调用表达式，遇到yield停止

当next调用遍历器对象时，不传参数，yield定义的表达式为undefined，当传参数时，就将参数赋值给上一个yield

```html
function * Person(){
console.log('start')
var x = yield '1'
console.log('1'+x)//不会输出x
var y = yield '2'
console.log('2'+y)//不会输出y
var z = yield '3'
console.log('3'+z)//不会输出z
}
var person = Person();
person.next(10);
// 执行前两句
// 将10作为第0个yield的返回值
// 第一句打印：start
// 第二句返回：{value: "1", done: false}
person.next(20);
// 执行三四句
// 将20作为第1个yield的返回值
// 第三句打印：120
// 第四句返回：{value: "2", done: false}
person.next(30);
// 执行五六句
// 将30作为第2个yield的返回值
// 第五句打印：230
// 第四句返回：{value: "3", done: true}
```

return方法

直接结束Generator函数，也就是done变成true，将传入的参数作为value返回，不传就是undefined

```html
person.return("per");// 不管是否还有yield，{value: "per", done: true}
person.next();//已经结束，返回{value:undefined,done:true}
```

若是try...fianlly，则直接进入finally块

throw方法

调用时抛出异常，但是在函数中捕获

```html
var function * g(){
     try{
     }catch(e){//函数中捕获
            console.log('catch',e)
       }
}
g().throw('a')//函数外抛出
//catch a
g().throw('b')//因为catch已经执行，所以不抛出
```

next和throw和return的异同

三者都将表达式替换，next将表达式替换为参数，throw将表达式替换为throw语句，return将表达式替换为一个return语句

yield*表达式

在构造器中使用一个构造器

```html
function* bar() {
  yield 'x';
  yield* foo();
  yield 'y';
}
// 等同于
function* bar() {
  yield 'x';
  yield 'a';
  yield 'b';
  yield 'y';
}
```

和for...of循环

for...of循环可以遍历Generator函数中的yield，不需要next()

构造器中的this

无法访问this，也无法使用new

使用call绑定构造器中的this，将this绑定给一个空对象

```html
function F(){
this.a = 1//普通访问失败
}
var obj = {}
var f = F.call(obj)//将F的this绑定到{}中并返回
f.next()
f.next()
obj.a
```

将obj转化到f中，不要另外的对象，绑定到构造器的原型属性中，prototype

```ht
var f = F.call(F.prototype)
```

## 15 async函数

作为构造器的语法糖

```html
const f1 = function *(){
const f1 = yield readFile();
}
//改写为
const f1 = async function(){
const f1 = await readFile()
} 
```

await的作用：当遇到await时，函数内部就先暂停，当执行完await的异步操作时，再回来继续执行

返回一个promise，在then方法中接收

## 16 proxy

代理：

检测是否是本地发送请求

解析一条url：协议+主机+文件名+请求参数

location.host：返回当前 URL 的主机名称和端口号。

location.protocol：返回当前url的协议

```html
/127\.0\.0\.1:|192\.168\.|localhost:|test|118\.126\.96\.106/.test(location.host) ||/file:/.test(location.protocol)
```



