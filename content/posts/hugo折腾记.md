+++
date = '2026-02-22T21:06:19-08:00'
draft = false
title = 'Hugo折腾记'
tags = ['hugo', '折腾']
categories = ['折腾记']
+++

周六突然觉得想折腾独立建博客了，每次博客都是半途而废原因有：

- 博客大巴死了
- wordpress太难用，模块太复杂
- 没有ai老师帮忙折腾前端 （对前端仅限react折腾一点lodash和bootstrap），css对我来说绝对是黑魔法

这次大致参考一下发现hugo足够简单易用的，写点东西也算不浪费时间，总比刷SNS好多了不是！

说干就干。

<!--more-->

## GitHub page

这部分没什么难的，github做到了足够的简单直接，打开hugo基本操作就能搞定。用了github action来deploy页面，直接用的现成workflow，除了版本什么都没改，开箱即用。这些年的网络服务真是把我这种除了上班就不想在infra上重复试错的人伺候的太好了。

## cloudflare

都有了GitHub page了又想要更多，于是打起了自己域名的主意。在网上冲浪这么多年，每个平台几乎都要创造一个新身份，不像有些熟人一个id走天下，同时又不想像local朋友同事那样真人出道。因此找个名字作为域名又费了不少力气。最难的部分居然在这里。

最后选了你目前看到这个。然而我现在也做不到手搓红黑树，甚至连crud的实现都快忘了，不考八股文真没必要逐行扫描。同时我经常在游戏里用这个id因为在竞技游戏里我真的很弱，为了示弱我就取个id谐音肉*器。

cloudflare真是大善人，除了域名花了13其余几乎免费可用。拿cloudflare r2当s3存储桶，以后图片上传就靠它了。

在这里其实还花了不少时间考虑怎么压缩，毕竟原图下载又慢又费流量，再精细的图片也没人放大认真看，我又不想每次上传之前跑一次webp压缩，picgo有压缩插件但是几乎都是几年前就不更新了，issue列了一堆，如果有支持webp压缩目前还可用的麻烦告诉我一下。

最后发现有[WebP Cloud Services](https://webp.se)帮忙中转cache，把r2的图片压缩成webp。

![还支持自定义域名](https://webp.rbtreefence.xyz/20260222-image.png)

在picgo的s3插件设置自定义输出url模版就好了
![](https://webp.rbtreefence.xyz/20260222-Untitled.png)

5MB的原图通过webp service大概能压缩到400kb，足够网络快速传输了，而且这个服务可以fallback，流量超过额度了就跳转回原图。这个博客没什么人看，大概不会有这么一天吧。

## 主题和样式

本以为主题和样式都是开箱即用的，结果发现还是经常不满意，现在用的paper似乎缺少一些分类信息。我当然不会手写html和css了，全靠codex免费教。

目前大概就是显示toc，显示taxonomies，统计字数和阅读时间，上下post这些基本导航功能。

明明什么还没写呢，一看时间就半夜一点多了。

目前对paper这个主题不算特别满意，doc写的太少了，很多功能需要自己补上，当然也许有违主题原本的极简目标。

接下来还想要

- [x] 支持评论功能，~~我挺讨厌 disqus 的，现在用的浏览器默认屏蔽 disqus 元素，其他的评论系统几乎都要自建服务，稍微有点重，还要承担维护功能。也许等到有人真的开始看了再实践也不错~~ （Feb 24：完成了）
- [ ] 搜索
- [ ] 访客统计
- [ ] 联动豆瓣书影音记录

当然最重要的还是文章本身，花13刀一年用来碎碎念其实性价比不错。vscode写中文md文章似乎不怎么舒服，更喜欢在obsidian上写了再copy过来，略微折腾，得想想有没有什么自动化的同步方式。

这就是我这个周末的side project，如果你真的看到了这里，感谢你作为早期读者。

## 参考资料

- 从零开始搭建你的免费图床系统 （Cloudflare R2 + WebP Cloud + PicGo）<https://sspai.com/post/90170>

- 如何建立写博客的习惯
<https://blog.douchi.space/keep-blogging/#gsc.tab=0>
- 在Netlify上部署Twikoo评论系统
<https://liudon.com/posts/deploy-twikoo-on-netlify/>

[//]: # (Write the rest of the post below.)
