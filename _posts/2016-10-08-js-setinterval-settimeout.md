---
layout: post
title: "setInterval()和setTimeout()定时器以及清除定时器的应用"
author: "hopeverse"
---

关于setInterval()、setTimeout()以及清除两种计时器效果的记录



<br/>

## setInterval()方法

基本语法：```setInterval(函数|可执行代码,交互时间);```

>此方法的特点是可以持续间隔，具体交互事件来再次调用函数代码，或者是需要执行的语句

使用setInterval方法，进行计时的效果：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        window.onload=function(){
            var a=0;
            obtn1 = document.getElementById("btn1");
            obtn1.onclick=function(){
                setInterval(function(){
                    document.getElementById("txt").value=a;
                    a++;
                },1000)
            }
        }
    </script>
</head>
<body>
    <input type="text" name="text" id="txt" />
    <input type="button" id="btn1" value="开始计时！" />

</body>
</html>

```

此功能实现的是从数字0开始，依次加一秒计时的效果。

<br/>

## setTimeout()方法

基本语法：```setTimeout(函数|可执行代码,延迟执行时间);```

>此方法的特点是仅仅只能使语句，进行一次调用，而不能持续调用交互。

使用setTimeout()方法，进行计时的效果：

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
    window.onload = function() {
        var a = 0;
        obtn1 = document.getElementById("btn1");
        obtn1.onclick = function rec() {
            setTimeout(function() {
                document.getElementById("txt").value = a;
                a++;
                setTimeout(rec(), 1000);
            }, 1000)

        }
    }
    </script>
</head>

<body>
    <input type="text" name="text" id="txt" />
    <input type="button" id="btn1" value="开始计时！" />
</body>

</html>


```

此代码效果是和上面计时器效果一样的。

>这里使用的是setTimeout()方法，虽然此方法原本自身只能调用一次函数语句，但是这里在自身setTimeout()中，再次调用自己，所以能够实现和setInterval()相同的效果。并且里面，由于为了方便再次调用这个点击函数，所以原本是匿名函数的，重新添加了名字。


综合案例：开始计时和结束计时

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
    window.onload = function() {
        var a = 0;
        obtn1 = document.getElementById("btn1");
        obtn2 = document.getElementById("btn2");
        obtn1.onclick = function() {
            setTimeout(function rec() {
                document.getElementById("txt").value = a;
                a = a + 1;
                x = setTimeout(rec, 1000)
            }, 1000)
        }
        obtn2.onclick = function() {
            document.getElementById('txt').value = 0;
            a = 0;
            clearTimeout(x);
        }
    }
    </script>
</head>
<body>
    <input type="text" name="text" id="txt" />
    <input type="button" id="btn1" value="开始计时！" />
    <input type="button" id="btn2" value="结束计时！" />
</body>

</html>

```

>这个效果需要最后注意重置数字为0

此案例效果是点击开始计时，从0开始往后累加，结束计时是定时器清零，并且暂停计时，如果再次点击，定时器从0开始重新计时。

<br/>

## clearInterval()和clearTimeout()方法

这两种方法只需要让setTimeout()方法，setInterval()方法赋值给一个id之后，直接clearInterval(id)，clearTimeout(id)，就可以实现清除计时器的效果了。

>**其中setInterval()和setTimeout()方法中，第一个参数是可以用双引号包括字符串来传入，那么这个传入的字符串，会在超时时间或者间隔之后进行求值。并且setInterval()第二个参数如果为0，那么代表无限次调用函数，即第一个参数。那么setTimeout()中第二个参数如果为0，那么指定函数不会立刻执行，相反，会进入队列，当所有处理程序全部执行完毕之后，在立刻调用此函数。**


>对于定时器的两种方法，以及清除方法简单的记录完成了，今后如有更深的理解，再进行详细更新记录.如需转载，请注明出处！谢谢!  

[https://liutianzhu.me](https://liutianzhu.me)
