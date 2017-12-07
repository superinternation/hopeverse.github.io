---
layout: post
title: "Git版本控制工具的日常命令及操作"
author: "hopeverse"
---
 

世界上最先进的分布式版本控制系统 - Git  

<br/>

### Git初次运行配置

打开git bash然后分别键入以下两行命令 ：

```
git config --global user.name "你设置的用户名"

git config --global user.email  你的邮箱地址,不需要加双引号.

```

<br/>

### Git设置公匙

1.首先我们需要安装好Git，一直按照默认设置安装即可。

2.待安装完成之后，打开Git Bash，键入命令ssh-keygen -t rsa -C "Github用户名"之后会出现下图所示，提示你输入key名字

![jrml](/images/posts/git/jrml.PNG)  

3.然后输入名字为id_rsa，然后一路回车就可以了。出现下图则表示成功

![szcg](/images/posts/git/szcg.PNG)

4.之后会在C:\Users\计算机账户名，下面产生两个文件，分别是id_rsa和id_rsa.pub，那么把这两个文件复制到C:\Users\计算机账户名\ssh文件夹下

5.然后用记事本等等，打开id_rsa.pub文件，复制内容，再在github.com的网站上到ssh密钥管理页面，添加新公钥，随便取个名字，内容粘贴刚刚复制的内容即可

<br/>

### 初始化目录

```
git init

```

>经过此操作的目录，就可以使目录变成可以使用git来操作管理的目录，并且此目录下还会隐藏一个.git的文件夹

<br/>

### 添加文件到仓库

```
git add xxx

git add .     // 将所有修改跟踪的文件添加到暂存区


```

>xxx为需要添加的文件名，此命令可以重复操作，即重复添加文件到仓库，此时文件被添加到了暂存区

<br/>

### 提交文件到仓库

```
git commit -m "提交备注"  

```

> git commit 告诉git把文件提交到仓库   -m是本次提交说明  双引号内输入本次提交备注

<br/>

### 查看仓库当前状态

```
git status

```

>每次修改都能够用此命令实时查看当前仓库状态

<br/>


### 查看文件具体修改内容

```
git  diff 

```

>查看文件具体修改内容    git diff  xxx   查看具体文件修改详情

<br/>


### 查看提交日志

```
git  log

```

>显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数

<br/>


### 查看历史简要版本信息

```
git reflog 

```

> 当你回退一个版本之后，再想回到之前某个版本，但是又找不到了。那么就用这个命令可以看见每一次修改的信息，找到版本号。再用git reset --hard HEAD xxx，就可以回到某个版本去

<br/>


### 版本回退

```
git reset --hard  commit_id

```

> commit_id表示历史版本号   git  reset --hard commit_id 使用git reflog来查找编号替换commit_id，就可以回退到历史版本，但是必须是本地commit过的每一次版本，就算push到github也是可以回退到历史版本的

<br/>



### 撤销工作区文件修改

```
git checkout -- xxx文件名 

```

>把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
，就是让这个文件回到最近一次git commit或git add时的状态。  无论工作区是修改还是删除，都可以“一键还原”

<br/>



### 暂存区的修改撤销回工作区

```
git reset HEAD xxx文件名

```

>此命令可以把已经添加到暂存区的修改撤销掉（unstage），重新放回工作区，有两种情况：

1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

3：如果commit了之后对此版本不满意，那么请找到版本回退章节


<br/>


### 工作区和版本库最新版本的对比

```
git diff HEAD -- xxx文件名

```

>此命令可以查看工作区和版本库里面最新版本的区别

<br/>


### 删除工作区以及版本库文件

```
rm xxx文件名    // 用来删除工作区的文件

git rm  xx文件名  //删除工作区的文件并且推送到暂存区

```

>rm xx仅仅只是删除了工作区的文件，但是并没有推送到暂存区，如果想恢复可以使用git checkout -- xxx文件名来恢复。
如果使用的是git rm 那么工作区的文件不仅删除了，而且还添加到了暂存区，但是并没有commit。
如果是你删错了，那么版本库里面还有的呢，那么也可以使用git checkout -- xxx文件名来恢复。也就是恢复工作区的修改。
如果是你用git rm删除了，但是想恢复工作区，那么需要使用git reset HEAD xxx ，然后git checkout -- xxx

<br/>

### 本地仓库添加到远程仓库（先有本地，再有远程）

