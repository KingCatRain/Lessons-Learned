# django环境搭建

## 安装python

输入 `python` 可以查看 ***python*** 版本，且进入 ***python*** 环境，可以输入： `exit()` 来退出 ***python*** 环境

## 安装 Pip

### 下载

下载 [***get-pip.py***](https://bootstrap.pypa.io/get-pip.py) 安装包

到下载文件所在目录，然后运行一下命令（需要有管理员权限）：

~~~
$ python get-pip.py
~~~

## 安装Django

### 下载

从 ***Github*** 上[下载最新版本](https://github.com/django/django)

~~~
$ git clone https://github.com/django/django.git
~~~

### 安装

进入解压后的目录：

~~~
$ cd Django-1.x.y
$ sudo python setup.py install
~~~

安装成功后会输出一下信息

~~~
……
Processing dependencies for Django==1.x.y
Finished processing dependencies for Django==1.x.y
~~~

再进入站点目录，创建 ***Django*** 项目：

~~~
$ django-admin.py startproject testdj
~~~

启动服务：

~~~
$ cd testdj # 切换到我们创建的项目
$ python manage.py runserver
...
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
~~~

以上信息说明：项目已启动，访问地址为：http://127.0.0.1:8000/.

## 安装Venv

虚拟环境是一个将不同项目所需求的依赖分别放在独立的地方的一个工具，它给这些工程创建虚拟的 ***Python*** 环境。它解决了 “项目X依赖于版本1.X，而项目Y需要版本4.X”的两难问题，而且使你的全局 ***site-packages*** 目录保持干净和可管理。

比如，你可以工作在一个需 ***Django 1.3*** 的工程，同事维护一个需求 ***Django 1.0*** 的工程。

### Virtualenv

***vitualenv*** 是一个创建隔绝的 ***Python*** 环境的工具。***virtualenv*** 创建一个包含所有必要的可执行文件的文件夹，用来使用 ***Python*** 工程所需的包。

通过 ***pip*** 安装 ***virtualenv*** ：

~~~
$ pip install virtualenv
~~~

### 基本使用

* 为一个工程创建一个虚拟环境：

~~~
$ cd my_project_folder
$ virtualenv
~~~

`virtualenv venv` 将会在当前目录创建一个文件夹，包含了 ***Python*** 可执行文件，以及 ***pip*** 库的一个拷贝，这样就能安装其他包了。虚拟的环境名字（此例中的是venv）可以是任意的，若省略名字会把文件均放在当前目录。

在任何你运行的命令的目录中，这会创建 ***Python*** 的拷贝，并将之放在叫做 ***venv*** 的文件中。

你可以选择使用一个 ***Python*** 的解释器：

~~~
$ virtualenv -p /usr/bin/python2.7 venv
~~~

这将会使用 /usr/bin/Python2.7 中的 ***Python*** 解释器。

* 要开始使用虚拟环境，其需要被激活：

~~~
$ source venv/bin/activate
~~~

当前虚拟环境的名字会显示在提示符左侧（比如说（venv）你的电脑：你的工程 用户名 $）以让你知道它是激活的。从现在起，任何你使用 ***pip*** 安装的包将会放在 `venv` 文件夹中，与全局安装的 ***Python*** 隔绝开。

像平常一样安装包，比如：

~~~
$ pip install requests
~~~

* 如果你在虚拟环境中暂时完成了工作，则可以停用它：

~~~
$ deactivate
~~~

这将会回到系统默认的 ***Python*** 解释器，包括已安装的库也会回到默认的。

要删除一个虚拟环境，只需要删除他的文件夹。（要怎么做请执行 `rm -rf venv`）然后一段时间后，你可能会有很多个虚拟环境散落在系统各处，你将有可能会忘记他们的名字或者位置。

## 起服务

在 ***venv*** 下，运行 `python manage.py runserver`