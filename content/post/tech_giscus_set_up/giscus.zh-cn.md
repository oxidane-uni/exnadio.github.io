---
title: 将博客评论系统由 utterance 迁移至 giscus
date: 2023-11-18T17:20:26+08:00
description: "评论系统配置及迁移记录"
image: ./images/4featureimg/giscus.jpg
comments: true
math: true
categories: 
  - 技术
tags:
  - giscus
draft: false
---

## 前言

之前建博客的时候没听说过giscus，使用的是utterance。

不过看起来giscus的功能相对更优，而且之前配置博客时没有进行相应的记录，因此干脆直接换成giscus了。

**这里需要感谢[@chuxinyuan](https://github.com/chuxinyuan)大佬在评论区的建议**

## giscus是什么？

这里就直接全文摘抄[官网](https://giscus.app)的简介了，说得很明白：

> 利用 GitHub Discussions 实现的评论系统，让访客借助 GitHub 在你的网站上留下评论和反应吧！本项目深受 utterances 的启发。

相较于使用 issue 的 utterance，使用 discussion 的 gisus 在功能上更为丰富，详见[
GitHub Discussions 快速入门](https://docs.github.com/zh/discussions/quickstart)（而且 utterance 把评论全放在 issue 里也怪怪的）。

## 配置giscus

giscus的配置还是相当简单的。

首先，准备一个github仓库，这里我用的是原先utterance的仓库。

接下来在仓库的设置界面开启 Discussions 功能：  

![开启discussion](./images/4post/231119/discussion.png)

接下来的操作就是相当简单且无脑了，你需要做的就是在 github 上安装 [giscus APP](https://github.com/apps/giscus)  

![安装界面](./images/4post/231119/installation.png)  

具体的安装过程不再赘述，安装完毕后就只需打开[giscus官网](https://giscus.app)，输入具体的仓库名称（或者仓库链接）：  

![输入界面](./images/4post/231119/input.png)

若该仓库可用，那么就可以随着官网的说明一步步配置下去。配置完成后便可在 **启用 giscus** 下找到需要的代码：  

![代码示例](./images/4post/231119/demo.png)

之后的过程依主题的不同而不同，请参考各自的主题说明文档。

我使用的是Hugo的stack主题，需要在 `config.yaml` 中设置：
```
comments:
  enabled: true
  provider: giscus

```
之后再在giscus那栏中填入官网代码中的相应内容即可。


当然`config.yaml`中缺少了部分选项，你也可以直接将需要的js代码放进`./themes/hugo-theme-stack/layouts/partials/comments/provider/giscus.html`里：  

![文件界面](./images/4post/231119/html.png)

至此便配置完成，可以说是相当简单的。

还有一些高级用法，请自行参考官网对应说明。


## 迁移utterance评论

utterance 之类使用 Github issue 实现的评论系统的内容是可以转换为相应的 discussion的，详见[将议题转换为讨论](https://docs.github.com/zh/discussions/managing-discussions-for-your-community/moderating-discussions#converting-an-issue-to-a-discussion)

只需在相应库的 issues 界面的 labels 处将相应 label 转换为 discussion 即可（假如没标注的话请自行添加）。  

![转换界面](./images/4post/231119/convert.png)

转换完成后，若 discussion 标题与页面的映射关系正确，那么 giscus 就可以展示这些评论，迁移结束。


## 参考链接
[giscus](https://giscus.app)

[迁移博客评论系统从Utteranc.es到Giscus](https://agou-ops.cn/post/%E8%BF%81%E7%A7%BB%E5%8D%9A%E5%AE%A2%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F%E5%88%B0giscus)