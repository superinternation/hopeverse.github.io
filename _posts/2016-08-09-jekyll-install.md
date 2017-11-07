---
layout: post
title: "在windows操作系统下安装Jekyll的最新指南"
author: "hopeverse"
---

<span style="first-letter:60px;text-indent: 18px;">经</span>过重重困难，断断续续的坚持了两天，终于在网络上繁多的文章中，得出最为正确的Jekyll安装方法。


那么以下，我便将具体详细步骤，在下方进行详细的描述给大家，欢迎各位基友停留在此，至于Jekyll是什么我也不具体来说了，既然来了那么大家都是有过一番了解的，那么现在开始，走着！

 首先我们需要来到这个网站 [Rubyinstall](http://rubyinstaller.org/downloads)来下载这两文件，如下方：

![软件一](/images/posts/jekyll/1.png) 

![软件二](/images/posts/jekyll/2.png)

这两张图分别是两个软件所有的有效版本，那么你只要在其中分别选择下载一个就可以了，然后32位操作系统就下载32位的，64位就下载64位的 ，大家应该还是能够分辨清楚。

 下载软件之后，安装第一个软件rubyinstall，我安装在了C盘，安装过程中要把下面3个勾

![打勾](/images/posts/jekyll/3.png) 

给打上，接下来安装完成之后，运行打开cmd，输入  

// 注意，这里32位命名可能自动为ruby22，而64位命名你需要手动设置为ruby23，更好！

        ruby -v  
 
如果显示这张图，那么你就成功安装了rubyinstall.

![ruby](/images/posts/jekyll/4.png)  

检查rubyGems是否安装成功，不要心急，你如果按照了rubyinstall那么这个是默认一起安装的，所以不用百度去查怎么安装了，你只需要去cmd 输入：


        gem -v

如果显示

![gem](/images/posts/jekyll/5.png)  

 下面是版本号，那么你就成功了。

 然后我们安装Devkit这个软件，就是刚刚你下的第二个软件，这个东西很强很关键，认真安装喔。那么，开始双击安装这个文件，设置路径，一定要记得放在之前ruby的文件夹下喔老哥，下面是图  
  
![devkit](/images/posts/jekyll/6.png)  

  然后你的cmd要进入devkit的主目录 ，看清楚最后一个路径 要记得加cd空格 

![addmulu](/images/posts/jekyll/7.png) 


  这个就是进入这个主目录的代码，进入之后在cmd输入

        ruby dk.rb init

![init](/images/posts/jekyll/8.png)


   如果成功则如图中结果一样，然后这就是提示你需要修改config.yml文件然后去文件夹Devkit文件夹中找到此文件夹，将最后两段路径设置为ruby文件夹的名字，然后保存退出 


![config](/images/posts/jekyll/9.png)  

  

 接下来在cmd中输入这串代码：  <br/>

        
        ruby dk.rb install

![rubyinstall](/images/posts/jekyll/10.PNG)

  cmd出现此反馈，那么代表命令有效

 接下来需要更改默认的源，官方的源已经无法访问，那么请使用推荐的源，首先键入命令

       <br/>
        
         gem sources -l

  查看当前已经添加的源(默认应该是有官方源)

  然后键入命令删除官方的源

         gem sources -r https://rubygems.org/

  接下来在cmd中键入如下命令，来添加ruby chaina的源

         gem sources -a http://gems.ruby-china.org/

  修改完之后查看，是否已经修改

         gem sources -l


 这时候继续在cmd中输入安装Jekyll的代码：
<br/>

        gem install bundler       

  
  等待其加载完成，如果命令生效那么就会如下图所示：

![jjerror1](/images/posts/jekyll/16.PNG)

  然后键入如下代码：

        gem install jekyll

  
  这个时候你想把默认blog下载到什么文件夹呢？  我是在E:\Hope目录下，那么我们就必须用cmd切换到相应的文件夹中  cd 路径 或者直接E:  回车

这个时候cmd已经切换到这个目录了，那么我们接下来输入下面的命令：

          jekyll new myblog

  如果出现下图则blog创建成功:

![blogpic](/images/posts/jekyll/17.PNG)

  
  然后！老铁！去cmd把路径切换到myblog

        cd E:\Github\myblog

  在dmc中键入下面的命令：

        jekyll serve

  那么这个你就可以点击下面的链接看看你简单blog的样子咯~

 [myblog](http://localhost:4000/)

  
>如需转载，请注明出处，尊重劳动成果，欢迎大家停留在此，共同学习!谢谢！

[https://liutianzhu.me](https://liutianzhu.me)