首先，要先添加到远程库，那么先去github创建库，并且这个库先不能勾选README.md，因为这样远程仓库和本地仓库文件有差异，然后用下面这个命令进行关联：

```
 git remote add origin git@github.com:hopeverse/ceshi.git      

```

>hopeverse改成自己的github用户名  ceshi改成github库名

再进行全部内容的推送，创建库之后的第一次推送需要加-u，以后就可以简化如第二段：

```
git push -u origin master    //首次推送加 -u

git push origin master       //以后推送就可以这样

```

我们将本地库上传添加到远程库，所以在这一切步骤之前，我们要确定我们的库文件夹，已经init，add，commit过了，这样添加到远程库，才不会出错。

<br/>

### 推送（删除）本地分支到远程分支

在本地分支上，如果未合并到master分支时，我们单独希望将本地分支同步或者同步并创建到远程仓库上，那么就使用如下命令：

```
git push origin 本地分支名:远程分支名    // 远程分支没有就会自动创建

```

那么如果希望删除远程分支，那么就使用命令：

```
git push origin :远程分支名

```

<br/>


### 查看远程分支

```
git branch -a  //查看远程分支

git branch     //查看本地分支

git branch -vv  //查看本地分支和远程分支跟踪信息

```

<br/>

### 从远程仓库克隆到本地（先有远程，再克隆到本地）

我们从最初开发项目，那么最好先创建远程库，然后从远程库克隆到本地。

那么首先，我们需要先登录github，来创建一个远程库，新的仓库名为xxx，然后勾选READ

ME.md，一切准备就绪之后使用克隆命令克隆到本地仓库：

```
git clone git@github.com:hopeverse/ceshi.git 

```

>hopeverse改成自己的github用户名  ceshi改成github库名

要想克隆到本地电脑指定目录，那么需要建一个空文件夹，最好和远程库一个名字，然后使用如下命令：

```
git clone git@github.com:账户名/远程库名.git "f:/你新建的本地文件夹名"

```

<br/>


### 查看远程仓库

当你从远程仓库克隆库到本地，需要查看远程仓库信息时，可以使用如下命令：

```
git remote         // 查看远程仓库信息

git remote -v      // 查看远程仓库更加详细信息

```

git remote -v 出现的内容：

```
$ git remote -v
origin  git@github.com:hopeverse/xx.git (fetch)
origin  git@github.com:hopeverse/xx.git (push)

```

显示的是可以抓取和推送的origin地址，如果说没有权限就看不到push的地址了

<br/>


### 创建和合并分支

我们要创建一个分支，那么就是新建一个分支xx，然后HEAD指向这个分支xx，那么每一次

提交都是分支xx在进行版本的更新，那么master在没有指针HEAD指向的时候，是不会动的

，合并分支就是把master指向xxx的当前提交，就可以完成合并了。合并完成之后，删

除分支。其实就是把xxx分支给删除，最后只剩下master分支，那么合并分支完成。以下则

是实际操作：

创建xxx分支，然后切换到xxx分支：

```
git checkout -b xxx     //-b 表示创建并切换 

```

其实就是等于以下两条命令组成过来的：

```
git branch xxx         //创建分支xxx

git checkout xxx       //切换分支xxx

```

创建完成之后，输入以下命令查看当前分支：

```
git branch             // 出现一个分支列表，那么前面有*则是当前分支

```

接下来就可以在当前分支上面进行正常的提交了。然后我们切换到master分支上：

```
git checkout master    // 既是切换分支，也是控制HEAD指针指向哪个一分支

```

新添加的内容，切换到任何分支都会存在，但是具体在具体哪个分支commit的，那么这个新添加的内容就在哪个分支。切换分支后会发现原本xxx分支上面的修改的内容不见了。但是master分支的提交点还是没变，还在第一次建立分支的地方没动。

然后我们来合并分支：

```
git merge xxx分支          // git merge 用于合并某分支到当前分支

```

合并完成之后控制台会出现一段话 Fast-forward 这个告诉我们这次合并是快进模式，也

就是直接把master指向dev的当前提交，所以合并速度非常快。合并完成之后，就放心删除

xxx分支了，命令如下：

```
git branch -D xxx分支      // 删除xxx分支

git push origin :xxx分支名   // 删除远程仓库某分支

```

<br/>

### 解决分支冲突

