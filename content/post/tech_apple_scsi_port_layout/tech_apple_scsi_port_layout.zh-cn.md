---
title: "苹果 PowerBook 48pin SCSI 硬盘接口探究"
date: 2024-07-05T15:33:07+08:00
description: 
image: ./images/4featureimg/6ZMRZKdA2Yf3jfKD.jpg
comments: true
math: true
categories: 
  - 技术
tags:
  - 
draft: false
---

## 前言

在[翻译视频](https://www.bilibili.com/video/av1656008990/)的时候，我对苹果 PowerBook 上的 SCSI 硬盘所采用的接口产生了兴趣。

虽然很多资料明确地指出苹果在 PowerBook 上使用了 SCSI 硬盘，然而其接口形态却明显有别于台式机上的标准 SCSI 接口，关于这个冷门接口似乎并无多少资料，甚至这个接口的名字都找不到。不过幸运的是，我还是找到了一部分介绍，就放在这里做个集合吧。

![a SCSI connector](./images/4post/240718/PCSCSI.png)
> 图为常见的一种 SCSI 接口

![PowerBook connector](./images/4post/240718/CUKVV.jpg)
> 图为苹果在 PowerBook 上所使用的接口。可以看到其排针间距更大，总针脚只有 48pin，同时还没有外置的 Molex 供电接口。

## 介绍

首先是[vintage macmuseum](https://vintagemacmuseum.com/reading-powerbook-2-5-scsi-hard-drives/)上的一篇博文指出，这个接口本身是可以通过一些妙妙操作转接为最为常见的 SCSI 接口的，同时还介绍了几种转接方式。

![Adapter1](./images/4post/240718/PB-SCSI-Adapter1.jpg)
> 你能看到用于供电的 Molex 接口以及转接出来的 SCSI 数据接口

![Adapter2](./images/4post/240718/TDNC.png)
> This Does Not Compute 里使用的转接器

不过真正帮了大忙的是[superuser 上的一个问题](https://superuser.com/questions/1527997/what-is-this-48-pin-laptop-hard-drive-connector#)

![superuser](./images/4post/240718/spur.png)

以及[68kmla上的一个帖子](https://68kmla.org/bb/index.php?threads/40p-scsi-to-50p-scsi.8047/)，甚至连针脚定义图都给了，卧虎藏龙啊。

![68kmla](./images/4post/240718/68kmla.png)

另外，那个帖子里甚至还有人给出了一个 eBay 链接，眼熟。

![ebay](./images/4post/240718/ebay.png)

## 接口布局

回到接口本身。实际上这个接口运行的还是 SCSI 协议，所以其实仅仅在接口的物理形态上有所不同。

就如之前所说，虽然在有时会被描述为“50pin”，但该接口实际只有 48pin，排布如图：

![pinlayout](./images/4post/240718/connector.png)

其中左侧 40pin 部分用于供电与数据传输，右侧 8pin 负责 SCSI ID。

**左侧部分**定义如下：

![40pindef](./images/4post/240718/pdefc.png)

**右侧部分**定义如下：

![8pindef](./images/4post/240718/pdefs.png)

更多的信息，可以参考[这个链接](http://powerbook.micahgartman.com/dev/dn_duo_250.pdf)

所以当我们回过头来看先前所提到的转接板时就能很明显地看出其与通用 SCSI 接口的对应关系。

![Adapter](./images/4post/240718/s-l1600.webp)

![common scsi connector](./images/4post/240718/scsi.jpg)
> 这接口只有 5V，所以其实这里 Molex 只用上了里边的 5V（说实话我还是第一次知道 Molex 里有 5V） 
![molex](./images/4post/240718/molex.png)

## 参考链接

1.[Repairing an Unreleased Prototype Mac...TABLET!_This Does Not Compute](https://www.youtube.com/watch?v=OM64l8tZSwY)

2.[Reading PowerBook 2.5″ SCSI Hard Drives_vintagemacmuseum](https://vintagemacmuseum.com/reading-powerbook-2-5-scsi-hard-drives/)

3.[what is this 48-pin laptop hard drive connector?_superuser](https://superuser.com/questions/1527997/what-is-this-48-pin-laptop-hard-drive-connector#)

4.[40p SCSI to 50p SCSI_68KMLA](https://68kmla.org/bb/index.php?threads/40p-scsi-to-50p-scsi.8047/)

5.[50-Pin IDC 2.54mm Male to 50-Pin IDC 2.00mm Female SCSI Laptop HD Adapter_eBay](https://www.ebay.com/itm/CablesOnline-2-5-Laptop-50-Pin-w-Molex-Power-Cable-to-SCSI-Hard-Drive-Adapter-/270840619638)