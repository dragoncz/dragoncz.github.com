---
layout: post
title: "Update Octopress"
date: 2012-12-08 00:18
comments: true
categories: octopress 
---

最近一直在学习 iOS Programming，博客好久没更新了啊，再不更新荒废了。。。但是，作为不折腾会死星人，更新博客之前，先把 Blog Engine 更新了才对。

# Octopress
[Octopress][] 不比 Wordpress 等动态引擎，是纯静态并且没有后台的，想点击 `Update` 按钮一键更新是不可能的，一切都要在终端里进行。当然，这样也会强迫你每次使用都学到新东西，尤其像我这样的新手。  

由于 Octopress 本质上只是一个 `Generator`，生成器，根据你的博客源文件（像是文章，CSS，Javascript 等等各种资源）生成静态网页。那么更新 Octopress 实质上就是更新这个生成器，它一般存在与你自己的电脑或远程服务器上，这个和保存网站本身的服务器一般是两个不同的位置。
<!-- more -->
## Update
根据 Octopress 官网的 [指示](http://octopress.org/docs/updating/)，打开终端，进入你 Octopress 的目录，然后依次输入以下命令就可以更新了：
```
git pull octopress master     # Get the latest Octopress
bundle install                # Keep gems updated
rake update_source            # update the template's source
rake update_style             # update the template's style
```
解释一下，由于当时安装 Octopress 是使用的 `git Clone` 命令，那么本地存在的 Octopress 自然可以使用 `git pull` 来获取最新版本。第一行命令就是获取 Octopress 最新版本并与本地 branch 合并。  

如果你像我一样水，从来没对本地 git branch 进行过 `commit` 和 `push` 操作的话，以上命令是拯救不了你的，而且多半第一行会报错。俗话说，「亡羊补牢，犹未为晚」，在输入上述命令之前，先进行下 `commit` 和 `push`：
```
git add .
git commit -m 'source files archive'
git push origin source
```
好了，现在再输入那四行命令就可以更新了。

## 关于主题
由于我之前安装了 [`Slash`][] 这款主题，所以第三行和第四行的命令要稍微更改一下，不然主题会全乱了，如果你发现已经乱了，还是那句话，「亡羊补牢，犹未为晚」，再执行一边下面的命令就好了：
```
rake update_source['slash']     # replace 'slash' with your theme name
rake update_style['slash']      # replace 'slash' with your theme name
```

## 测试
```
rake preview
```
然后打开浏览器，访问 [127.0.0.1:4000](http://127.0.0.1:4000) 就可以看到效果了。看完效果别忘了回到终端 `Ctrl + C` 停止 Preview 进程。

[Octopress]: http://octopress.org "Octopress.org"
[Slash]: http://zespia.tw/Octopress-Theme-Slash/ "Slash for Octopress"