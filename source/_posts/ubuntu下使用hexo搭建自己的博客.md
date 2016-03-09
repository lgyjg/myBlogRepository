title: ubuntu下使用hexo搭建自己的博客
date: 2016-03-06 21:43:12
tags:
---

## ubuntu下使用hexo搭建自己的博客

hexo是Hexo 是一个快速、简洁且高效的博客框架。可以生成静态页面的博客，Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。在本地搭建好环境后，以后发布博客只需要几条简单的命令将生成博客文件通过git，发布到github或者其他git库中即可。
>关于hoxo详细的介绍请查看官方文档：[hexo gitio](https://hexo.io/zh-cn/docs/index.html)

接下来就直接看看搭建过程吧。


----------


### 安装git
git，我想大多数读者是安装了的，因为需要使用到git发布博客，所以这里简单提下：
>sudo apt-get install git-core

### 安装Nodejs
**Node.js**是一个开放源代码、跨平台的、可用于服务器端和网络应用的运行环境。Node.js应用JavaScript语言写成，在Node.js运行时运行。它支持OS X、Microsoft Windows、Linux、FreeBSD、NonStop、IBM AIX、IBM System z和IBM i等众多平台。详见：[Nodejs官方网址](https://nodejs.org/en/)

hexo生成静态网页使用到了nodejs的技术，所以首先我们需要安装nodejs。安装nodejs的方法很多，以下介绍两种常用的方法：
### 1.使用apt-get命令安装nodejs
>sudo add-apt-repository ppa:chris-lea/node.js、
>sudo apt-get update
>sudo apt-get install nodejs
这种方式简单，不过它自带的版本可能过低，所以需要添加源。以后升级也不方便。

### 2.使用nvm安装nodejs
这里使用shell下的下载工具curl或者wget来完成nvm的安装：
>curl https://raw.github.com/creationix/nvm/master/install.sh | sh  
或者使用以下工具：
>wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh

等nvm安装完之后就可以使用nvm来安装nodejs了。
**首先查看下最新的远程nodejs的版本。**
> nvm ls-remote

选择最新的版本进行安装：
>nvm install v5.7.1

如果安装过程没有问题，恭喜你完成了nodejs的安装。接下来安装重头戏hexo。

### 安装hexo
>npm install -g hexo

安装完后就可以进行部署写作了。

### 生成博客目录
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
> hexo init  文件夹
> cd 文件夹
> npm install

在这里你就可以使用hexo命令创建你自己的blog了。更多关于hexo的使用请访问：[hexo doc](https://hexo.io/zh-cn/docs/writing.html)

>**注意：**转载请注明出处
