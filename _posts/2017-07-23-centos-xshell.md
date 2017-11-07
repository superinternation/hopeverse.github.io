---
layout: post
title: "关于Centos网络配置以及使用xshell远程工具登录的方法"
author: "hopeverse"
---
 
关于配置centos的网络以及使用xshell来连接centos，期间真是踩了不少的坑。下面就讲

一讲这里面的步骤以及出现的一些问题吧。

<br/>

### centos网络配置

在这之前首先我们要确保虚拟机上centos的安装大家是没有任何问题的。如果说大家还不知道如何在虚拟机上正确安装centos，可以去谷歌一下。然后我们现在主要开始记录的是网络配置的问题。

在这之前，首先声明一下，我本地是自动获得ip地址，以及自动获取服务器DNS的选择。


第一，首先进入centos虚拟机之后，我们使用setup来配置网络。登录root之后键入：

```
setup   // 运行工具

```

然后根据下图的选项进行选择：

![1](/images/posts/centos/1.PNG)

![2](/images/posts/centos/2.PNG)

![3](/images/posts/centos/3.PNG)

![4](/images/posts/centos/4.PNG)

那么看到第四张图，我们这个上面需要填的是什么呢？

就是你电脑物理机网络的详细配置

第二，请打开```cmd```

键入```ipconfig/all``` ，找到现在你物理机上网的网卡到底是那个，然后填入相关的IP，网关，以及DNS

比如现在我的上网卡是这个，进入电脑网络和共享中心，也就是右下角右键你的上网图标进入。然后点击左边的更改适配器设置，然后看看你现在是什么网卡在上网，比如我的是无线网卡

![5](/images/posts/centos/5.PNG)

看到了吧，这个就是等会你要打开cmd然后输入命令```ipconfig/all```里面找的东西

然后我现在找一下我，看到下面的标记了吧，这就是之前上面我对应的网卡。

![6](/images/posts/centos/6.PNG)

然后把这些相关的内容都填进我们之前centos里面的网络配置项去。替换成你自己的。

ps：这里要注意，咱们ip是192.168.1.101，那么填到setup那个网络配置里面去的ip，前三位可以相同，第四位不能相同所以我改成了108结尾。只要在一个ip地址段里面就行了。最后一个随便填一个合理的都可以。

替换完成之后TAB选择ok，返回上一级，继续TAB然后Save，然后Save$Quit，最后看到Run Tool 和Quit 选择Quit退出。

ps:如果说，你的网络并没有开启DHCP动态地址分配的话，那么上面setup中，最后填的所有信息，就是和你现在本地网络相同的设置，除了ip第四位不需要相同，其他对的都要对应相同。

第三，接下来输入命令：

```
service network restart     

```

如果说你看到了这个，那么你就成功了。

![7](/images/posts/centos/7.PNG)


疑问一，但是假如只显示了前面两个怎么办？就是下面这个样子.那么请键入命令

![8](/images/posts/centos/8.jpg)

```
vi /etc/sysconfig/network-scripts/ifcfg-eth0        //  后面是数字0

```


接下来要按回车键进入设置，然后你会看见这个东西。

![9](/images/posts/centos/9.PNG)

请把那个```ONBOOT=no```改成```yes```，因为我改完了所以是对的。你们出现了问题那么请改成yes，还有你必须按```i```键才能更改里面的内容，改完之后按```ESC```，然后退出，退出的方法是，按住```ESC+Shift+ ：```后面还一个冒号，要注意了。接下来你会在最后面看到一个冒号，然后在冒号后面输入```x```然后回车，就可以继续回到命令模式了。

疑问二，但是加入只显示了前三个还有最后一个什么什么ip adress一直有延迟问题怎么办？下面是报错的相关语句：

```
Bringing up interface eth0: Determining if ip address is already in use for device eth0    //  是的，前三条已经没问题了，最后这里出了问题。

```

那么请进入刚刚的命令

```
vi /etc/sysconfig/network-scripts/ifcfg-eth0        //  后面是数字0

```

然后在最后面添加一句命令，
  
``` 
ARPCHECK=no
```

然后保存退出就可以了。保存退出的方法依旧是按ESC，然后ESC+Shift+：然后输入x回车。

如果说你四条基础配置都成功了。

![10](/images/posts/centos/10.PNG)


第四，接下来就是输入命令

```
ifconfig

```

如果看到下面这两段英文，那么就是都成功了。

![11](/images/posts/centos/11.PNG)

其中红色笔圈出来的，要记住了，等会要使用xshell远程工具来设置。

### xshell远程登陆工具配置

打开xshell，大家可以去官网下载一个，xshell4或者5都行

打开软件，然后点击左上角文件，新建，弹出下图

![12](/images/posts/centos/12.PNG)

其中名称随便填，协议必须SSH，主机也就是之前我用红笔圈出来的ip地址，也是setup网络配置里面咱们设置的当前ip地址，端口22不变。

然后其余都不用改，点击左边用户身份验证

![13](/images/posts/centos/13.PNG)

然后大家添一个用户名就行了，密码不用填，点击确定，如果连接成功了，还会让咱们输入密码，输入完成对了，点击接受并保存，那么连接就成功了。

疑问三，如果说咱们centos配置完成，没问题了。但是总是死活不能和xshell工具连接登录，该怎么办啊？

那请你到虚拟机的主界面左上角找到编辑点击进去，找到虚拟机网络编辑器，左下角还原默认设置，然后确定，那么再次连接。那么就可以成功连接进入了。



>如需转载，请注明出处。谢谢！

[https://liutianzhu.me](https://liutianzhu.me)
