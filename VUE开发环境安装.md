# VUE开发环境安装

## 安装依赖

### NodeJS
> 最新稳定版（6.2.0），可以从 [官网](https://nodejs.org/en/) ，或者 [中文网](http://nodejs.cn/) 下载安装。安装完成后可用 `$ node -v` 来查看版本。

### NPM
> 安装完 ***NodeJS*** 后会自带 ***NPM*** ,但可能不是最新版本，可以执行：

~~~
$ npm install -g npm 
~~~

> 来升级到最新版本，安装完成后可用 `$ npm -v` 来查看版本。

###CNPM
> 由于网络环境问题，建议使用 ***CNPM*** (淘宝镜像)。这是一个完整 ***npmjs.org*** 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。

> ####执行以下脚本来安装：

~~~
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
~~~

> 可以通过 `$ cnpm -v` 来查看 ***CNPM*** 的版本
>
> ####安装模块：
> 
> 使用时跟 ***NPM*** 语法一致：

~~~
$ cnpm install [name]
~~~ 

> ####同步模块：
> 
> 直接通过 sync 命令马上同步一个模块, 只有 cnpm 命令行才有此功能:

~~~
$ cnpm sync connect
~~~

> 当然, 你可以直接通过 web 方式来同步: [/sync/connect](https://npm.taobao.org/sync/connect)

~~~
$ open https://npm.taobao.org/sync/connect
~~~


## 开始安装

### VUE

> ####安装VUE：

~~~
$ npm install vue
~~~

> 安装完后为 ***VUE*** 最新版本，可以用 `$ vue -V` 来查看版本。

### VUE-CLI(用来搭框架，开发可忽略)

> ***vue-cli***为官方脚手架，用来快速搭建 ***VUE*** 项目
> 
> #### 安装 VUE-CLI：

~~~
$ npm install -g vue-cli
~~~

> #### 搭建 VUE 框架：

~~~
$ vue init <template-name> <project-name>
~~~

> ***template-name*** 为项目模板，官放提供 ***webpack*** 、 ***webpack-simple*** 、 ***browserify*** 、 ***browserify-simple*** 、 ***simple*** 五个模板，下面以 ***webpack*** 为例：
 
~~~
$ vue init webpack my-project
~~~

#### 安装框架依赖：

> 执行下边脚本安装 ***VUE*** 依赖：

~~~
$ cd my-project
$ npm install
~~~

## 起服务

> 启动服务，方便调试，进入项目所在文件夹：

~~~
$ npm run dev
~~~


## 参考文档

* [NodeJS中文网](http://nodejs.cn/)
* [NPM官网](https://www.npmjs.com/)
* [CNPM官网](http://npm.taobao.org/)
* [VUE官网](http://cn.vuejs.org)
* [vue-cli官网](https://github.com/vuejs/vue-cli)
* [vue-cli脚手架总结](http://www.cnblogs.com/Shinnosuke/p/5680818.html)