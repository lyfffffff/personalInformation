# TypeScript

在vscoed中使用ts

新建js文件

使用tsc --init

打开json文件，取消outDir的注释，指的是编译到的路径，新建一个文件夹js存放编译后的js

编译ts文件：tsc 文件名.ts

ts中声明变量

var num:[变量类型，例如number] = 12

声明数组

var num:number[]

var num Array[变量类型:number]

声明函数

var fun = function (a:number,b:number):number{}

var fun:(a:number,b:number)=>number = function(a,b){}

与js的区别

js参数可选，传入参数的数可以不等于默认数，ts固定

默认参数，js默认参数在前，可以不传，ts默认参数不固定位置，但是至少传一个undefined

可选参数，即可以不传的参数，参数名后加问号：lastName?: string

所有参数

在js中，arguments为函数实参对象，可以通过数组形式拿取实参，arguments.callee引用函数自身，在ts中，可以使用一个数组接收剩余的参数...restOfName: string[]

类型兼容

基本类型（对象）：x兼容y，则y中含有x属性，小到大

函数兼容：x兼容y，则x中含有y中参数，大到小

```html
let x = (b: number, s: string) => 0;
let y = (a: number) => 0;
x = y; // OK
y = x; // Error
```

枚举对象兼容：枚举可以兼number，但是不兼容枚举
