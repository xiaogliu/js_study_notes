#选项卡
- `this`在js当中非常常用，他具体指**当前发生的事件**，比如选项卡中很多按钮，当点击哪个时，this就代表那个，实际上，可以理解为及时的变量。
> `this`，指当前发生的事件

- 看我写的这几行js都错了哪些地方！

 ```
//一组按钮点击后高亮
<script>
window.onload { // onload应跟一个函数
    var oDiv=document.getElementById('div1');
    var aBtn=oDiv.getElementsByTagName('input') // 漏了分号

        aBt.onclick=function() { // 一次只能错做一个元素的stylestyle，此处应该用数组
            this.class='active'; // class在js中是保留字，要用className,最开始都没用this，而是aBtn!
            // this.style.className='active'; // 加上style就错，why?因为class不属于style的子属性
        }
}
</script>
```
- 正确代码（不完整，点击后全部高亮，不能消失）

 ```
// 一组按钮点击后高亮
window.onload=function() {
    var oDiv=document.getElementById('div1');
    var aBtn=oDiv.getElementsByTagName('input');

    for(var i=0; i<aBtn.length; i++){ // 变量使用前必须声明
        aBtn[i].onclick=function() {
            // alert(this.value);
            this.className='active';
        }

    } // 大括号都能忘...
}
```
- 正确完整代码，点击后只有一个高亮
```
window.onload=function() {
    var oDiv=document.getElementById('div1');
    var aBtn=oDiv.getElementsByTagName('input');

    for(var i=0; i<aBtn.length; i++) {
        aBtn[i].onclick=function() {
            for(var i=0; i<aBtn.length; i++){ // 清除高亮
                aBtn[i].className='';
            }

            // alert(this.value);
            this.className='active';
        }
    }
}
```

> ==有个有意思的事，变量命名的时候经常会看到获取一个元素时是`oDiv`，如获取`id`，而获
> 取一组元素时是用`aBtn`，比如获取`tag`时，这里的*o*是*one*的缩写？*a*是*array*的
> 缩写？==

- 自定义属性
> 通过html添加的自定义属性，有些浏览器不认，通过js添加的自定义属性，所有浏览器都认

- 选项卡完整代码(markdown下面的代码为什么不能和this行对齐？)

```
<!-- 选项卡 -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title> ex </title>
<style>
#div1 .active {
    background: yellow;
}
#div1 div {
    width: 200px;
    height: 300px;
    background: #ccc;
    border: 1px solid #000;
    display: none;
}
</style>
<script>
window.onload=function() { // 加载完整个document后执行下js面代码
    var oDiv=document.getElementById('div1')       // oDiv的o是one的缩写？
    var aBtn=oDiv.getElementsByTagName('input')    // a是array缩写？
    var aDiv=oDiv.getElementsByTagName('div')   

    for(var i=0; i<aBtn.length; i++) {
        aBtn[i].index=i; // 自定义属性，写在html中有些浏览器不认（且多写代码）
        aBtn[i].onclick=function() { // 点击后才触发执行，先清空，再高亮/block，
            //alert(this.index);
            for(var i=0; i<aBtn.length; i++) { // 这里少了i++，chrome直接卡死了！
                aBtn[i].className='';
                aDiv[i].style.display='none';
            }

                this.className='active'; //this指的是这一个，所以不需要用数组表示
                aDiv[this.index].style.display='block'; // input下的div怎么对应？
        }
    }
}

</script>
</head>
<body>
    <div id='div1'>  <!-- 这里加个div并命名css中操作的时候方便 -->
        <input class='active'active type="button" value='股文杂谈' />
        <input type='button' value='新闻精选' />
        <input type='button' value='涨停分析' />
        <div style='display: block'> 1111 </div>
        <div> 2222 </div>
        <div> 3333 </div>
    <div>
</body>
</html>
```