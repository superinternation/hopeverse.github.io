---
layout: post
title: "createTextNode()创建文本节点以及与innerHTML的区别"
author: "hopeverse"
---
 
现在记录一下在元素中创建新文本节点的方法。


## CreateTextNode()创建文本节点

基本语法：``document.createTextNode("string")`` 

>string:字符串，这里就是创建文本节点的具体内容。

下面是例子一:

```
<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>

    <script>
        var oUl = document.getElementsByTagName("ul")[0];
        var oLi = document.createElement("li");
        var newText = document.createTextNode("hello world!");

        oUl.appendChild(oLi);
        oLi.appendChild(newText);

    </script>

```

效果图：

![cjwb1](/images/posts/cite/cjwb1.JPG)


例子二:

```
<head>
    <style>
        .main{
            width: 200px;
            height: 200px;
            background: yellow;
        }
    </style>
</head>
<body>
    <script>
    var oDiv = document.createElement("div");
    oDiv.className = "main";
    var newText = document.createTextNode("hello world!");
    oDiv.appendChild(newText);
    document.body.appendChild(oDiv);
    </script>
</body>

```

效果图:

![cjwb2](/images/posts/cite/cjwb2.JPG)

>所以我们可以记住以下思路，那么就是**首先创建文本节点需要想好在哪个父元素节点插入，然后创建新的文本节点，参数就是需要插入的内容，最后就是在父元素节点下插入新创建的文本节点。**

<br/>
## createTextNode()与innerHTML的区别

我们可能在运用createTextNode()方法的时候，感觉很熟悉，因为这个方法和innerHTML真的很像，那么我们就来说说这两者之间的区别到底是什么。请往下看~

例子一：createTextNode()方法插入文本:

```
<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>

    <script>
        var oUl = document.getElementsByTagName("ul")[0];
        var oLi = document.createElement("li");
        var newText = document.createTextNode("<strong>hello world!</strong>");
        oUl.appendChild(oLi);
        oLi.appendChild(newText);

    </script>
</body>

```

效果图：

![cjwbqb1](/images/posts/cite/cjwbqb1.JPG)

例子二：innerHTML方法插入文本:

```
<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>

    <script>
        var oUl = document.getElementsByTagName("ul")[0];
        var cLi = document.createElement("li");
        cLi.innerHTML = "<strong>hello world!</strong>";
        oUl.appendChild(cLi);
    </script>
</body>

```

效果图：

![cjwbqb2](/images/posts/cite/cjwbqb2.JPG)

>根据上面两组例子得出结论：**createTextNode()方法插入文本，只是纯粹是插入文本，额外的代码不会产生效果但是还是会和文本一起当成文本显示出来，innerHTMl方法插入文本的话，如果文字被html代码嵌套，那么代码的效果会在浏览器中解析出来。**

>如需转载，请注明出处！谢谢！

[https://liutianzhu.me](https://liutianzhu.me)