当主干master和分支dev分别在同一个文件中，同一行代码中做出不同的修改并且commit之后，再从master上merge合并dev分支，会出现分支冲突的情况。那么它会出现如下内容提示:

```
$ git merge dev
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html 
// 那么出现冲突提示的是index.html文件
Automatic merge failed; fix conflicts and then commit the result.


```

然后用编辑器打开相对应的文件，会出现如下效果：

```
<<<<<<< HEAD
主分支修改的内容.......
=======
其他分支修改的内容.......
>>>>>>> dev

```

直接删除不需要的内容，做出最终的修改之后，保存文件，再去git进行add和commit操作，就自动合并完成，最后进行分支的删除。

```
git log --graph   // 查看分支合并过程图

```

<br/>

### 分支策略 && --no-ff模式

当我们在分支中进行修改并且commit之后，切换到主分支上面，那么从主分支master上merge某分支，在我们默认的情况下，使用的是快进模式Fast-forward，那么这种情况下，合并完分支之后使用git log--graph进行分支合并图信息的查看的时候，分支上的操作信息都会丢失。

所以我们应该采用--no-ff模式来进行分支的合并。这种模式下跟默认的快进模式的区别就是，在此模式下从master主分支上合并某分支之后，使用git log --graph能够在分支合并图上看到具体分支的合并过程。那么具体的方法就是，

```
首先切换到分支，进行修改然后commit，再切换到主分支上使用

git merge --no-ff -m "merge --no-ff dev" dev   

--no-ff是模式 ， -m是此次合并分支的描述 " " 当中是描述语 最后是选择合并哪一条分支

```

<br/>


#### 分支策略

在实际开发中，需要参照几个基本原则进行分支管理：

1.master分支只能用于发布版本，是最稳定的，不能在上面进行修改

2.需要团队工作，修改，我们需要创建一个分支，例如dev；

3.团队中所有人的工作分支，要在dev基础上创建自己的工作分支，每个人在自己修改完成之后commit，再合并到dev上，当一个重要功能做好之后，再从dev合并到主分支master上

4.一定要记住，团队在dev上创建的工作分支，一定要先merge到dev分支上，因为直接merge到master上面之后，dev分支上，依旧存在对应修改。当然直接merge到master主分支，git不会报错，只是会出现前面说的情况。如果非要这样，那么除非是最后dev也是要直接删除的，不然不推荐这样做。

5.在master分支上，创建了dev分支和del分支，分别在其之上还创建了dev2和del2分支，在子代分支上创建的后代分支上进行修改并且commit之后，直接merge到master分支上，那么后代分支的父分支（master子分支）依旧还会存在对应未修改的内容，同4。严格的来说，在分支上再次创建分支，其中他们之间的关系并不能用父子关系来定义，经过测试，在master上直接删除del分支，del2分支并不会同时被删除。所以说，在master主分支上创建的所有新分支，都是平级关系，互相修改commit不会影响对方，但是为了同步merge相对应的内容，不造成错乱，还需要遵守下图，依次merge到dev上，再一次性从dev来merge到master上，作为大版本更新。

<br/>

引用廖老师的图：

![分支策略](/images/posts/cite/branch.png)

<br/>

### Bug分支

当我们在master分支dev上面，做的修改并未提交或者根本就不能提交，然后突然之间接到任务，需要修复master分支上的bug时，那么我们又开始从master上新建一个分支del，但是我们现在dev分支上的内容还没完成，又不能提交怎么办？如果说贸然切换到del分支，进行修改commit，那么dev未add的内容，会把dev还未完成的修改在del上进行add，再commit的话，那么dev上修改的内容，会commit在del上进行提交推送到本地master分支上，那么将会出现问题。因为这不是你所希望的。那么我们如何将还未完成，尚不希望提交的内容进行隐藏，然后单独来处理bug呢？下面我们来继续：

首先我们在dev上未完成的工作要切换到对应分支，来使用下面的命令来进行隐藏：

```
git stash

```

那么这样使用这条命令之后，可以用git status 看到dev和master分支都没有工作区修改的显示，这就证明已经隐藏了，那么接下来我们来修复bug，首先确定在哪个分支上修复bug，假如在master上，就从master上新创建一个临时分支，修改完具体内容之后commit提交，然后切换到master分支上进行--no-ff合并操作，最后删除分支

