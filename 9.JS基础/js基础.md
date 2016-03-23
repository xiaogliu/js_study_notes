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

> - ECMA，几乎没有兼容性问题，简单嘛！

> - DOM，有一些操作不兼容，但是都可以解决；

> - BOM，没有兼容问题，因为完全不兼容，少用。



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

> ![匈牙利命名法前缀含义](https://raw.githubusercontent.com/xiaogliu/js-study-notes/master/9.JS%E5%9F%BA%E7%A1%80/%E5%8C%88%E7%89%99%E5%88%A9%E5%91%BD%E5%90%8D%E6%B3%95%E5%89%8D%E7%BC%80.jpg "匈牙利命名法前缀含义")

> - 首字母大写，即驼峰命名法。



####运算符（部分常用）
- 算数：加`+`，减 `-`，乘 `*`，除 `/`，取模（取余）`%`
> `%`即取余数，比如`12%5 //2`,再比如`13%6 //1`。取余非常有用，比如隔变色，秒转时间。
```
// 隔行变色
<script>
window.onload=function() {
    var aLi=document.getElementsByTagName('li');
    for(var i=0; i<aLi.length; i++) { // 做个循环就可以吧所有的li选出来了！选择！
        if(i%2==0) {
            aLi[i].style.background='#ccc';
        }
        else {
            aLi[i].style.background='';
        }
    }
}
</script>
```
```
// 秒转时间
var a=1333;
alert(parseInt(a/60)+'分'+a%60+'秒');
```

- 赋值：`=`，`+=`，`-=`，`+=`，`/=`，`%=`
> 自增的写法：`i=i+1` or `i+=1` or `i++`，其中，`i++`每次只能加一个，要想循环加大于1的只能采取这样的方法，如每次+3，则`i=i+3` or `i+=3`.

- 关系：`<`，`>`，`<=`，`>=`，`==`，`===`，`!=`（不等于），`!==`

```
alert(5!=7); // true

alert(5!=5); // false
```

- 逻辑：`&&`与，`||`或；`!`否

```
// &&应用：判断是不是两位数
var a=7

if(a>9 && a<100) {
	alert('两位数')
    }

else {
	alert('不是两位数')
    }
// 不是两位数

-----------------------------------------

//!很好用，可以颠倒黑白，扭转乾坤，应用

alert(!true); // false

alert(!!true); // true

```
- 运算优先级：`()`括号

####程序流程控制（就是`if`，`for`这些结构）

- 判断：`if`，`switch`,`?：`
> - `if`里面可以有无数个`else if`，但只能有一个`else`
> - `switch`语法如下
> ```
> // switch的语法
> switch(变量) {
> 	case 值1：
> 		语句1
> 		break；
> 	case 值2：
> 		语句2
> 		break；
> 	....
> 	default: // 上面没有符合的语句执行语句n，可以省略
> 		语句n；
> 	}
> // ex，登录界面根据男女写欢迎语
> var name='abc'
> var sex='男'
> swithc(sex) {
> 	case '男'：
> 		alert(name+'先生，您好！');
> 		break;
> 	case '女'：
> 		alert(name+'女士，您好！');
> 		break;
> 	default:	
> 		alert(name+'您好！');
> 	}
> ```
> - `?：`三目运算符（三元运算符），`if` `else`的简写，做判断用（但复杂判断还是用`if`，用`?：`会很乱），三目语法如下：
> ```
> // ?:的语法
> 条件？语句1：语句2
> // 例子，判断单双数
> var a=35;
> a%2==0?alert('双数')：alert('单数'); // a%2==0不需要加括号
> ```

- 循环：`for`，`while`

- 跳出：`break`中断,`continue`继续，循环里面特有的两个语句，作用见下面代码：
```
// break
for(var i=0; i<5; i++) {
	if(i==3) {
    	break; // 中断整个循环
    }
    alert(i); // 只能弹出到2，当i=3时，break
}
// continue
for(var i=0; i<5; i++) {
	if(i==3) {
    	continue; // 只中断本次循环，后面的循环continue
    }
    alert(i); // 只是没有弹出到3，其他都弹出
}
```
- 什么是真，什么是假（暂时用不到，课程后面会大量用到。干吗用？）：
> - 真：true，非零数字，非空字符串（空格也是非空的），非空对象（document也是对象哇）
> - 假：false，数字零，空字符串，空对象（null），undefined

# JSON
- json是为了js而生的,是存储js**数据**的一种方法。json和数组有点像，也是**用来存东西的**，但json使用`{}`，用法见下：
> ```
> /*var a=12;
> var b=5;
> var c='abc';
> */
> var json={a: 12, b: 5, c: 'abc'}; // 数据之间用逗号分开
> 
> json.b++; // 放在json里面的数据可以像正常变量一样操作，比如++
> 
> alert(json.b); // 6
> ```

- json和数组的关系及区别
> ```
> // 字符串和数字之间的关系
> var json={a: 12, b: 5, c: 7};
> var arr=[12, 5, 7]
> 
> alert(json['a']); // 12，json的下表是个字符串（方括号可以代替所有js里面的点）
> 
> alert(arr[0]); // 12，数组的下表是个数字
> 
> // json没有length属性，循环用 for in，见下
> var json={a: 12, b: 5, c: 7};
> var arr=[12, 5, 7]
> d
> for(var i in arr) {
> 	alert('第'+i+'个东西'+arr[i]); // 第0个东西：12
> 	}
> 	
> for(var i in json) {
> 	alert('第'+i+'个东西'+json[i]); // 第a个东西：12（为啥不是json['i']？）
> 	}
> 	
> 	
> /* 关于循环的建议（后面会解释为什么）
> 数组: 还是用for 0 length
> json： for in
> */
> 
> ```
