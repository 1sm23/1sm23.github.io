---
title: 提交pull request
date: 2020-03-22 01:28:11
categories:
- git
tags:
- git 
- github
- pull request
---

公司有用到腾讯云的[TIC](https://github.com/tencentyun/TIC) PasS服务，TIC全称腾讯云互动课堂在线教育解决方案，就是一个白板加上IM功能，在小程序端里其中的白板组件board-component使用起来体验极其不好，画笔垂直绘画的时候很大几率会引起页面滚动，在小程序社区找到解决问题的办法后我有了提pull request的想法。

<!--more-->

首先fork一份到自己的仓库



然后clone自己的fork到本地

```bash
git clone yourforkrepo
```



作出修改后

```bash
git add .
git commit -m ''
git push origin master
```



最后在自己的仓库上方点击Pull request , New pull request，作出评论即可啦

![](https://tva1.sinaimg.cn/large/00831rSTgy1gd22scz3dcj31ex0u0jxd.jpg)

