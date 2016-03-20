#if判断
- if在js中是做判断的，所谓做判断，就遇到不同的情况，做不同的处理。
- 在js中
> = 是赋值（改变）
> == 接近与数学中的等号，但在js中主要做判断用，判断两边是否相等

- 一个简单的if判断函数实现下拉菜单的显示隐藏（和纯css相比有哪些优缺点？）

 ```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title> 鼠标移入移出 </title>
<style>
#div1 {
    width: 200px;
    height: 200px;
    background: red;
    display: none;
}
</style>
<script>
function showHide() {
    var oDiv=document.getElementById("div1");
	
    // 如果条件写=='none'，会出现需点击两次的情况，我的逻辑能力真的差
    if (oDiv.style.display=="block") { // ==判断用，最开始写成=出错
        oDiv.style.display="none";
    }

    else {
        oDiv.style.display="block";
    }
}
</script>
</head>
<body>
    <input type="button" value="showHide" onclick="showHide()" />
    <div id="div1">
    </div>
</body>
</html>
 ```
- 可以为`<a>`链接添加js，相比将`<a>`的值定为`#`，域名没有变化，见代码：
```
<a href='javascript:;'> // js中的值为空，当然也可以添加代码，比如加个alert(a)
```