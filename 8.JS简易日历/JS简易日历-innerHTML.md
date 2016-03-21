#JS简易日历-innerHTML，数组使用，字符串连接

- 和选项卡类似，但有不同，只写一个div，然后更改里面的`innerHTML`，这个算是html or js里面最有用的东西。其中如果给`innerHTML`赋值时是一段html代码，那么html代码中的元素会真的创建出来,比如：
```
oTxt.innerHTML='<h2>'+(this.index+1)+'月活动</h2><p> 快过年了，大家可以商量去哪玩~ </p>';
// 结果是 "<h2> 1月活动 <h2> <p> 快过年了，大家可以商量去哪玩~ </p>"，标签会起作用
```

- **什么时候声明变量：**
> 就web开发，js主要用于操作DOM，所以js将会操作什么元素，就将元素提取的方法声明个变量，后面
> 调用这个方法的时候直接使用声明过得变量就可以了。

- `css`语法相关:`link`标签中`type`属性可以省略，但`rel`不可以
```
<link rel='stylesheet' href='zns_style.css'>
```
- 字符串连接（拼接）
```
alert('abc'+'def') // abcdef
alert('abc'+12+5+'def') // abc125def，同数学中的加法，先两个两个加
alert('abc'+(12+5)+'def') // abc17def，提高优先级
```
- `innerHTML`可以给`input`以外的标签设置里面的文字。注意不要跟`value`混了，`value`是给`input`使用的。

- `数组`初步，注意啊，计算机都是从0开始计数的，比如，index。