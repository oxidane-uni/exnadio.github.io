---
title: 使用Hugo Stack主题对博客的重建与主题优化记录
date: 2023-04-22T14:56:05+08:00
draft: false
description:
image:
comments: true
categories: ["手册"]
tags: ["hugo"]
---

## 为何再次重建博客？  
是，我知道我上次更新博客是2021年，但是这个博客我的确是没有忘的。~~（主播只是入狱了）~~  
实际上这个博客是我在21年暑假用Hugo建的，使用的是Eureka主题。整体效果确实非常不错，但遗憾的是配置过程及其奇怪：虽说有专门的[说明文档](https://www.wangchucheng.com/zh/docs/hugo-eureka/),但是于我而言这玩意写得实在是不太友好~~太坏了，准备写邮件去骂.jpg~~，所以当时我的配置过程纯粹靠蒙，虽说最后还是搞出来了，但确实是一种折磨。  
正好最近几天又想写博客了，就把Hugo又下了回来，结果升级Eureka主题的时候又折磨了好久，还是没整明白。

> 使用git submodule下来的Eureka配置后存在的大量报错，不断提示module未定义，反正也看不懂，干脆换主题了。  
  
因此本次的折腾就再走一遍之前的路，从零开始重建博客，顺带记录下以防之后忘记。  

## Hugo之安装
> “Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。 ” 

本次我使用的是Hugo v0.111.2与git v2.38.0，操作系统为win 11。在Hugo的[releases](https://github.com/gohugoio/hugo/releases)和Git的[官网](https://git-scm.com/)都能很方便地下载。我选择的是hugo_extended_0.111.2_windows-amd64.zip
版本，以便后续折腾。下载完成后将压缩包里的东西解压至你喜欢的目录，再将该目录的路径添加到环境变量中以便后续调用。至于Git的安装，我就不再赘述了。
![PATH]()  

## Hugo基本命令

### 新建网站
运行Hugo.exe后，输入:  
`hugo new site ./path   #比如我这里就是./exnadio.github.io `  
运行后便会输出一个网站目录，其结构为（引用自[炸鸡人博客](https://zhajiman.github.io/post/rebuild_blog)）：
```
.
├── archetypes      # 存放文章模板
├── config.toml     # 简单的配置文件
├── content         # 存放文章
├── data            # 存放生成静态页面时的配置文件
├── layouts         # 存放页面布局的模板
├── static          # 存放图片等静态内容
└── themes          # 存放下载的主题
```
此时便搭好了一个基础框架，可以进行主题的导入了。

### 导入主题  
这一步你就可以打开[Hugo Themes](https://themes.gohugo.io/)这个网站，选择一个你喜欢的主题，然后跟随着它的说明一步一步配置就大功告成了。~~那么我们下期再见~~  
实际上我认为这步是整个Hugo建站中最复杂的一步。且每个人选择的主题不尽相同，很难以一个完善的教程（何况我这篇是否算教程也有待考虑）通杀一切，我就分享下我这次的经历好了。
安装主题一般而言存在三种方式：  
- git submodule 安装
- go module 安装（需要安装Go语言）
- 本地安装

我个人更推荐第一种方式，考虑到后续升级的难易，这算是最均衡的一种方式。具体的安装方法可以在各主题的说明中找到，我这里安装的是[Stack](https://stack.jimmycai.com/)。 
在网站目录下，输入： 
```
git init
git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
```  
等待下载完成后，便可以进行配置了。假如你想用其他方式安装，也可以参考[这里](https://stack.jimmycai.com/guide/getting-started)。  
Stack本身有全英文的[说明文档](https://stack.jimmycai.com/config/)，我建议是将`./themes/hugo-theme-stack/exampleSite/content`和`./themes/hugo-theme-stack/config.yaml`直接夺舍，根据说明与需求修改，会剩下很多时间。  
> 根据Stack的说明文档，Stack后续改用.toml格式，其配置步骤基本相同。 

### 预览网站  
很多教程会先教创建文章，不过我觉得配置完主题后还是先预览网站为好。Hugo的一大好处就是可以进行即时预览，你可以看到你每一步修改所产生的变化，也可以看到你是如何把一切搞崩溃的。
输入:  
`hugo server`  
即可建立一个本地服务器。  
![Hugo server]()  
当然你也可以加上一些flag来达到一些其他目的：比如指定主题的`--theme=Stack`和关闭快速渲染的`--disableFastRender`等，具体可以查阅文档。  
之后便可以在浏览器里打开`http://localhost:1313`预览。

### 创建文章  
Hugo中的文章采用Markdown格式，通过以下命令你可以在`./content/post`路径下创建一篇文章：
`hugo new post/rebuild_blog.md`
打开后你会发现生成的Markdown文档带有一段FrontMatter部分，具体的意思可以在[这里]()找到。大体上可以认为是文档的一些属性。[!]()
虽然大部分的主题都会帮你配置好FrontMatter部分，但是也是有部分主题是需要自行配置的，很不幸，Stack就是这类主题之一。不过这也没啥关系，修改之前提到的`./archetypes/default.md/`下的`default.md`即可。

### 

## Stack主题自定义  
首先放一下对比图：  
![lightmode_default]()    
![lightmode_modified]()  

### 改善浅色模式可读性
配置完Stack后，我并不是很满意，假如说满分100的话我只能打个70分左右。最大的不满在于其浅色模式下可读性实在是过于糟糕,你可以在[Demo网站](https://demo.stack.jimmycai.com/)上感受一下，我不清楚为什么作者采用了`#bababa`这个颜色，导致其与背景的对比度来到了可怜的1.94，简直就是一场彻头彻尾的灾难。  
不过好在Stack主题预留了自定义的空间，详见[官网的说明]()。这里具体介绍下自定义的方法：  
在Stack以及很多主题中，主题文件夹下的`assets/scss`下都提供了一个供用户自定义的`custom.scss`文件。  
> 原理便是在最后引入这个文件，使其位于最终css文件的末尾，从而覆盖原先的属性，达到“自定义”的效果。  

因此，想要自定义就很简单了：找到你希望修改的元素和它对应的选择器，重新定义这个选择器即可。  
万幸，目前的浏览器为我们提供了好用的开发者工具。以我现在使用的Edge为例，按下`F12`弹出开发者工具，使用左上角的小箭头使你的鼠标变成一个查看器(你也可以使用`SHIFT`+`CTRL`+`C`的组合键)，只要将光标置于你想修改的元素上，就能找到该元素的源代码。  
例如我现在想改浅色模式下的文本颜色，只需选择一段文本,就能在右下角看到它对应的css:  
![选择元素]()  
![文本对应css]()  
可以看到文本被指定为`--accent-color`。  
再顺藤摸瓜找到对应的颜色控制：  
![颜色css]()  
把要修改的部分直接复制出来放进`custonm.scss`文件中，修改下即可。比如我使用的就是一套volvo色：
```
:root {
  --body-background: #EBEBEB;
  --accent-color: #1B365D;
  --accent-color-darker: #202A44;
  --accent-color-text: #FFF;
  --body-text-color: #202A44;
}

:root {
  --card-background: #FFF;
  --card-background-selected: #EBEBEB;
  --card-text-color-main: #202A44;
  --card-text-color-secondary: #53565A;
  --card-text-color-tertiary: #888B8D
}
```  
此时就能达到这种效果了：  
![lightmode_modified]()  

### 修改网站布局  
原先挤满所有空间的布局我不喜欢，遂改。
这里使用[仙贝的代码](https://xrg.fj.cn/p/hugo-stack%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%96%B0%E5%B0%8F%E8%AE%B0/#%E4%B8%BB%E9%A1%B5%E5%B8%83%E5%B1%80)，一样是在`custom.scss`中添加：
```
.container {
    margin-left: auto;
    margin-right: auto;

    &.extended {
        /* range: 768-1024 */
        @include respond(md) {
            max-width: 1024px;
            --left-sidebar-max-width: 25%;
            --right-sidebar-max-width: 30%;
        }

        /* range: 1024-1280 */
        @include respond(lg) {
            max-width: 1280px;
            --left-sidebar-max-width: 25%;
            --right-sidebar-max-width: 22%;
        }
    }

    &.compact {
        @include respond(md) {
            --left-sidebar-max-width: 25%;
            max-width: 768px;
        }

        @include respond(lg) {
            max-width: 1024px;
            --left-sidebar-max-width: 20%;
        }

        @include respond(xl) {
            max-width: 1280px;
        }
    }
}
```  
即可。

### ~~老头~~滚动条修改  
同上，不喜欢，[仙贝代码](https://xrg.fj.cn/p/hugo-stack%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%96%B0%E5%B0%8F%E8%AE%B0/#%E6%BB%9A%E5%8A%A8%E6%9D%A1%E7%BE%8E%E5%8C%96)，添加：  
```
html{
    ::-webkit-scrollbar {
        width: 20px;
      }
      
      ::-webkit-scrollbar-track {
        background-color: transparent;
      }
      
      ::-webkit-scrollbar-thumb {
        background-color: #d6dee1;
        border-radius: 20px;
        border: 6px solid transparent;
        background-clip: content-box;
      }
      
      ::-webkit-scrollbar-thumb:hover {
        background-color: #a8bbbf;
      }
}
```

### 图标添加  
Stack主题带了几个很好看的Tabler图标，可惜并不全，部分缺失的图标要手动添加。  
例如我想添加一个比比汗丽丽的图标，在[Tabler官网](https://tabler-icons.io/)搜索发现居然真有：  
![搜索结果]()  
将svg文件其下载到主题中的`.assets\icons`中调用即可。  

## 目前仍未完成的部分  
当然目前这个网站仍存在以下问题：  
1. 过往文章未恢复  
2. 评论系统未接入  
3. 部分界面还未完全配置好 
4. 网站图标未设置（其实是还没做） 
以上，下次必然一定修复！  

![预告]()
## 真实配置过程  
