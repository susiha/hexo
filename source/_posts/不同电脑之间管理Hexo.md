---
title: 不同电脑之间管理Hexo
date: 2018-06-22 17:06:08
categories: "Hexo教程" #文章分类目录 可以省略
tags: #文章标签 可以省略
     - 教程
     - 其他
---

####新建远程repo

在github上新增repo，例如名为hexo，地址为github.com/xxx/hexo

####在旧终端中创建本地repo

进入本地hexo目录
```bash
git init
```

####查看未提交的文件（默认不包含public、deploy文件）
```bash
git status
```

根据查看结果将本地hexo建站原始文件纳入版本控制（我本地是scaffolds、source、themes文件夹以及.gitignore、_config.yml、package.json文件）
```bash
git add …
git commit -m …
```
需要注意的是.gitignore中需要增加一行，忽略~结尾的文件

*~

####在旧终端中创建远程分支连接
```bash
git remote add origin git@github.com:xxx/hexo.git
git remote -v

```

显示如下：
```bash
origin git@github.com:XXX/hexo.git (fetch)
origin git@github.com:XXX/hexo.git (push)
```
####在旧终端中提交本地文件至远程repo
```bash
git push -u origin master
```
换了终端以后

在新终端中安装node、git环境，配置github sshkey

####在新终端中创建空目录作为hexo工作目录，从远程仓库中clone出之前备份的repo
```bash
mkdir hexo
cd hexo
git init
git clone git@github.com:xxx/hexo.git
```
####在新终端中git clone成功后，本地出现myhexo文件夹，开始安装hexo环境
```bash
cd hexo
npm install hexo
npm install
npm install hexo-deployer-git
```
####查看本地同步效果，访问localhost:4000
```bash
hexo g
hexo server
```
####在新终端中继续使用和管理hexo

新建文章并修改
```bash
hexo new xxx
```
####提交原始md文件至远程repo
```bash
git status
git add
git commit -m xx
git push
```
发布静态网页
```bash
hexo g -d
```
####切换至旧终端使用hexo

更新网站原始文件
```bash
git pull
hexo g
hexo server
```
测试更新成功后，表明终端顺利切换完成
