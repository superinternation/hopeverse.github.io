---
layout: post
title: "js中创建元素节点以及在指定位置插入子节点的方法"
author: "hopeverse"
---
 
当我们需要在html中的子节点列表中插入一个子节点，那么我们需要有如下思路。


首先插入节点必须要先创建一个元素节点，那么创建完之后，如果是在最后插入子节点的话，那么就要使用到appendChild()，那么如果是要在指定位置插入子节点的话，我们要使用到insertBefore()方法来在指定位置插入子节点，最后如果我们需要删除某个子节点的话，那么则需要用到removeChild方法来实现效果，那么下面就具体记录了这几种方法：

<br/>

## CreateElement()创建元素节点

基本语法：``document.createElement("tagName")`` 

>tagName是需要创建的元素类型

<br/>
## appendChild()方法

基本语法：```appendChild(newNode)```

>appendChild()在指定父节点下，子节点列表最后插入一个新节点。
>newNode一般是创建完新节点之后所赋值给的对象()

如果结合**appendChild()**方法在子节点最后插入一个子节点，则是下方代码所示：

```
<body>
    <ul>
        <li>11</li>
        <li>22</li>
        <li>33</li>
        <li>44</li>
        <li>55</li>
        <li>66</li>
    </ul>

    <script>
        var oUl = document.getElementsByTagName("ul")[0];
        var newNode = document.createElement("li");
        newNode.innerHTML = "77";
        oUl.appendChild(newNode);
    </script>
</body>

```


> 这里需要注意一开始获取父节点的时候，如果是TagName记得要加上索引值
不然最后是没效果的。


效果图：

![zjjd1](/images/posts/cite/zjjd1.JPG)

## insertBefore()方法

基本语法：```insertBefore(newNode,xxnode)```

>newNode:这个参数指要插入的新节点。
>xxnode:这个参数指在某某节点之前插入。


如果是与**insertBefore()**方法混合使用的话，则如下方代码所示：

```
<body>
    <ul>
        <li>11</li>
        <li>22</li>
        <li>33</li>
        <li>44</li>
        <li>55</li>
        <li>66</li>
    </ul>

    <script>
        var oUl = document.getElementsByTagName("ul")[0];
        var newNode = document.createElement("li");
        var xxnode = oUl.getElementsByTagName("li");
        newNode.innerHTML = "hello world!";
        oUl.insertBefore(newNode,xxnode[3]);
    </script>
</body>

```


>这里特别要注意的是，因为要指定插入子节点的具体位置，那么必须还要获取tagName元素节点对象的集合才可以进行索引，并且！！！由于是getElementsByTagName()所以并不是访问节点，所以索引不算空白节点，那么就代表，按照正常的数组索引0，1，2，3取过来就好啦。并且！！！如果父节点下面的子节点列表中，元素节点并不是相同的元素，那么可以使用childNodes来进行索引。例：var t = xx父节点.childNodes (childNode记得这里类似数组) 

效果图：

![zjjd2](/images/posts/cite/zjjd2.JPG)

## removeChild()方法

基本语法：```nodeObject.removeChild(node)```

>nodeObject：一般指父节点
>node:需要删除的子节点

 如果是需要删除父节点下，子节点列表中的某个子节点那么就使用removeChild()方法来实现，则如下方代码所示：

```
<body>
    <ul>
        <li>11</li>
        <li>22</li>
        <li>33</li>
        <li>44</li>
        <li>55</li>
        <li>66</li>
    </ul>
    <script>
        var oUl = document.getElementsByTagName("ul")[0];
        var xxnode =document.getElementsByTagName("li");
        oUl.removeChild(xxnode[3]);
    </script>
</body>

```

>这里只需要获取父节点，然后获取子元素节点集合来进行索引，再通过这个方法删除对应的子节点就可以了。

效果图：

![scjd](/images/posts/cite/scjd.JPG)

> **从所以的实际操作来看，基本上访问节点创建元素节点，插入子节点都是在其父节点之下操作的，应该要多注意，而获取属性的方法，则可以直接获取元素之后使用，而不需要一定在父节点之下。**那么这一小节记录就到这儿了。如需转载，请注明出处！谢谢！

[https://liutianzhu.me](https://liutianzhu.me)