---
layout: post
title: "get & setAttribute()获取元素以及设置元素的方法 "
author: "hopeverse"
---
 
初入DOM，记录一下关于getAttribute的笔记,相对于后面的知识点来说，这一小节还是比较好理解的，那么现在开始记录一下此刻心得了。

<br/>

**getAttribute()方法**

基本语法：```element.getAttribute(attributename)```

>此方法的意思就是通过元素节点的属性来获取它的属性值,它的参数只有一个。

下面是例子：

```
<body>
 <p id="wz" title="hello"></p>
    <script>
        var text= document.getElementById("wz");
        var hq=text.getAttribute("title");
        alert(hq);
        //最后弹出hello
    </script>
</body>

```
    
那么在上面代码中：

```
text.getAttribute("title")  //text只是获取的元素储存的对象
```

//  这是使用text含有提取的p标签，来用getAttribute()方法来获取特定的属性值，那么括号之内 **“ ”** 之中则是提取谁的属性值了。

因为上面代码当中有一p标签做为html的段落，其中已经有title属性了，那么我们要提取出title这个属性的话，那么就需要通过getElementById()方法来先获取这个p标签，所以需要在text下使用getAttribute()方法，来获取title值。
<br/>

>当然还需要注意的是，不仅仅是只能使用**getElementById()**的方法来获取元素，同样也可以使用getElementTagName()的方法来获取标签元素，那么返回的就是一个数组了，理所当然那么需要在获取的元素后面加上索引了。 例如：getElementByTagName("")[0]

<br/>



另外一个例子，使用getAttribute()方法获取某个不为空的属性的属性值（简单来说就是这个元素当中有属性的，都返回出它对应的属性值）看下面：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
 <ul>
    <li title="one">a</li>
    <li>b</li>
    <li title="three">c</li>
 </ul>
 
 <script>
    var oLi = document.getElementsByTagName("li");
    for(var i=0;i<oLi.length;i++){
        var t = oLi[i].getAttribute("title");  //这里注意一下，遍历全部li之后，首先要试试获取到底有没有这个属性，才能继续下面的判断。
        if(t!=null){
            document.write(t+"<br/>");
        }
    } 
 </script>
</body>
</html>

```

下面是最后正确的结果：title属性值不为空的为属性值为one，three的这两个li

![domget](/images/posts/cite/domget.JPG)

## setAttribute - DOM篇
<br/>
基本语法：```elementNode.setAttribute(name,value)```

>此方法的意思就是通过setAttribute()方法来增加一个自定义的属性和属性值，或者为已有的属性设置一个属性值。

//  这里（name，value）分别代表 （属性名，属性值）

下面是一个例子：

```
<body>
    <p id="intro">我的课程</p>
    <script type="text/javascript">
    var con = document.getElementById("intro");
    var t = con.setAttribute("title", "hello");
    alert(con.getAttribute("title"));
    //这里最后弹出最新的title属性的属性值
    </script>
</body>
```

>// 从上面代码可以看出来，要设置一个属性值，不一定先要获取该属性值，如果有必要，可以直接进行属性值的设置，括号中两个参数("属性"，"属性值")，都需要双引号括起来，那么最需要注意的就是，最后你需要更新你setAttribute()设置的属性值，一定要使用getAttribute()方法进行更新，如果如果你直接用  **alert(t);**  来更新你当时设置的属性以及属性值，这是错误的！因为当你设置完属性和属性值后，存储在你特定的容器(ps：这里是t )中时，js是不会自动更新的你所设置的属性的，所以，必须要重新使用X.getAttribute()（ps：x就是获取的元素，意思就是更新在谁里面获取某属性对应的属性值）方法来进行更新，才能在html中显示正确。

下面就是最后设置完成的效果：

![domset](/images/posts/cite/domset.JPG)

在这里，我们已经可以看到p标签中，元素内title属性以及属性值设置成功了。

<br/>
> **所以说获取元素属性的方法，直接获取元素之后，就可以来进行属性和属性值的获取以及设置了。**那么今天我们就把这两种通过元素节点，获取和设置元素属性和属性值方法的一些小笔记完成了。如需转载，请注明出处！谢谢！

[https://liutianzhu.me](https://liutianzhu.me)
