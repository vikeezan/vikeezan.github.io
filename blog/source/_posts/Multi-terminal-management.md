---
title: Hexo多终端管理的搭建流程
date: 2019-03-27 19:08:28
tags:
	- hexo
	- 多终端搭建
categories: 建站填坑
---
## 1.原理介绍
多终端管理的基本思路是将博客在Github网站上分为两个分支来管理：
- 一个是master主分支用于存放博客的静态网站文件（`hexo server`之后会在本地文件里生成public文件夹，public文件夹内是根据.md生成的html静态网站文件），我们在电脑上更新完博客之后可以`hexo deploy`到该分支上，平时点进你的网站[https://username.github.io/](https://username.github.io/)时看到的内容就是这个分支解析出来的。
<!--more-->
- 另一个分支则是hexo副分支（自己起的名字，可以更改），这个分支的作用是保存博客的最新版本，在不同的电脑上pull并新建博客后，push到这个分支上，这样随时都可以找到博客的最新版本，该分支上的更改如果不经过`hexo deploy`，不会影响到master主分支上的内容。

**PS：个人建议之前没有接触过git的同学可以先看一下有关git的基础教程，因为没接触过git的同学瞎用指令会把网站搞崩的，别问我为啥知道...这里推荐廖雪峰的课**[廖雪峰git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## 2.搭建流程
1.创建仓库，[https://username.github.io/](https://username.github.io/)。其中的**username**要由你自己定义，要和你Github注册的用户名保持一致;
2.创建两个分支，master和hexo。这一步不用手动创建，后面有指令会自动创建hexo分支的；
3.设置hexo为默认分支。因为我们只需要手动管理这个分支上的网站文件，设置方法为项目右上角setting里的branch选项卡，将其中的默认分支更改为hexo即可；
4.在第二台电脑上使用git clone git@github.com:username/username.github.io.git拷贝仓库；
5.在本地的与Github相连的[https://username.github.io/](https://username.github.io/)文件夹下右键使用Git Bash依次执行`npm install -g hexo-cli `安装hexo、`hexo init`初始化hexo、`npm install hexo-deployer-git --save`让hexo知道你要把blog部署在哪一个位置。这三条指令完成后当前分支应显示为hexo；
6.修改博客站点配置文件`_config.yml`中的deploy参数，将branch的参数改为master；
7.依次执行`git add .`添加所有文件到缓存区、`git commit -m “…”`提交缓存区的文件同时增添备注、`git push origin hexo`将更改的内容push到github的hexo分支进行备份；
8.执行`hexo g -d`生成网站并部署到Github上。
经过以上操作之后，我们的master分支用于存放网站的静态文件，hexo分支用于存放网站的原始文件，井水不犯河水，简直太完美了有没有！
### 2.1第一个终端的hexo分支
在一开始创建博客的电脑上，将本地blog文件夹内必要的hexo文件push到username.github.io的hexo分支上，具体操作如下：
```
git init  //初始化本地仓库
git add source //将必要的文件依次添加，有些文件夹如npm install产生的node_modules由于路径过长不好处理，所以这里没有用`git add .`命令了，而是依次添加必要文件,例如source themes scaffolds _config.yml package.json package-lock.json等。
git commit -m "Blog Source Hexo" //备注这是blog网站最原始的文件
git branch hexo  //新建hexo分支
git checkout hexo  //切换到hexo分支上
git remote add origin git@github.com:yourname/yourname.github.io.git  //将本地与Github项目对接
git push origin hexo  //push到Github项目的hexo分支上
```
### 2.2另一终端完成clone复制以及push更新
在另一个终端更新博客，只需要将Github的hexo分支上的内容克隆到本地，然后再对其进行更改和push更新，具体操作如下：
```
git clone -b hexo git@github.com:yourname/yourname.github.io.git  //将Github中hexo分支clone到本地
cd  yourname.github.io  //切换到刚刚clone的文件夹内
npm install -g hexo-cli    //注意！一定要切换到刚刚clone的文件夹内执行，安装hexo
npm install hexo-deployer-git --save //让hexo知道你要把blog部署在哪一个位置
hexo new post "new blog name"   //新建博客并编辑内容
git add source  //经测试每次只要更新source中的文件到Github中即可，因为只是新建了一篇新博客
git commit -m "XX" //对本次修改进行备注
git push origin hexo  //将当前终端的文件更新到Github上的hexo分支上
hexo d -g   //将自己写的博客部署到自己的博客网站上，同时同步Github中的master分支
```
## 3.日常的修改流程
先对本地的博客进行修改，例如增加博客，更改样式等，再将新的内容push到Github的hexo分支上，哭啼的操作如下：
```
git pull origin hexo  //先pull云端的hexo分支文件，完成本地与远端的融合
hexo new post " new blog name" //新建博客并编辑内容
git add source
git commit -m "XX"
git push origin hexo
hexo d -g
```

本文的参考链接：[https://blog.csdn.net/ZmeiXuan/article/details/78339376](https://blog.csdn.net/ZmeiXuan/article/details/78339376)