```
git checkout -b dev          // 新建临时分支并操作
git commit -m "submit"       // 改完bug之后的提交
git checkout master          // 切换到master分支
git merge --no-ff -m "merge dev"  dev   //合并dev分支
git branch -d dev            // 删除dev分支
 
```

当bug修复完成之后，现在我们回到dev当时隐藏的对应未完成的工作分支，工作区是干净的，那么去哪儿了呢？所以使用命令查看：

```
git stash list

```

那么我们可以查看到所有隐藏了的工作区，那么要恢复则使用命令：

```
git stash apply

或者

git stash pop

```

那么他们的区别是：

第一种恢复方法： git stash apply恢复，但是恢复后，stash过往隐藏内容列表并不删除，你需要用git stash drop来删除

第二章恢复方法： 用git stash pop，恢复的同时把stash内容也删了

那么我们使用git stash pop恢复工作区之后，再用git stash list就看不到任何stash内容了，如果在工作中多次git stash 恢复的时候，先用git stash list查看，然后恢复指定的stash，命令如下：

```
git stash apply stash@{0}

```

<br/>

### 放弃del分支

当我们在工作中，接到任务说需要开发一个新功能，然后我们经过一系列的努力之后，准备要切回主分支合并然后删除分支，上级说此项任务终结不需要再添加进来了。那么这样的话，我们就需要将此分支给删除了，在master上，使用命令：

```
git branch -d del 

```

但是它出现了报错，说是del分支并未合并：

```
$ git branch -d del
error: The branch 'del' is not fully merged.
If you are sure you want to delete it, run 'git branch -D del'.

```

那么我们来使用强制删除操作命令，来销毁del分支：

```
git branch -D del

```

因为del分支并未合并，那么如果删除掉之后，数据就会丢失。其实不需要的这个分支并不一定要删除，只是留着会显得很混乱而已。

<br/>

### 多人协作

#### 推送分支

其实推送分支，就是把本地分支推送更新到远程库，推送的时候，需要具体指定推送的本地分支名，那么git就会推送到远程库上对应的分支，比如：

```
git push origin master        //推送到master分支上

或者

git push origin dev           //推送到dev分支上

```

但是，我们其实并不需要把所有的分支全部推送到远程库上去，一部分需要，一部分不需要：

第一，master分支一般都是主分支，是更新大版本或者已经具体确定发布内容的，就需要推送到远程库，并且要时刻同步更新；

第二，dev是开发分支，我们团队里面所有开发人员都要在上面进行开发，同样需要同步远程库；

第三，在dev分支之下，新的bug修复分支，就不用推送到远程库了，除非需要看具体时间内，到底修复了几个bug；

第四，del分支，具体推送不推送到远程库，也是自己决定。

所以，对于哪些分支是否推送到远程库，完全是自己来决定的。

#### 抓取分支

当团队中有多名开发人员，协作开发时，大家都在向master、dev分支推送修改，现在一名小伙伴，在他电脑上克隆了远程库，但是克隆下来，他只能看到master分支，这是真的，那么他需要在dev分支上进行开发，那么就要创建远程origin的dev分支到本地，所以开始使用下面的命令操作：

```
git checkout -b dev origin/dev   // 创建远程dev分支到本地

```

那么下面他就可以在dev分支上面进行修改了然后push到远程dev分支，ps：也同样可以在dev分支上创建分支，再合并，只有最后merge到dev分支，然后一个小版本就推送到远程dev就好了。

当他push完之后，刚好，你之前也在同样的文件，同一个地方进行了修改push，接下来他那边显示push失败，原因是有冲突，那么我就使用命令把最新的提交拉取到本地来，合并再提交：

```
git pull   

```

突然，他那边显示git pull也失败了，因为没有指明具体要拉取合并更新的具体分支，那么使用命令：

```
git branch --set-upstream dev origin/dev  

```

再次进行git pull，合并成功，但是由于两个人都在同一个文件同一个地方进行了修改，推送，所以出现了冲突，那么就进入对应文件解决冲突，保存，add，commit之后再次使用命令：

```
git push origin dev   // 推送到dev分支

```

最后协作开发一小阶段就完毕了。

所以在多人协同开发中，具体模式一般是：

第一，首先推送自己的修改到对应分支 ps：git ```push origin xx分支```

第二，如果说某个人推送失败，那是由于远程仓库比本地仓库要新，所以需要用```git pull``` 来合并；

