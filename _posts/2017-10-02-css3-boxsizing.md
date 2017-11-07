---
layout: post
title: "通俗的记录一下CSS3的box-sizing属性"
author: "hopeverse"
---

对于CSS3中，box-sizing这一属性，可能对于刚刚学习CSS3的朋友来说，还真有时候

分不太清楚其中的具体细节，那么我将这个属性通俗的记录一下。希望能给大家一些帮助

<br/>

### 盒模型

  首先我们需要说一下盒模型这个东西，在CSS中盒模型被分为两种，第一种是w3c的标准模型，另一种是IE的传统模型，它们相同之处都是对元素计算尺寸的模型。我们看看这两种盒模型的区别：

W3C标准盒模型

![w3cbox](/images/posts/css3/w3cbox.png)

```

div实际显示大小

    div实际的高 = height+（padding+border+margin）*2

    div实际的宽 = width+（padding+border+margin）*2

div内容大小 

    根据对应设置的width，height决定，不包含border，padding，border

```


IE下的盒模型

![iebox](/images/posts/css3/iebox.png)

```
div的实际大小：

　　　　　div实际的高 = height+margin*2

　　　　　div实际的宽 = width+margin*2

     div内容占大小：

　　　　　div内容的高 = height-（border+padding）*2

　　　　　div内容的宽 = width-（border+padding）*2

```
<br/>

>所以盒子的具体宽高，是根据多方面来进行计算的。并且不仅仅是这样，而且我们在对div设置width宽度的时候，如果额外添加margin，padding等值，div的内容原本宽度是不会变的，变化的是div实际宽度也就是整个盒模型。W3C 盒子模型的范围不但包括 margin、border、padding、content，而且 content 部分不包含其他部分。而IE 盒子模型的范围也包括 margin、border、padding、content，和标准 W3C 盒子模型不同的是：IE 盒子模型的 content 部分包含了 border 和 padding



<br/>

### box-sizing:border-box;

  我们首先来看看W3school是如何介绍的。

![border-box](/images/posts/css3/boxs1.png)

我相信刚开始了解这个属性的朋友，都会觉得抽象，不那么好想象理解。那么我下面用简单的方法来给大家梳理。

其实```box-sizing:border-box```简单来说，也就是在你为元素比如div，设置了一个固定宽高，那么当你不设置box-sizing：border-box的时候，你所添加的额外属性，border和padding。那么都会将你的盒模型给向四周撑开，但是margin本身就是会撑开周围的元素，但是它在这里，不会增加盒模型的宽高，仅仅只是占用对应的像素而已。比如下面：

```
    <style>
        div{
            width: 300px;
            height: 300px;
            background: red;
            color: #fff;
            padding: 0 20px;
            border: 10px solid red;
        }
    </style>

    // 在原宽高300*300的基础上,并且不加box-sizing：border-box的情况下，再加上
    边框10px和左右内边距20px 的效果
```

这里我们可以看到，盒模型的宽度已经增加到360px了。


![noborderbox](/images/posts/css3/boxs2.png)

然而此时此刻内容的宽度，还是和我们最开始设置的时候，一模一样，为300px。看看

![noborderbox](/images/posts/css3/boxs2-1.png)

那么接下来我们看加上了```box-sizing:border-box;```之后的效果

![borderbox](/images/posts/css3/boxs3.png)

>通过上面的对比，我们可以得出一个结论。在块级元素中，**不加box-sizing:border-box的情况下** ，那么所有添加的border以及padding都将加到内容宽高之上，最后成为盒模型的真实宽高，但是最初设置的块级元素内容宽高不变。那么在 **加box-sizing:border-box的情况下** ，我们已经在块级元素上设定的宽高不变，不管加多少单位的border或者padding，改变永远都只是内容的宽高。也就是说，加上了这个属性，也就是一直往盒模型内部压缩内容区域。

所以加上box-sizing:border-box的好处就是，不用关心我们在块级元素上设置完的宽高，由于加上了border和padding而发生改变，导致盒模型变形。它仅仅只是会往内部压缩而已。

<br/>


### box-sizing:content-box;

现在我们来看看```box-sizing：content-box```在w3school是如何描述的

![contentbox](/images/posts/css3/conbox1.png)

>最后一句，在宽度和高度之外绘制元素的内边距和边距

根据这句话，我们看了前面那个例子，应该有一点思绪了，那么我们下面来测试一下。首先给div加上如下代码 ：

```
    <style>
        div{
            width: 300px;
            height: 300px;
            background: red;
            color: #fff;
            padding: 0 20px;
            border: 10px solid red;
        }
        // 在原宽高300*300的基础上,并且不加上box-sizing：content-box的情况下，再加上
    边框10px和左右内边距20px 的效果
    </style>
```

![noborderbox](/images/posts/css3/boxs2.png)

下面再加上```box-sizing：content-box```

![noborderbox](/images/posts/css3/boxs2.png)

从两者的区别来看，毫无差别。由此可以得出结论：

>在box-sizing属性中
>box-sizing:content-box  为W3C盒模型的默认值
>box-sizing：border-box  IE盒模型

<br/> 

### box-sizing:inherit;

![inherbox](/images/posts/css3/inherbox.png)

那么，第三个属性值就是继承父元素的box-sizing属性

<br/>

附上一张box-sizing属性的兼容性图

![boxsizingjr](/images/posts/css3/boxsizingjr.png)

<br/>

那么经过以上的了解，我们会出现几个疑问 ：

一 、W3C盒模型和IE盒模型，跟box-sizing属性有什么关系呢？

>因为w3c盒模型和ie盒模型，是两种不同的标准。那么现在都是默认使用W3C盒模型标准，然而box-sizing可以让我们设置是采用哪种盒模型的计算方式（换句话说就是，所添加的padding和border，是在元素之外增加尺寸，还是在内部元素压缩内容空间）。


二 、在计算盒子的宽高时，我们会发现按照W3C盒模型或者IE盒模型所给出的计算公式，得出来的结果并不相同，其中具体就是并没有加上边距margin的值？

>这是因为W3C标准盒模型和IE盒模型，根据两种标准盒模型计算出来的尺寸，实际上是所占用的像素尺寸，然而调试工具不会加上margin的值，因为这仅仅只能算边距的距离。所以说盒子的真实宽高尺寸，是不会加margin的值的，但是它盒子所占的实际像素尺寸，是会加上margin值，实际上确实也算盒子的宽度了。

<br/>

>如需转载，请注明出处。

[https://liutianzhu.me](https://liutianzhu.me)
