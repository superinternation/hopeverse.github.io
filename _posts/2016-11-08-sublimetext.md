---
layout: post
title: "前端开发神器之Sublime Text 3及其常用插件"
author: "hopeverse"
---
 

前端开发神器SublimeText3的安装方法以及常用插件

<br/>

### Sublime Text 3

下载地址：[http://pan.baidu.com/s/1dFgnZax](http://pan.baidu.com/s/1dFgnZax)

<br/>

### package control

>需要在sublime上使用插件，那么必须安装插件库package control。那么安装完sublime之后，打开软件按ctrl+~打开控制台，然后粘贴以下支持sublime text 3的代码，安装完成之后就可以开始插件的安装啦。

```
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

```
<br/>

### PyV8 

>sublime text 3安装后面需要的emmet的时候，这个pyv8需要下载一小段时间，所以我们可以提前下载好，然后就可以进sublime 浏览插件目录Installed Packages 创建文件夹  PyV8然后解压文件，然后文件包含在上面的sublime软件包里面了，这里就不提供下载地址了。

<br/>

### chinese

>这个插件可以让sublime里面的选项全部汉化，这样我们就可以看得懂各个选项里面的功能啦。但是有一个副作用就是，可能会导致你不能更换sublime主题。如果你使用了，导致不能更换编辑器主题，那么你可以删除这个插件，就可以恢复正常啦。

<br/>

###  HTML-CSS-JS prettify

>html-css-js-json格式化插件，能够让自己编辑的代码规范整洁，但是使用它的前提是需要安装node.js文件。然后右键编辑器桌面进入 set  pluging  option   设置好node.exe的路径保存就好了，node.js文件也同样包含在sublime软件压缩包里面了。

<br/>

### LiveReload

>此插件就是保证前端自动化的功能。能够在我们保存每一次代码之后，实时更新在浏览器里面显示，但是我仅仅只测试谷歌浏览器，其他浏览器大家可以自己尝试一下，那么在sublime中下载完这个插件之后，我们还需要去谷歌浏览器，安装拓展工具LiveReload，安装完成之后，进入浏览器扩展程序里面，勾选允许访问文件网址。就绪之后，每一次打开浏览器需要实时更新，还需要点击右上角的扩展程序变成小实心点。还需要去以下路径设置如下代码：

```
 Preference>Package Settings>LiveReload>Settings User
 //这是设置路径
 //下面是设置内容


{
    "enabled_plugins": [
        "SimpleReloadPlugin",
        "SimpleRefresh"
    ]
}

```

<br/>

### TAG

>自动缩进插件

<br/>

### Markdown editting以及Markdown preview 

>这两个插件是支持markdown的，并且可以本地实时预览Markdown文件，下载完毕之后，进入 key Bindings  粘贴如下代码：

```
[
    {"keys": ["alt+m"], "command": "markdown_preview", "args": { "target": "browser"}}
]

//使用alt+m就可以实时预览啦。

```

<br/>

### a file icon

>只是可以改变侧边目录图表文件的插件，比较好看，推荐！

<br/>

###  DeleteBlankLines

>此插件可以清除代码中多余的回车空格。按键为ctrl+alt+退格backpace   另一种是还加个shift

<br/>

### emmet

>经典中的经典，代码快速编写神器，当自动缩进出现bug然后进package settings里面Emmet的setting-user里面加入：

---

{
"autodetect_xhtml":false,
}

//自动缩进没bug就不用管啦。

---


<br/>

### Sublime-Better-Completion

>这个插件是代码快速匹配插件，简短的缩写就能够自动匹配到相关代码，首先设置点击preferences进入，再packge-setting，找到Sublime-Better-Completion，然后点击user设置来复制如下代码：

下载地址：[http://pan.baidu.com/s/1dF1mDLf](http://pan.baidu.com/s/1dF1mDLf)

---
{
// --------------------
// sublime-better-completions-Package (sbc package)
// --------------------
// API files is contains the *keyword* such as `html`, `jquery`, `myglossary` with lowercase as filename `sbc-api-${filename}.sublime-settings` place in `/packages/User/` (your own) or `/packages/${this-package}/sublime-completions/` (package build-in).
// After you enable, disable or added new your own completions, you might need restart your Sublime Text Editor.
//
// Your own setting file `sbc-setting.sublime-settings` need to place in `/packages/User/` and contains all your api setting property that you want to enable.
//
// --------------------
// APIs Setup
// --------------------
// `true` means enable it.
// `false` means disable it.
"completion_active_list": {
// build-in completions
"css-properties": false,
"gruntjs-plugins": false,
"html": false,
"lodash": false,
"javascript": true,
"jquery": true,
"jquery-sq": false, // Single Quote
"php": true,
"phpci": false,
"sql": false,
"twitter-bootstrap": true,
"twitter-bootstrap-less-variables": false,
"twitter-bootstrap3": true,
"twitter-bootstrap3-sass-variables": false,
"underscorejs": false,
"react": false,

// Your own completions?
// ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User/sbc-api-my-angularjs.sublime-settings
"my-angularjs": false,

// ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User/sbc-api-my-glossary.sublime-settings
"my-glossary": false,

// ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User/sbc-api-my-html.sublime-settings
"my-html": false,

// ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User/sbc-api-my-javascript.sublime-settings
"my-javascript": false
  }
}


要开关什么，改true，false，就好。

---

<br/>

### Color​Picker

>直接在sublime中调用颜色选择板，快捷键是ctrl+shift+c

<br/>

### autofilename

>快捷提示调用文件路径

<br/>

### SyncedSidebarBg

>插件自动同步编辑窗口底色

<br/>

### 常用快捷键

```
ctrl+【】调整字体大小

Ctrl+ ? 注释单行。

Ctrl+Shift+ ? 注释多行。

ctrl+shift+【】  折叠打开代码

```

<br/>

### 右键打开方式

>将sublime编辑器设置在右键快捷方式当中，可以方便的用编辑器打开文件。那么首先创建一个文本文档，名字修改为sublime_addright.inf 然后进入文本当中粘贴以下代码，然后将此文件剪切至sublime安装文件夹中（也就是跟sublime.exe同一个目录下）：

```

[Version]
Signature="$Windows NT$"

[DefaultInstall]
AddReg=SublimeText3

[SublimeText3]
hkcr,"*\\shell\\SublimeText3",,,"用 SublimeText3 打开"
hkcr,"*\\shell\\SublimeText3\\command",,,"""%1%\sublime_text.exe"" ""%%1"" %%*"
hkcr,"Directory\shell\SublimeText3",,,"用 SublimeText3 打开"
hkcr,"*\\shell\\SublimeText3","Icon",0x20000,"%1%\sublime_text.exe, 0"
hkcr,"Directory\shell\SublimeText3\command",,,"""%1%\sublime_text.exe"" ""%%1"""

```


<br/>

### 关闭软件自动更新

>sublime有一点不太舒适就在于总是弹出需要更新注册。那么关闭这个提示的方法，并且注册的话，就需要进入preference里面setting选项中在字体大小代码后面回车粘贴第一段代码，注册的话那么就点击Help点击Enter License，粘贴第二段代码：


```
"update_check":false,
// 这是第一段



—– BEGIN LICENSE —–
Michael Barnes
Single User License
EA7E-821385
8A353C41 872A0D5C DF9B2950 AFF6F667
C458EA6D 8EA3C286 98D1D650 131A97AB
AA919AEC EF20E143 B361B1E7 4C8B7F04
B085E65E 2F5F5360 8489D422 FB8FC1AA
93F6323C FD7F7544 3F39C318 D95E6480
FCCC7561 8A4A1741 68FA4223 ADCEDE07
200C25BE DBBC4855 C4CFB774 C5EC138C
0FEC1CEF D9DCECEC D3A5DAD1 01316C36
—— END LICENSE ——

—– BEGIN LICENSE —–
Alexey Plutalov
Single User License
EA7E-860776
3DC19CC1 134CDF23 504DC871 2DE5CE55
585DC8A6 253BB0D9 637C87A2 D8D0BA85
AAE574AD BA7D6DA9 2B9773F2 324C5DEF
17830A4E FBCF9D1D 182406E9 F883EA87
E585BBA1 2538C270 E2E857C2 194283CA
7234FF9E D0392F93 1D16E021 F1914917
63909E12 203C0169 3F08FFC8 86D06EA8
73DDAEF0 AC559F30 A6A67947 B60104C6
—— END LICENSE ——

—– BEGIN LICENSE —–
Nicolas Hennion 
Single User License 
EA7E-866075 
8A01AA83 1D668D24 4484AEBC 3B04512C 
827B0DE5 69E9B07A A39ACCC0 F95F5410 
729D5639 4C37CECB B2522FB3 8D37FDC1 
72899363 BBA441AC A5F47F08 6CD3B3FE 
CEFB3783 B2E1BA96 71AAF7B4 AFB61B1D 
0CC513E7 52FF2333 9F726D2C CDE53B4A 
810C0D4F E1F419A3 CDA0832B 8440565A 
35BF00F6 4CA9F869 ED10E245 469C233E 
—— END LICENSE ——

// 这是第二大段，这里分三段，都可以注册成功，随便选一小段就行了。

```

<br/>

### 恢复出厂设置

>如果你想恢复出厂设置那么，进入文件夹  C:\Users\计算机用户名\AppData\Roaming   删除sublime文件夹就可以了，卸载都不用就可以重新设置。

<br/>

>如需转载，请注明出处。谢谢！

[https://liutianzhu.me](https://liutianzhu.me)
