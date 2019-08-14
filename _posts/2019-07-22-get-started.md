---
layout: post
title:  "使用Github和Jekyll制作静态主页"
date:   2019-07-22 10:25:00 +0800
author: 西伯利亚虎
categories: technical
---
本主页使用[Github](https://github.com/)和[Jekyll](https://jekyllrb.com/)制作。

Jekyll是Ruby的一个Gem。Ruby是一种编程语言，而Gem是Ruby库的意思。Ruby词义为红宝石，Gem词义为经切割、磨光后的宝石，二者的关系亦由词义暗示。

以Ubuntu系统为例说明主页的本地搭建。运行`ruby -v`可查看安装的Ruby版本，间接判断是否已安装Ruby。在已安装Ruby的情况下，只需在终端中输入以下4行代码即可建立主页。
```
gem install jekyll bundler
jekyll new myblog
cd myblog
bundler exec jekyll serve
```
其中`jekyll new myblog`一步可能用时较久，耐心等待即可。

新建主页默认使用的Jekyll主题是minima。查看主题文件使用命令`bundle show minima`。
现在我们对minima主题作一些修改。

## 增加访问统计功能

使用[不蒜子](http://ibruce.info/2015/04/04/busuanzi/)。首先将`busuanzi.js`添加到`_includes/head.html`中：
```html
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
```
再在需要显示的位置，插入站点计数
```html
<span id="busuanzi_container_site_pv">
    点击n篇文章计n次的访问量<span id="busuanzi_value_site_pv"></span>次
</span>
```
```html
<span id="busuanzi_container_site_uv">
  点击n篇文章计1次的访客数<span id="busuanzi_value_site_uv"></span>人次
</span>
```
和单页计数
```html
<span id="busuanzi_container_page_pv">
  浏览数<span id="busuanzi_value_page_pv"></span>次
</span>
```

## 增加评论功能
使用[Utterances](https://utteranc.es/)。Utterances基于Github Issues，不依赖第三方网站。首先在自己网页的Github仓库下安装[utterances app](https://github.com/apps/utterances)，随后，在需要放置评论处插入
```html
<script src="https://utteranc.es/client.js"
        repo="[ENTER REPO HERE]"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
```
评论者需通过Github OAuth授权给Utterances来代替他们发布Github Issues。
