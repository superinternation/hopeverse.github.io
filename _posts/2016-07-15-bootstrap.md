---
layout: post
title: "Bootstrap基础知识点抽选"
author: "hopeverse"
---
 
最受欢迎的HTML、CSS、JS前端框架，用于开发响应式布局和移动设备优先的WEB项目。

<br/>

### 起步

首先大家需要配置好bootstrap环境，来[bootstrap](http://v3.bootcss.com/getting-started/)进行相关文件的下载。

只需要下载bootstrap文件就好了。

有几个地方需要注意，我们要用HTML5文档格式来写网页，有助于bootstrap的正常显示。

下载好文件之后，分别放置在css和js文件夹中，只需要找到bootstrap.min.css和bootstrap.min.js就能使bootstrap标签生效。

同时可以直接使用CDN来支持：

```
<!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">

<!-- 可选的 Bootstrap 主题文件（一般不用引入） -->
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap-theme.min.css" integrity="sha384-rHyoN1iRsVXV4nD0JutlnGaslCJuC7uwjduW9SVrLvRYooPp2bWYgmgJQIXwl/Sp" crossorigin="anonymous">

<!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
<script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>

```

在这之前还需要下载Jquery支持文件[jquery](http://jquery.com/download/)，来进行支持。

为了能够在手机上适应设备还需要加入一条语句：

```
<meta name="viewport" content="width=device-width, initial-scale=1">

```

为了让我们在布局时，解决没有图片的尴尬处境，我们可以使用holder.js来生成图框架[holderJs](http://www.bootcdn.cn/holder/)

```
<script src="holder.js"></script>

使用方法: <img src="holder.js/300x300" /> 
//此处默认是px作为单位，如需100%那么写成100p，此处宽高乘用字母x表示

```

所以一般我们一切准备就绪是这样：

```

<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Bootstrap</title>   
        <!-- Bootstrap -->
        <link href="css/bootstrap.min.css" rel="stylesheet">
        <!--你自己的样式文件 -->
        <link href="css/my.css" rel="stylesheet">        
        <!-- 以下两个插件用于在IE8以及以下版本浏览器支持HTML5元素和媒体查询，如果不需要用可以移除 -->
        <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
        <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
        <![endif]-->
        <!-- 虚拟图片占用框架 -->
        <script src="holder.js"></script>
    </head>
    <body>
        <h1>Hello, world!</h1>
        
        <!-- 调入jQuery -->
        <script src="http://libs.baidu.com/jquery/1.9.0/jquery.min.js"></script>
        <!-- 包括所有bootstrap的js插件或者可以根据需要使用的js插件调用　-->
        <script src="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script> 
    </body>
</html>

```

<br/>

### 栅格布局

居中显示，两边留白的固定div宽度使用 ```.container```，100%宽度```.container-fluid```

#### 栅格参数

![栅格参数](/images/posts/bootstrap/shange.PNG)

```
行 row ，一行12列  

列 col-xx-num表示

嵌套关系是：

<div class="container">
        <div class="row">
            <div class="col-md-6">hello</div>
            <div class="col-md-6">world</div>
        </div>
</div>  

上面的意思是一行两列。  在bootstrap中一行分为12格，一行中的列，必须相加或者乘积为12
```

#### 列偏移

```
col-md-offset-3      // 此处为在桌面屏幕下左偏移3个列宽 md以及列宽可根据情况修改

```

#### 嵌套列

```

<div class="container">
        <div class="row">
            <div class="col-md-6">
                <div class="row">
                    <div class="col-md-6">hello</div>
                    <div class="col-md-6">world!</div>
                </div>
            </div>
            <div class="col-md-6">world</div>
        </div>
</div>  

```

#### 列排序

通过使用``` .col-md-push-*``` 和``` .col-md-pull-* ```类就可以很容易的改变列（column）的顺序。

```
<div class="row">
  <div class="col-md-9 col-md-push-3">.col-md-9 .col-md-push-3</div>
  <div class="col-md-3 col-md-pull-9">.col-md-3 .col-md-pull-9</div>
</div>


直接在：

<div class="col-md-6 pull-right"> 
 在列中加入pull-right或者pull-left，可以达到float效果，更加简便。
</div>

```

<br/>

### 排版

#### 段落突出 

```
<p class="lead">...</p>

```

#### 内联文本着重某文字

```
<mark>highlight</mark>

```

#### 删除文本

```
<del>hello!</del>

```

#### 小号字体

```
<small>hello!</small>
```

#### 文字对其方式

```
<p class="text-left">Left aligned text.</p>            左对齐
<p class="text-center">Center aligned text.</p>        居中对齐
<p class="text-right">Right aligned text.</p>          右对齐
<p class="text-justify">Justified text.</p>            左对齐                 
<p class="text-nowrap">No wrap text.</p>               左对齐 

```

#### 改变文字大小写

```
<p class="text-lowercase">Lowercased text.</p>        全部小写
<p class="text-uppercase">Uppercased text.</p>        全部大写
<p class="text-capitalize">Capitalized text.</p>      单词首字母大写

```


#### 无样式列表

```
<ul class="list-unstyled">
</ul>

等价于list-style:none;

```

#### 内联列表

```
<ul class="list-inlie">
    <li></li>
    <li></li>
    <li></li>
</ul>

等价于display:inline-block

```

<br/>

### 表格
#### 表格样式

```
table           表格基础样式

.table-striped   表格条纹

.table-bordered  加上边框

.table-hover     鼠标悬浮效果

.table-condensed 行高微小收缩

```

#### 状态类

![表格颜色](/images/posts/bootstrap/bgcolor.PNG)

```
.info

.success

.active

.warning        

.danger    

```


#### 响应式表格

当表格内容足够多，而表格跟着浏览器缩小内容装不下时，表格会出现横向滚动条

```
<div class="table-responsive">
    <table class="table">
        ...
    </table>
</div>

```

<br/>

### 表单

#### 基本表单

单独的表单控件会被自动赋予一些全局样式。所有设置了``` .form-control ```类的 ```<input>```、```<textarea>``` 和 ```<select>``` 元素都将被默认设置宽度属性为``` width: 100%;```。 将``` label``` 元素和前面提到的控件包裹在``` .form-group ```中可以获得最好的排列

![基本表单](/images/posts/bootstrap/jbbd.PNG)


```
<form>
  <div class="form-group">
    <label for="exampleInputEmail1">Email address</label>
    <input type="email" class="form-control" id="exampleInputEmail1" placeholder="Email">
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">Password</label>
    <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
  </div>
  <div class="form-group">
    <label for="exampleInputFile">File input</label>
    <input type="file" id="exampleInputFile">
    <p class="help-block">Example block-level help text here.</p>
  </div>
  <div class="checkbox">
    <label>
      <input type="checkbox"> Check me out
    </label>
  </div>
  <button type="submit" class="btn btn-default">Submit</button>
</form>

```

注意：要将lable和输入框input嵌套在```<div class="form-group"></div>``` 中    

#### 内联表单

为``` <form> ```元素添加``` .form-inline``` 类可使其内容左对齐并且表现为 ```inline-block ```级别的控件。只适用于视口（viewport）至少在 768px 宽度时（视口宽度再小的话就会使表单折叠）。

![内联表单](/images/posts/bootstrap/nlbd.PNG)


```
<form class="form-inline">
  <div class="form-group">
    <label for="exampleInputName2">Name</label>
    <input type="text" class="form-control" id="exampleInputName2" placeholder="Jane Doe">
  </div>
  <div class="form-group">
    <label for="exampleInputEmail2">Email</label>
    <input type="email" class="form-control" id="exampleInputEmail2" placeholder="jane.doe@example.com">
  </div>
  <button type="submit" class="btn btn-default">Send invitation</button>
</form>

```

隐藏lable ``` class="sr-only"``` ：

![隐藏lable](/images/posts/bootstrap/yclb.PNG)


```
<form class="form-inline">
  <div class="form-group">
    <label class="sr-only" for="exampleInputEmail3">Email address</label>
    <input type="email" class="form-control" id="exampleInputEmail3" placeholder="Email">
  </div>
  <div class="form-group">
    <label class="sr-only" for="exampleInputPassword3">Password</label>
    <input type="password" class="form-control" id="exampleInputPassword3" placeholder="Password">
  </div>
  <div class="checkbox">
    <label>
      <input type="checkbox"> Remember me
    </label>
  </div>
  <button type="submit" class="btn btn-default">Sign in</button>
</form>

```

#### 输入框

![输入框](/images/posts/bootstrap/srk.PNG)

```
<input type="text" class="form-control" placeholder="Text input">

//  placeholder="Text input"   输入框中默认显示内容

```


#### 文本域

![文本域](/images/posts/bootstrap/wby.PNG)

```
<textarea class="form-control" rows="3"></textarea>

// row 控制着文本域的高度

```



<br/>

### 按钮

![按钮](/images/posts/bootstrap/btn.PNG)

```
.btn

.btn-default           

.btn-primary

.btn-success

.btn-info

.btn-warning

.btn-danger

.btn-link

```


#### 按钮大小

```
.btn-lg  大按钮

.btn-default  默认大小

.btn-sm   小按钮

.btn-xs   超小尺寸

```

#### 禁用状态

```
<button type="button" class="btn" disabled>
    
</button>

属性中加上disabled
```

<br/>

### 图片

![图片](/images/posts/bootstrap/pic.PNG)

```
不需要基础class img 可直接写下面class

img-rounded     圆角

img-circle      圆

img-thumbnail   图片之外有外壳边框  

img-responsive  图片自适应

```

IE8不支持，最好是IE9以上

<br/>

### 辅助类

#### 文本颜色

![字体颜色](/images/posts/bootstrap/fontcolor.PNG)

```
<p class="text-muted">...</p>
<p class="text-primary">...</p>
<p class="text-success">...</p>
<p class="text-info">...</p>
<p class="text-warning">...</p>
<p class="text-danger">...</p>

```

#### 背景颜色

![背景颜色](/images/posts/bootstrap/bgcolors.PNG)

```

<p class="bg-primary">...</p>
<p class="bg-success">...</p>
<p class="bg-info">...</p>
<p class="bg-warning">...</p>
<p class="bg-danger">...</p>

```


#### 关闭按钮

![关闭按钮](/images/posts/bootstrap/gban.PNG)

```

<button type="button" class="close" aria-label="Close"><span aria-hidden="true">&times;</span></button>

```

#### 下三角符号

![下三角按钮](/images/posts/bootstrap/xsjan.PNG)

```
<span class="caret"></span>

```


#### 浮动

```
.pull-left    左浮动

.pull-right   右浮动

```


#### 清除浮动

```
<div class="clearfix">
    ...
</div>

```


#### 居中显示

块设置了宽高之后，加上类center-block就能居中。行内标签同理

```
.center-block

```


#### 显示隐藏

任何标签加上以下类样式均显示或者隐藏

```
.hide   隐藏

.show   显示

```

<br/>

## 组件

### 下拉菜单

将下拉菜单触发器和下拉菜单都包裹在 .dropdown 里，或者另一个声明了 position: relative; 的元素。然后加入组成菜单的 HTML 代码。

![下拉菜单](/images/posts/bootstrap/xlcd.PNG)

```
<div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">
    Dropdown
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>

```

#### 标题

点击下拉菜单，在下拉菜单中标题显示灰色，在任何下拉菜单中均可通过添加标题来标明一组动作。

![下拉菜单](/images/posts/bootstrap/bt.PNG)

```
<ul class="dropdown-menu" aria-labelledby="dropdownMenu3">
  ...
  <li class="dropdown-header">Dropdown header</li>
  ...
</ul>

```


#### 对齐

不建议使用 .pull-right

从 v3.1.0 版本开始，我们不再建议对下拉菜单使用 .pull-right 类。如需将菜单右对齐，请使用``` .dropdown-menu-right ```类。导航条中如需添加右对齐的导航（nav）组件，请使用 .pull-right 的 mixin 版本，可以自动对齐菜单。如需左对齐，请使用 ```.dropdown-menu-left``` 类。


#### 分割线

为下拉菜单添加一条分割线，用于将多个链接分组。

![分割线](/images/posts/bootstrap/fgx.PNG)

```
<ul class="dropdown-menu" aria-labelledby="dropdownMenuDivider">
  ...
  <li role="separator" class="divider"></li>
  ...
</ul>

```


#### 禁用菜单

为下拉菜单中的 <li> 元素添加 .disabled 类，从而禁用相应的菜单项。

![禁用菜单](/images/posts/bootstrap/jycd.PNG)

```
<ul class="dropdown-menu" aria-labelledby="dropdownMenu4">
  <li><a href="#">Regular link</a></li>
  <li class="disabled"><a href="#">Disabled link</a></li>
  <li><a href="#">Another link</a></li>
</ul>

```

<br/>

### 按钮组







>如需转载，请注明出处。谢谢！

[https://liutianzhu.me](https://liutianzhu.me)