第三，如果说合并冲突失败了的话，那么修改合并之后提交到本地库之后push到dev分支

其中，git pull时如果出现以下提示：

```
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 2), reused 3 (delta 2), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:hopeverse/xx
   7ae51ac..e4fb3d8  dev        -> origin/dev
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev


```

这就说明本地分支和远程分支相互之间的跟踪信息没有建立，需要使用命令：

```
git branch --set-upstream-to=origin/<branch> dev   

```

最后多人协作开发模式结束.

<br/>

### 创建Tag标签

其实创建tag标签，就是为了替代我们在需要对应历史版本的时候，解决commit_id过于繁琐而发明的一种标记方法，这样，我们今后在恢复历史commit版本时，就可以直接恢复对应tag标签，让人更加直观，明确的知道是哪一个版本。

创建标签命令：

```
git tag v1.0          // 此处git tag为固定格式，后面为标签号

```

每一次的默认标签，都是打在了最近一次commit上了。如果我们希望看看现在有多少个标签了，键入命令：

```
git tag               // 查看所有tag标签

```

当我们希望在某一次历史commit上打标签，那么方法是：首先找到历史commit_id，然后键入命令。例如：

```
git log --pretty=oneline --abbrev-commit     // 查看历史commit简要信息     
5ffse2 merge three
8dw23a merge two
9se54v merge one

```

接下来我希望给merge two 打上tag标签，那么键入命令：

```
git tag vx.x 8dw23a 

```

这里要注意：标签并非按时间顺序，而是按照字母顺序来进行排列，如需查看具体标签内容：

```
git show vx.x 

```

不仅如此，还可以创建带有说明文字的标签：

```
git tag -a vx.x -m "说明文字" commit_id

```

如果想看到历史所有tag标签，对应的是那一次的commit，那么输入命令：

```
git tag -l -n

```

假设标签打错了的话，使用下方命令则可以删除：

```
git tag -d xxx      // 删除具体xxx标签

```

标签都只是保存在本地，不会推送到远程。那么如果需要推送到远程，使用命令：

```
git push origin tagname     //推送tagname标签到远程

```

如果感觉每次推送一个标签到远程比较麻烦，那么可以使用下方命令，一次性推送：

```
git push origin --tags      // 一次性推送所有标签至远程

```

那么当tag标签已经推送到远程了之后，我们想删除，那么就分下面两步进行操作：

第一、首先在本地仓库删除tag标签：

```
git tag -d xxx    

```

第二、然后删除远程tag标签：

```
git push origin :refs/tags/xxx   //删除远程某个xxx标签

```

<br/>

### 自建Git服务器

github是一个免费的开源代码托管平台，但是有些公司或者个别开发者并不希望将自己的代码开源，那么有两个办法，第一个就是自己开通一个私有仓库的服务，当然这是要钱的。第二个就是今天要讲的自建Git服务器。那样我们就可以将它作为私有仓库啦。那么开始说自建git服务器的步骤：

前言，搭建git服务器需要在一台linux机器上那么最好也最简单，ubuntu是个不错的选择

第一，安装git 

```
$ apt-get install git

```

第二，创建git用户，来运行git相关服务

```
$ sudo adduser git 

```

第三，创建证书登录git

将所有需要参与开发的人员的公匙```id_rsa.pub```文件，导入进```/home/git/.ssh/authorized_keys``` ，每行输入一个

第四，初始化git仓库

选择一个文件夹作为git仓库，然后在对应文件夹下键入命令：

```
$ sudo git init --bare xxx.git    // 你到时候需要克隆的仓库名称xxx
```

这样git就创建了一个毫无任何东西的仓库，然后把owener改成git：

```
$ sudo chown -R git:git xxx.git   //git名同上

```

第五，禁shell登录

为了安全，git用户不能登陆shell，那么可以编辑```/etc/passwd```文件做到。

```
找到git:x:1001:1001:,,,:/home/git:/bin/bash

修改 -->

git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell

```

这样用户就不能登录shell了。

第六，克隆远程仓库

```
git clone git@server:/srv/xxx.git

```


**最后，Git的学习记录到此结束。多使用，熟练于心，那么它会给我们带来非常大的便捷！**

>如需转载，请注明出处。谢谢！

[https://liutianzhu.me](https://liutianzhu.me)
