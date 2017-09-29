##Git时间-最简单的命令行
---

最近开始学习使用Git和GitHub，总结一下Windows下的基本使用，详细参数可以参考[官方文档](https://git-scm.com/)等教程。
<br/>

###Git 安装
---
Windows下使用Git需要配置Cygwin之类的模拟环境。当然工具安装过程越简单越好，直接从[msysgit](https://git-for-windows.github.io/)下载.exe，默认选项安装，完毕。

<br/>

###Git 使用
---
在电脑任意位置右击打开Git Bash，然后愉快的输入命令行吧~

**git config**

顾名思义，config是用来对Git进行一些配置，首先用到的就是配置当前机器用户的姓名和Email地址

```
$ git config --global user.name "name"
$ git config --global user.email "email@example.com"
```

**git init**

Git一个基本概念就是**仓库(repository)**，简单点理解，创建的每个仓库都对应某个文件夹，仓库管理的就是该文件夹内的文件增删查改。

在想要创建仓库的目录下打开Git Bash，输入init命令就创建了一个新的仓库，然后就可以随心所欲的操作对应目录下的文件了。相对的本地仓库的删除也十分简单，直接把文件夹删除就可以了。

```
$ git init
```

**git status**

status命令可以用来查询当前目录下文件的修改情况，绿色是已经提交的部分，红色是增加或者修改后未保存的部分。

```
$ git status
```

**git add**

add命令是最常用的，要和commit命令搭配使用，可以看做一个保存动作。后边可以为. /filename /foldername，分别对应所有文件，文件和子文件夹。


**git commit**

commit命令的字符串描述了本次保存操作，也是告诉Git这次保存结束了。

```
$ git add .
$ git add file.txt
$ git add folder
$ git commit -m "Description of commit"
```

**git rm**

和增加对应的就是删除操作。

```
$ git rm file.txt
$ git rm -rf folder
```

考虑到远程操作[见下一节]，如果想只删除repository上的文件夹，直接用git rm会使本地的文件夹也被删除，此时应该[删除缓冲](https://stackoverflow.com/questions/7927230/remove-directory-from-remote-repository-after-adding-them-to-gitignore)。还遇到过一些[其他问题](https://help.github.com/articles/removing-sensitive-data-from-a-repository/)。

```
$ git rm -r --cached some-directory
$ git commit -m "Remove"
$ git push origin master
```

<br/>

###Git 远程操作
---
现在我们有了本地的管家，但是电脑不在手边又想修改怎么办呢，那就需要[GitHub](https://zh.wikipedia.org/wiki/GitHub)啦。首先注册一个GitHub账号，按照网站的引导创建一个repository。不勾选生成README.md，就可以看到如下教程
![](methods.png)
在需要远程的仓库位置打开Git Bash，粘贴git remote add...和git push...语句就可以将仓库和远程主机连接啦~

**git remote**

我们来看看刚刚复制的命令是做什么的，remote用来管理主机名，可以对远程主机进行添加、删除、重命名和查询。其中添加就是上边的连接部分啦。

```
$ git remote add <主机名> <网址>
$ git remote rm <主机名> 
$ git remote rename <原主机名> <新主机名>
$ git remote show <主机名>
```

只使用git remote时，会列出所有的远程主机。这里的网址可以是[SSH](https://zh.wikipedia.org/wiki/Secure_Shell)或者HTTP，在GitHub里边点击绿色的Clone or download按钮就可以查看哟。

**git clone**

一般来说，远程操作要先从远程主机克隆一个版本库，与本地的一个目录关联，默认与远程主机版本库同名。

```
$ git clone <版本库的网址>
$ git clone <版本库的网址> <本地目录名>
```

这里的网址同样是HTTP、SSH、Git或者本地协议文件。

**git push**

push命令用于将本地分支的更新同步到远程主机。例如将本地的master分支推送到origin主机的master分支，远程分支不存在则被创建。

```
$ git push <远程主机名> <本地分支名>:<远程分支名>
$ git push origin master
```

**git pull**

pull命令用来取回远程主机某个分支的更新，然后和本地的合并。例如取回origin主机的next分支，和本地的master分支合并。

```
$ git pull <远程主机名> <远程分支名>:<本地分支名>
$ git pull origin next:master
```


**git fetch**

fetch命令同样是取回远程主机的更新，与pull的区别在于，它不会修改本地的仓库。默认情况下取回所有分支的更新，当然也可以自己指定。例如取回origin主机的master分支。

```
$ git fetch <远程主机名>
$ git fetch <远程主机名> <分支名>
$ git fetch origin master
```

远程操作部分[阮一峰老师](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)写得很好，本篇有所参考。

配方简单，食用愉快~ =)



