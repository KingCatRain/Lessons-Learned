# iTerm2 配置

## 下载

登录[官网下载](http://www.iterm2.com)最新 ***iTerm2*** 

## 使用zsh

一般mac会自动带着zsh，可以用 `zsh --version` 来查看zsh的版本。

### 安装zsh

via curl

~~~
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
~~~

via wget

~~~
wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | sh
~~~

### oh my zsh 安装

克隆仓库：

~~~
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
~~~

如果你已存在~/.zshrc文件，则备份现有的~/.zshrc文件

~~~
cp ~/.zshrc ~/.zshrc.orig
~~~

改变默认shell

~~~
chsh -s /bin/zsh
~~~

重新启动你的终端（Terminal）

## 配置护眼配色

### 下载

登录 [SOLARIZED](http://ethanschoonover.com/solarized) 查看文档，下载配置文件包到本地。
进入 ***iTerm2 -> reference -> Profiles -> Color Presets -> Solarized Dark***

### 配置主题

`zsh`的配置主要集中在用户当前目录的`.zshrc(~/.zshrc)`里。我主要进行了一下配置:

~~~
alias cls='clear'  
alias ll='ls -l'  
alias la='ls -a'  
alias vi='vim'  
~~~

在`.zshrc`里找到`ZSH_THEME`，就可以设置主题了，默认主题是:

~~~
ZSH_THEME="robbyrussell"
~~~

将其修改成

~~~
ZSH_THEME="agnoster"
~~~

主题我们在哪儿看了？就是在我们之前下载的 `Oh My Zsh` 的主题里面，具体的地址如下:

~~~
/Users/chenyuan/.oh-my-zsh/themes
~~~

每次修改完了 `.zshrc` 文件，都必须重新`source`一下才行。就是`source ~/.zshrc`才能生效。

到这里，还是不够美观，漂亮的箭头还是没有出现，那是应为字体的原因，需要对Mac的字体库进行安装。这里有一个地址，是可以下载到本地，然后安装的。

~~~
git clone https://github.com/supermarin/powerline-fonts.git
~~~

下载完安装字体 `Monaco for Powerline`

进入 ***iTerm2 -> reference -> Profiles -> Text*** 把 ***Font*** 和 ***Non-ASCII-Font*** 都设置成 ***Monaco for Powerline***


## 更多详细信息请参考

* [iTerm2 + Zsh + Oh My Zsh + solarized](http://www.cyblogs.com/iterm2-zsh-oh-my-zsh-solarized/)
* [oh my zsh 官网](http://ohmyz.sh)
* [Solarized 官网](https://github.com/altercation/solarized)