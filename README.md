# Git_File_Crazy_Test

#### 介绍---百度百科
Git（读音为/gɪt/）是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。 [1] Git 是 [Linus Torvalds](https://baike.baidu.com/item/Linus Torvalds/9336769) 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

Torvalds 开始着手开发 Git 是为了作为一种过渡方案来替代 BitKeeper

#### 特点

[编辑](javascript:;)

分布式相比于集中式的最大区别在于开发者可以提交到本地，每个开发者通过克隆（git clone），在本地机器上拷贝一个完整的Git仓库。

下图是经典的git开发过程。

[![img](https://bkimg.cdn.bcebos.com/pic/a71ea8d3fd1f4134ca7667d8251f95cad0c85ed6?x-bce-process=image/resize,m_lfit,w_220,h_220,limit_1)](https://baike.baidu.com/pic/GIT/12647237/0/a71ea8d3fd1f4134ca7667d8251f95cad0c85ed6?fr=lemma&ct=single)

Git的功能特性：

从一般开发者的角度来看，git有以下功能：

1、从服务器上克隆完整的Git仓库（包括代码和版本信息）到单机上。

2、在自己的机器上根据不同的开发目的，创建分支，修改代码。

3、在单机上自己创建的分支上提交代码。

4、在单机上合并分支。

5、把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。

6、生成补丁（patch），把补丁发送给主开发者。

7、看主开发者的反馈，如果主开发者发现两个一般开发者之间有冲突（他们之间可以合作解决的冲突），就会要求他们先解决冲突，然后再由其中一个人提交。如果主开发者可以自己解决，或者没有冲突，就通过。

8、一般开发者之间解决冲突的方法，开发者之间可以使用pull 命令解决冲突，解决完冲突之后再向主开发者提交补丁。

从主开发者的角度（假设主开发者不用开发代码）看，git有以下功能：

1、查看邮件或者通过其它方式查看一般开发者的提交状态。

2、打上补丁，解决冲突（可以自己解决，也可以要求开发者之间解决以后再重新提交，如果是开源项目，还要决定哪些补丁有用，哪些不用）。

3、向公共服务器提交结果，然后通知所有开发人员。

优点：

适合[分布式开发](https://baike.baidu.com/item/分布式开发)，强调个体。

公共服务器压力和数据量都不会太大。

速度快、灵活。

任意两个开发者之间可以很容易的解决冲突。

离线工作。

缺点：

资料少（起码中文资料很少）。

学习周期相对而言比较长。

不符合常规思维。

代码保密性差，一旦开发者把整个库克隆下来就可以完全公开所有代码和版本信息。



#### 介绍

## 介绍

[编辑](javascript:;)

Git --- The stupid content tracker, 傻瓜内容跟踪器。Linus Torvalds 是这样给我们介绍 Git 的。

Git 是用于 Linux[内核](https://baike.baidu.com/item/内核)开发的[版本控制](https://baike.baidu.com/item/版本控制)工具。与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持（wingeddevil注：这得分是用什么样的服务端，使用http协议或者git协议等不太一样。并且在push和pull的时候和服务器端还是有交互的。），使[源代码](https://baike.baidu.com/item/源代码)的发布和交流极其方便。 Git 的速度很快，这对于诸如 Linux kernel 这样的大项目来说自然很重要。 Git 最为出色的是它的合并跟踪（merge tracing）能力。

实际上[内核](https://baike.baidu.com/item/内核)开发团队决定开始开发和使用 Git 来作为内核开发的版本控制系统的时候，世界开源社群的反对声音不少，最大的理由是 Git 太艰涩难懂，从 Git 的内部工作机制来说，的确是这样。但是随着开发的深入，Git 的正常使用都由一些友好的脚本命令来执行，使 Git 变得非常好用，即使是用来管理我们自己的开发项目，Git 都是一个友好，有力的工具。现在，越来越多的著名项目采用 Git 来管理项目开发.

作为开源自由原教旨主义项目，Git 没有对版本库的浏览和修改做任何的权限限制。

目前GIT已经可以在windows下使用，主要方法有二：msysgit和Cygwin。Cygwin和Linux使用方法类似，Windows版本的GIT提供了友好的GUI(图形界面)，安装后很快可以上手，不在此做大篇幅介绍。

本文将以 Git 官方文档 Tutorial， core-tutorial 和 Everyday GIT 作为蓝本翻译整理，但是暂时去掉了对 Git 内部工作机制的阐述，力求简明扼要，并加入了作者使用 Git 的过程中的一些心得体会，注意事项，以及更多的例子。建议你最好通过你所使用的 Unix / Linux 发行版的安装包来安装 Git, 你可以在线浏览本文 ，也可以通过下面的命令来得到本文最新的版本库，并且通过后面的学习用 Git 作为工具参加到本文的创作中来。

(Snake.Zero 注：以下假设环境为Unix/Linux，本次修正主要是版本问题，git-add git-init-db等命令都改为了类似git add形式的，以免误导新手。)

#### 增加内容

[编辑](javascript:;)

增加内容跟踪信息：git add

为了简明起见，我们创建两个文件作为练习：

```
$``echo``"Helloworld"``>hello``$``echo``"SnakeZero"``>snake
```

我们再用 git add 命令将这两个文件加入到版本库文件索引当中：

```
$git add hello snake
```

git add 实际上是个脚本命令，它是对 git 内核命令 git update-index 的调用。因此上面的命令和下面的命令其实是等价的：

```
$git update-index --add hello snake
```

如果你要将某个文件从 git 的目录跟踪系统中清除出去，同样可以用 git update-index 命令。例如：

```
$git update-index --force-remove foo.c
```

注意：

git add 可以将某个目录下的所有内容全都纳入内容跟踪之下，例如： git add ./path/to/your/wanted 。但是在这样做之前，应该注意先将一些我们不希望跟踪的文件清理掉，例如，gcc 编译出来的 *.o 文件，vim 的交换文件 .*.swp 之类。

应该建立一个清晰的概念就是，git add 和 git update-index 只是刷新了 git 的跟踪信息，hello 和 snake 这两个文件中的内容并没有提交到 git 的内容跟踪范畴之内。

普通用户总是应该使用 git add， 而不要使用上面提到的 update-index[内部命令](https://baike.baidu.com/item/内部命令)。

添加所有未[跟踪文件](https://baike.baidu.com/item/跟踪文件)用 git add -A, 添加所有未跟踪文件并且提交用 git commit -a。（注意大小写）

从当前跟踪文件中删除用 git reset HEAD <filename>。事实上也就是用当前 HEAD（commited） 中的内容替换掉 index（staging） 的内容。

#### 参与贡献

## 提交内容

[编辑](javascript:;)

提交内容到版本库：

```
git commit
```

既然我们刷新了 Git 的跟踪信息，现在我们看看版本库的状态：

```
git status
```

我们能看到 git 的状态提示：

```
#``#Initial commit``#``#``#Updated but not checkedin:``#(willcommit)``#``#newfile:example``#newfile:hello``#
```

提示信息告诉我们版本库中加入了两个新的文件，并且 git 提示我们提交这些文件，我们可以通过 git commit 命令来提交：

```
$git commit -m ``"Initial commit of git tutor reposistory"
```

查看当前的工作：git diff

git diff 命令将比较当前的工作目录和版本库数据库中的差异。现在我们编辑一些文件来体验一下 git 的跟踪功能。

```
$``echo``'这段是后来加的'``>snake
```

我们再来比较一下，当前的工作目录和版本库中的数据的差别。

```
$gitdiff
```

差异将以典型的 patch 方式表示出来：

```
diff``--gita``/snakeb/snake``index3b85043..d79f20a100644``---a``/snake``+++b``/snake``@@-1+1@@``-snakezero
```

+这段是后来加的

此时，我们可以再次使用组合命令 git add 和 git commit 将我们的工作提交到版本库中。

```
$git add snake``$git commit -m ``"new day for git"
```

实际上，如果要提交的文件都是已经纳入 git 版本库的文件，那么不必为这些文件都应用 git add 命令之后再进行提交，下面的命令更简捷并且和上面的命令是等价的。

```
$git commit -a -m``"new day for git"
```


#### 码云特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  码云官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解码云上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是码云最有价值开源项目，是码云综合评定出的优秀开源项目
5.  码云官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  码云封面人物是一档用来展示码云会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
