# CSS

### 像素

**三种视口**

1，布局视口（layout viewport）

整个塞进去

2，视觉视口（visual viewport）

用户正在看的区域

3，理想视口（ideal viewport）

设备多宽，视口就多宽

**设备像素和css像素**

设备像素是物理屏幕，css像素是逻辑像素

在pc端，1设备像素 = 1逻辑像素

在移动端，苹果推出tetina屏幕，在尺寸没有变化的情况下，增加物理像素

1设备像素 ！= 1逻辑像素

 2设备像素 = 1逻辑像素

iPhone6,7,8都是**两倍屏手机，即一个CSS像素等于两个物理像素**。

**分辨率**

即显示器显示的小方块有多少

**二倍图和多倍图**

当一个css为50*50px的图片，二倍屏幕手机会将它显示为100x100px像素，也就是模糊

做法是准备一个100x100px的图片，缩放到50x50px，然后浏览器放大为100*100px像素，其实就是原来的，没有缩放

# Less

css预处理器

1，定义变量

@abc:10px

使用：width:@abc

2，混合

mixin--在一个选择器中调用另一个选择器

```html
.abc{
.bcd()//括号可选
可以继承它的所有属性
}
```

混合参数---在定义一个选择器时传入参数，供使用者灵活调用

```html
1,普通使用
.border(@width; @style; @color) {//可以定义默认参数
    border: @width @style @color;
}
.myheader {
    .border(2px; dashed; green);
}

2,arguments的应用
作为参数列表传入
.box-shadow(@x: 0; @y: 0; @blur: 1px; @color: #000) {
          box-shadow: @arguments;
等价为：box-shadow: 0 0 1px #000;
}

3，匹配模式
给匹配设置名字，调用时根据名字调用不一样的匹配，以及可以使用@_设置公共的属性
.mixin(dark; @color) {
  color: darken(@color, 10%);
}
.mixin(light; @color) {
  color: lighten(@color, 10%);
}
.mixin(@_; @color) {
  display: block;
}

.class {
  .mixin(light; #888);
}

最终编译为：
{
color: darken(#888, 10%);
display: block;
}
```

3，

&字符和@字符

&表示父级选择器

@表示同级，但优先

```html
.abc{
@media{
}
}
转为
@media{
.abc{
}
}
```

4，命名空间

使用一个类的某个嵌套子类

```html
#bundle(){
.button{
}
}
#bundle.button();
```

5，映射

使用一个类的属性

```html
#colors(){}
.button{
color:#colors[color]//拿到函数中的color属性
}
```

6，extend扩展语法

将其他的样式扩展到自己

```html
.style:extend(.contain)
此时style会包括自身样式和contain样式
```

7，
