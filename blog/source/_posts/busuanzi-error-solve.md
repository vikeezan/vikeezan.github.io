---
title: Hexo博客next主题下不蒜子busuanzi访问量统计不显示
date: 2019-03-27 10:51:54
tags:
  - 分享
  - hexo
  - next
categories: 建站填坑
---
首先明确在hexo博客的主题配置时，有两个文件经常会用到。一个是blog根目录下的`_config.yml`文件，我们称其为**站点配置文件**，另一个则是`themes\next`下的`_config.yml`文件，我们称其为**主题配置文件**，在主题配置文件内next本身已自集成了一个统计算法，具体的用法如下:
<!--more-->

打开**主题配置文件**，建议用Sublime Text打开，可以使用`ctrl+f`快捷键，输入`busuanzi`,你会看到以下代码:（V5版本)
```
busuanzi_count:
  # count values only if the other configs are false
  enable: false
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i> 
  site_uv_footer: 
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i>
  site_pv_footer: 
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-file-o"></i>
  page_pv_footer: ```
（v7版本）
```
busuanzi_count:
  enable: false
  total_visitors: true
  total_visitors_icon: user
  total_views: true
  total_views_icon: eye
  post_views: true
  post_views_icon: eye```
两个版本的算法虽然在具体细节上有所不同，但总的来说大同小异，使用方法都是将`enable: false`语句更改为`enable: true`，改完之后就可以在网站底部看到浏览量已经显示出来了。

这时v5版本的用户可能会发现浏览量依旧显示不出来，打开控制台查看发现是因为`不蒜子`的js文件找不到所以出错了，据`不蒜子`的作者[不蒜子官方网站](http://ibruce.info/2015/04/04/busuanzi/)介绍是原先的域名失效了，所以不得已更换了新的域名。所以现在我们要在js文件里重新引用一下，接下来是解决方法：

简单来讲就是将`next`主题下`不蒜子`的js引用文件更改一下即可。我们首先进去blog根目录下的`themes`文件夹，找到我们在用的`next`主题文件夹，然后在`\layout\_third-party\analytics`下找到`busuanzi-counter.swig`文件，右击用sublime text打开，在该文件下找到如下语句：
```
<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```
将这句话更改为：
```
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
```
然后再刷新下页面，就大功告成啦~总的来说解决问题的方法不难，不过不清楚门道的话不知道怎么改，反正我折腾了很久就是了
### 祝大家建站快乐，少遇坑~
