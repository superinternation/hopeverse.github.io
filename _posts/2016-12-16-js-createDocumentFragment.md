---
layout: post
title: "js性能优化之文档碎片"
author: "hopeverse"
---
 

这一小节记录下js性能优化之文档碎片createDocumentFragment，那么什么是文档碎片呢？

它其实就是可以帮助我们将所有的DOM节点，存放到一个地方，那么就是文档碎片里面，然后进行一次性加载渲染，而不是需要每一个添加一个节点就渲染一次，从而大大的提高了我们浏览器的渲染速度。 下面我们试一试不进行文档碎片处理的渲染速度：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
     <ul id="ul1">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
     </ul>

     <script>
        window.onload=function()
        {
            var oUl = document.getElementById('ul1');
            for(var i=0;i<10000;i++)
            {
                var oLi = document.createElement('li');
                oLi.innerHTML = "hello" ;
                oUl.appendChild(oLi);
            }
        }
     </script>
</body>
</html>

```

大家可以亲测一下上面的代码，分别在chrome和ie下进行对比试试。我们可以得出，在chrome下就算插入了10000个子节点，那么浏览器打开的速度也是很快的，换过来在ie下打开，加载这么多个DOM节点，打开浏览器之后，完全渲染出来的时间差不多有10秒多的样子。所以在这种情况下，性能优化的必要性就很明显了。

<br/>

那么下面就开始测试一下：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
     <ul id="ul1">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
     </ul>

     <script>
        window.onload=function()
        {
            var oUl = document.getElementById('ul1');
            var oFgm = document.createDocumentFragment();
            for(var i=0; i<10000;i++)
            {
                var oLi = document.createElement('li');
                oLi.innerHTML = "hello";
                oFgm.appendChild(oLi);
            }

            oUl.appendChild(oFgm);
        }
     </script>
</body>
</html>

```

那么最后我们使用了createDocumentFragment方法创建了文档碎片之后，明显的不管是chrome还是ie打开速度已经都差不多了，所以在性能优化上面有了明显的提升。 这个方法的具体思路就是，创建好文档碎片createDocumentFragment，然后把所有的oLi全部都插入到文档碎片中去，文档碎片相当于一个袋子，那么所有一切都装好之后，我们再一次性插入到oUl里面，这样我们就省去了每次添加一次就渲染一次的时间，性能就大大提升了。

<br/>

>如需转载，请注明出处。谢谢！

[https://liutianzhu.me](https://liutianzhu.me)