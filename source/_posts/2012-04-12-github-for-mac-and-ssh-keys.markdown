---
layout: post
title: "GitHub for Mac and SSH keys"
date: 2012-04-12 03:13
comments: true
categories: github fix
---

折腾 Octopress 的时候安装了 Git, 之前还安装过 GitHub for Mac, 然后创建 SSH Keys 的时候就发现 `~/.ssh/`目录下面有
```
Zhens-MacBook-Pro:~ caozhen$ ls ~/.ssh/
github_rsa				id_rsa
github_rsa.pub			id_rsa.pub
github_rsa.pub_bak-github	known_hosts
github_rsa_bak-github
```
[Github Help](http://help.github.com/mac-set-up-git/ "Help.GitHub - Set Up Git") 上面的指导文章让生成使用的是 `id_rsa` 和 `id_rsa.pub` 这个 key pair, 那么 `github_rsa` 和 `github_rsa.pub` 是做什么的?
<!-- more --> 
经过猜测和 Google 大神的指引, 确定是 GitHub for Mac 傻瓜化的为用户创建的. 话说干嘛不创建个名称一致的... 那么我连接 GitHub 的时候到底是用的哪一个 key pair 呢? 可以用下列命令确定:
```
$ ssh -vT git@github.com
```
在输出里面找到类似
```
...
debug1: Offering RSA public key: /Users/caozhen/.ssh/github_rsa
...
```
说明现在使用的是 `github_rsa` 这个 key.

#问题解决

现在根据 stackoverflow 上的[这篇文章](http://stackoverflow.com/questions/7968656/why-is-a-cap-deploy-giving-permission-denied-publickey "stackoverflow")切换到默认的 `id_rsa`:
```
$ ssh-add -D
```
这个命令的作用是清除 `ssh-agent` 的缓存, 这样就不会优先使用 `github_rsa` 了.  
#后记
写完博客才想到, 如果一直默认使用 `github_rsa` 这个 key 的话, 其它 ssh 服务也会出现问题, 因为我的 VPS 也是使用的 `id_rsa` 这个 key.
