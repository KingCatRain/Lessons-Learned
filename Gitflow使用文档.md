# 版本管理系统使用

## Git安装及使用

***git***   是一款高效的分布式版本管理系统
### 下载：
* 如果是 ***OSX*** 系统，安装 ***Xcode*** ，会自带 ***Git***

* 也可以打开终端执行如下脚本

~~~
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
~~~

* 也可以 [点击这里下载](https://git-scm.com/download/mac/)，并安装！

## Brew 安装

如果机器没有 ***brew*** 可以执行下边代码安装，也可以阅读[官网文档](http://brew.sh/index_zh-cn.html)

~~~
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
~~~

## 生成SSH密钥

生成 ***Git SSH KEY*** 对提高频繁操作 ***git*** 有提高效率的好处，如何生成：

### 设置Git的user name和email：

~~~
$ git config --global user.name "name"
$ git config --global user.email "name@mail.com"
~~~

### 生成SSH密钥：

1. 查看是否已经有了 ***ssh*** 密钥：`cd ~/.ssh` 如果没有密钥则不会有此文件夹，有则备份删除。

2. 生成密钥：

~~~
ssh-keygen -t rsa -C "name@mail.com"
~~~

按三个回车密码为空，最后得到了两个文件：***id_rsa*** 和 ***id_rsa.pub***

3. 添加密钥到 ***ssh：ssh-add*** 文件名，需要之前输入密码。

4. 在github上添加ssh密钥，这要添加的是 ***id_rsa.pub*** 里面的公钥。复制公钥出来，然后登录 ***Git*** 网站，添加SSH。

## Git-flow安装及使用

### 基础建议
> ***Git-flow*** 提供了极出色的命令帮忙以及输出提示。请仔细阅读并观察发生了什么事情

> ***OSX*** 程序 [Sourcetree](https://www.sourcetreeapp.com) 是一个极出色的 ***Git*** 界面客户端，已经提供了 ***Git-flow*** 的支持
 
> ***Git-flow*** 是一个基于归并的解决方案，它并没有提供重置(rebase)特性分支的能力

### 安装
> 确定本机已安装 ***Git***，可以执行 `$ git --version` 查看 ***git*** 版本
>
> ***osx*** 系统下安装 ***Git-flow*** ,需要执行 

~~~
$ brew install git-flow-avh
~~~




> 更多的 ***Git-flow*** 安装指引，请阅读 [Git-flow wiki](https://github.com/petervanderdoes/gitflow-avh/wiki/Installing-on-Mac-OS-X)

### 初始化
> 需要再现有的一个git库中执行。

~~~
$ git flow init
~~~

> 你必须回答几个关于分支的命名约定的问题。
建议使用默认值。

### 建立新分支
> 新分支的开发是基于 ***develop*** 分支的。通过下面的命令建立新分支:

~~~
$ git flow feature start MYFEATURE
~~~
> 这个操作创建了一个基于'develop'的特性分支，并切换到这个分支之下。

### 完成新分支

> 完成开发新分支执行：

~~~
$ git flow feature finish MYFEATURE
~~~
> 这个动作执行了以下操作：
> 
> 合并 ***MYFEATURE*** 分支到 ***develop***
> 
> 删除这个新特性分支
> 
> 切换回 ***develop*** 分支

### 发布新特性

> 你是否合作开发一项新分支？
发布新分支到远程服务器，所以，其它用户也可以使用这分支。

~~~
$ git flow feature publish MYFEATURE
~~~

### 获取新分支

> 取得其它用户发布的新分支，并签出远程的变更。

~~~
$ git flow feature pull origin MYFEATURE
~~~

> 你也可以使用
 
~~~
$ git flow feature track MYFEATURE
~~~
> 跟踪 ***origin*** 上的特性分支。



### 紧急修复

> 紧急修复来自这样的需求：生产环境的版本处于一个不预期状态，需要立即修正。
> 
> 有可能是需要修正 ***master*** 分支上某个 ***TAG*** 标记的生产版本。

### 开始紧急修复

> 像其它 ***Git-flow*** 命令一样, 紧急修复分支开始自：
 
~~~
$ git flow hotfix start VERSION [BASENAME]
~~~

> ***VERSION*** 参数标记着修正版本。你可以从 [BASENAME]开始，[BASENAME]为***finish release*** 时填写的版本号。

### 完成紧急修复

> 当完成紧急修复分支，代码归并回 ***develop*** 和 ***master*** 分支。相应地，***master*** 分支打上修正版本的 ***TAG***。
 
~~~
$ git flow hotfix finish VERSION
~~~

### merge

从develop分支，merge到当前分支

~~~
$ git merge develop 
~~~

## 更多详细信息请参考

* [Git 使用文档](http://www.cnblogs.com/goody9807/p/4372477.html)
* [Git-flow 备忘清单](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html) 
* [如何正确使用 Git-flow](http://www.cnblogs.com/cnblogsfans/p/5075073.html)
