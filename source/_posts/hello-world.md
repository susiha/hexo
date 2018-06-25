---
title: 通过Hexo创建个人博客
date: 2016-06-01 23:47:44 #文章生成時間
categories: "Hexo教程" #文章分类目录 可以省略
tags: #文章标签 可以省略
     - 教程
     - 其他
---
<!--Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).-->
本文是结合网络上的教程以及自己摸索中的经历而成的，旨在记录和总结,因为并不懂前端和和不十分懂这些命令，因此不会阐述这些命令是什么意思。所有注释只是根据自己实践中的理解以及结果网上给出的注释。




## 准备部分

### 安装NodeJs
Hexo 是基于NodeJs的静态博客,特别是npm 命令 非常有用，后面会用到很多
[下载地址](http://nodejs.cn/download/)
安装很简单 安装完成之后可以在终端测试
``` bash
$ node -v
```
能看到的是安装的版本号
因为npm默认的源的下载速度很慢，因此设置淘宝的镜像服务，命令如下

``` bash
$ npm config set registry "https://registry.npm.taobao.org"
```

### 安装Hexo
先在电脑上创建一个文件夹，我自己的叫blog,然后cd 到blog目录下

``` bash
$ hexo init 
$ npm install
```
完成之后blog文件夹下面应该是这样的结构

```bash
├── _config.yml
├── package.json
├── scaffolds
├── source
 |   ├── _drafts
 |   └── _posts
└── themes
```


### 安装git

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)
