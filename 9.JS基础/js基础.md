#JS基础
> - JS组成，js不是一个整体，或者说他是一个整体，但不是严肃的像块砖头一样，而是有三部分组成。
> - 变量，分不同类型，并且类型是可以检测的。不同数据类型是可以转换的，怎么转换，为什么转换，在什么时候转换是重点。
> - 变量的作用域和闭包（难点，啥是闭包？）。
> - 命名规范，舒服，合理，让别人看得懂。
> - 运算符，很简单，但很重要，是后面学习的基础。
> - 程序流程控制，判断，循环，跳出，真假等。
> - Json，好重要的样子，经常看到。

####js组成
- ECMAScript:解释器，翻译。将人类语言写好的程序翻译成机器语言01，反之亦然。js当中最核心的部分，当然也只是提供了最基本的功能，比如加减乘除，定义函数变量等，如果仅仅是这些，js充其量只是一个计算器。
- DOM，`document`实际上指的就是`html`，即以`html`为对象模型。DOM赋予了js操作html的能力，是操作`html`的一个入口，比如获取，修改，创建元素都是通过DOM（`document`这个对象）完成的。
- BOM，让js可以操作浏览器本身，在js中有一个专门对象`window`，比如弹出，关闭窗口，或者复制文字到剪切板等跟浏览器打交道的操作统称为BOM。
---
- **兼容性**
- ECMA，几乎没有兼容性问题，简单嘛！
- DOM，有一些操作不兼容，但是都可以解决；
- BOM，没有兼容问题，因为完全不兼容，少用。

####变量类型
- 常见类型：`number`，`string`，`boolean`，`undefined`（没定义也是一种数据类型！），`object`，`function`

```
var a=12;
alert(typeof a); // number

var a='adfdkjfka';
alert(typeof a); // string

var a=true;
alert(typeof a); // boolean

var a=function() {
	alert('agdfd');
}
alert(typeof a); // function，函数也是一种数据类型

var a=document;
alert(typeof a); // object，对象是一个十分庞大的类型，好多东西都是object

alert(typeof b); // undefined，没定义也是一种类型

var b;
alert(typeof b); // undefined，js的变量本身没有数据类型，完全取决于它里面存的东西
// undefined存在两种情况
// 1.确实没定义（定义就是声明的意思，var ）
// 2.定义了，但没有给东西
```

- js当中变量的数据类型不会被限制，这样的灵活付出的代价是有点乱，所以**一个变量最好只存一种类型的数据**。

####数据类型转换
- 为什么要进行数据类型转换？因为很多时候默认的数据类型并不符合我们的要求。比如，两个文本框中的数据相加，默认是字符串，这样想得到数字求和，就要先将`string`转换为`number`
**字符串转数字**用`parseInt()`,如

```
var a='1';
alert(parseInt(a)+1); // 13 

// parseInt()工作时是由左往右扫描字符串，碰到第一个非数字就将前面的数字提取出，如
var a='12px32df'
alert(parseInt(a)+1); // 13

// 如果碰到字符串自一个字符不是数字，直接报NaN，Not a number，如
var a='ad12px32df'
alert(parseInt(a)+1); // NaN

```

- 注意，`NaN`和`NaN`是不相等的！有内部原因，也有js设计原因，甭管，如

```
var a=parseInt('abc');
var a=parseInt('def');

alert(a==b); // false
```

- 检测一个结果是不是非数字（`NaN`）用函数`isNaN()`,如

```
var a=parseInt('def');

alert(isNaN(a)); // true
```

- 求和程序见同文件夹下例程*9.2求和-isNaN()*

- `parseInt()`有个局限性，只能转换为整数，如要转换小数用其兄弟`parseFloat()`，如果不知道被转换的是小数还是整数，可以都用`parseFloat()`

```
var a=3.5
parseInt(a) // 3

var a=3.5
parseFloat(a) // 3.5
```
> `parseInt()`,或者`parseFloat()`都是**显式类型转换**，又叫强制类型转换，必须转，哪怕转出是`NaN`；还有**隐式类型转换**，没告诉计算机要转，默认就转了，做好事不留名，请叫我雷锋，典型雷锋是`==`，他的兄弟就不是雷锋了`===`，见下面例子：
> ```
> // ex1
> 
> var a=5;
> var b='5';
> 
> alert(a==b); // true    先转换相同类型，再比
> alert(a===b); // false  不转换，直接比
> ------------------------------------------
> //ex2
> 
> var a='12';
> var b='5';
> 
> alert(a+b); // 125,因为‘+’在js中即能字符串连接，又能数字相加，计算机这玩意很懒。。。
> alert(a-b); // 7，‘-’在js中只有数字相减一种功能，所以就给转了
> ```

####变量的作用域和闭包
- 变量作用域就是指边用的作用范围，引出**局部变量**，**全局变量**
> 局部变量，只能在定义它的函数内使用；全局变量，在任何地方都能用，例如
> ```
> //ex1
> function aaa() {
> 	a=12; // a为局部变量
> }
>
> function bbb(){
> 	alert(a);
> }
>
> aaa();
> bbb(); // 报错，a没有定义
>
> -------------------------------------------------
> //ex2
> var a //a为全局变量
>
> function aaa() {
> 	a=12;
> }
>
> function bbb(){
> 	alert(a);
> }
>
> aaa();
> bbb(); // 12
> ```

#闭包
- Blue讲之前查了下百度百科，评论相当经典：*上面基本上都不是人话，你很难从中得到有用的信息。*

- 简单讲，**闭包就是子函数可以使用父函数的局部变量**(还有高级应用，后面讲)，比如

```
function aaa() { // 父函数
	a=12; // a为局部变量

	function bbb(){ // 子函数
		alert(a);
	}

	bbb(); // 12
}

aaa();
```
- 闭包是个很自然的过程，写的时候不要想这是闭包什么的，要不然想着想着就乱了，比如之前用的（`window.load`是很自然的父函数）：

```
window.onload=function() { // 父函数
    var oTxt1=document.getElementById('txt1');
    var oTxt2=document.getElementById('txt2');
    var oBtn1=document.getElementById('btn1');

    oBtn1.onclick=function() { // 子函数，oTxt1并没有重新定义
        var n1=parseInt(oTxt1.value);
        var n2=parseInt(oTxt2.value);

        if(isNaN(n1)) {
            alert('您输入的第一个数字有误');
        }

        else if(isNaN(n2)) {
            alert('您输入的第二个数字有误');
        }

        else {
            alert(n1+n2);
        }
    }
}
```
####命名规范
- 命名规范
> - 可读性，尽量让别人看得懂，团队合作很重要；
> - 规范性，一般都遵守**匈牙利命名法**
- **匈牙利命名法**
> - 类型前缀，告诉别人是什么数据类型，比如`oDiv`，前面的`o`代表`object`，那你就不能`oDiv=12`了，12显然是`number`而非`object`。注意，类型前缀只在给变量取名时用，给函数取名时不用。
> ![匈牙利命名法前缀含义]("匈牙利命名法前缀含义")
> - 首字母大写，即驼峰命名法。




