---
title: 关于喜提gfw认证这件事
date: 2021-04-25 19:02:04
hidden: true
tags:
- gfw
- 防火长城
- the great firewall
- bandwagonhost
- v2ray
categories:
- 闲言碎语
---

​		这个博客部署的服务器是搬瓦工的19.9cn2套餐，上面有个v2ray服务，2021年3月一天早上起来v2ray就异常了，上搬瓦工自带的检测工具一测试，果然是IP被ban了，等于这个博客也被连坐，还好hexo deploy配置里同样加了[github pages](https://1sm23.github.io)虽然这样不符合github pages 的原本用途，但现在也只能是权宜之计了。

​		在被ban之后我花了8美刀更换IP，半个小时没到又被封了，发了工单给客服，回复说没有更好的解决办法，

![](https://tva1.sinaimg.cn/large/008i3skNgy1gpwa3gn2d3j30vn0u0gv2.jpg)

<!--more-->

![](https://tva1.sinaimg.cn/large/008i3skNgy1gpwa4ekp81j318k0lw42b.jpg)

只能关掉服务等待gfw自动解封（可能）。之后我就彻底躺平了，关机等待可能的解封。今天突然想到这件事情，重新启动服务，发现还是没解封，但意外的发现用梯子还是可以访问博客内容的，但每次文章更新怎么部署到主机就要下一番功夫了，直接`hexo deploy`现在是不行了，只能每次手动拷贝生成后的`public`文件夹。所以我打算就这样吧，能看到我博客内容的都是和gfw抗争过的战友了，salute！

![](https://tva1.sinaimg.cn/large/008i3skNgy1gpwa55t1cyj30m80ci0tw.jpg)



