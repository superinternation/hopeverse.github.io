---
layout: post
title: "js中什么是真什么是假，关于ie、火狐以及谷歌浏览器下获取非行间样式的方法"
author: "hopeverse"
---
 

记录一些简单的关于什么是真什么是假，判断的问题，以及在ie、火狐、谷歌浏览器下使用currentStyle、getComputedStyle来获取行间样式的方法。

<br/>

### 什么是真，什么是假

>在if中写的条件，那么它会自行转换成true或false

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <script>
        window.onload=function(){
            var a = 0;   // 可以等于数字，字符串，数组，等等。。。。
            if(a){       // 直接判断是否是数字，字符串，数组，等等。。。。
                alert("is really");
            }
            else{
                alert("no really");
            }
        }
    </script>
</body>
</html>

```

**真：true ，非零数字 ，非空字符串 , 非空对象**  
**假：flase ，数字零 ，空字符串 ，空对象 ，undefined**

<br/>

### currentStyle方法

>ie下获取非行间样式的方法

```
<script>
        window.onload = function() {
                var odiv = document.getElementsByTagName("div")[0];
                alert(odiv.currentStyle.width);  
                //仅仅只支持ie浏览器下的获取非行间样式
            }
</script>   

```

<br/>

### getComputedStyle方法

>火狐和谷歌浏览器下获取非行间样式的方法

```
<script>
        window.onload = function() {
                var odiv = document.getElementsByTagName("div")[0];
                alert(getComputedStyle(odiv,false).width);  
                //火狐和谷歌浏览器下的获取非行间样式方法
            }
</script>

```

<br/>

### 兼容各浏览器

>可以在ie、火狐和谷歌浏览器中共同兼容，获取非行间样式的方法

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    * {
        margin: 0;
        padding: 0;
    }
    
    div {
        background: yellow;
        width: 200px;
        height: 200px;
    }
    </style>
</head>

<body>
    <div></div>
    <script>
    window.onload = function() {
        var odiv = document.getElementsByTagName("div")[0];
        if (odiv.currentStyle) {
            alert(odiv.currentStyle.width);
        } else {
            alert(getComputedStyle(odiv, false).width);
        }
    }
    </script>
</body>

</html>


```

>其中用if(obj.currentStyle)来进行判断是因为，在ie浏览器下alert(obj.currentStyle)返回了一串字符串，证明在ie下是用这个方法是有东西的，是非空的。然后在谷歌或者火狐浏览器下，alert(obj.currentStyle)返回的是undefined，是未定义的。那么根据最开始我们了解的，什么是真什么是假，就可以得出，使用if就可以来解决这个浏览器的兼容问题了。

<br/>

### 封装非行间样式的方法

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        div{
            width: 300px;
            height:400px;
            background: red;
        }
    </style>
</head>
<body>
    <div></div>

    <script>
        function getStyle(obj,name){
            if(obj.currentStyle){
                return obj.currentStyle[name];
            }
            else{
                return getComputedStyle(obj,false)[name];
            }
        }

        window.onload=function(){
            var odiv = document.getElementsByTagName("div")[0];
            alert(getStyle(odiv,"height"));
        }
    </script>
</body>
</html>

```

>这里需要注意的是，封装的函数中要使用return返回，并且将name之前的.用[]来表示，否则将不能使用封装的方法，还有最后在调用的时候，要将需要返回的某个样式用双引号框起来

>css(obj,"width")   获取样式
>css(obj,"width","200px")  设置样式

<br/>

### 复合&单一样式

>复合样式:background、border
>单一样式:width、height、position

**currentStyle和getComputedStyle只能取单一样式，不能取复合样式，那么就是去说如果要取background，是无法取到此非行间样式的，一定要取的话，那么修改为backgroundColor就可以了**

<br/>

>如需转载，请注明出处。谢谢！

[https://liutianzhu.me](https://liutianzhu.me)