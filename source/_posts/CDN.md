---
title: CDN加速
img: /medias/featureimages/12.jpg
top: false
cover: false
toc: true
mathjax: true
date: 2020-09-21 21:46:18
password:
summary: 配置Cloudflare，使用免费CDN加速网站的访问
tags:
- 工具
- 博客
categories:
- 环境搭建
---
<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=22692292&auto=1&height=66"></iframe></div>

>总结下使用免费CDN加速网站访问的过程👀。

由于本博客部署在GitHub上，而GitHub服务器部署在海外。因此在国内访问本博客速度较慢，特别是网络拥挤时，延迟更高。为改善这一情况，决定使用CDN加速博客的访问。

# 简介
---
## CDN
>内容分发网络（英语：Content Delivery Network或Content Distribution Network，缩写：CDN）是指一种透过互联网互相连接的电脑网络系统，利用最靠近每位用户的服务器，更快、更可靠地将音乐、图片、影片、应用程序及其他文件发送给用户，来提供高性能、可扩展性及低成本的网络内容传递给用户。
><p align="right">——维基百科</p>

简单来说，CDN 就是部署在世界各地的缓存服务器，它们会提前缓存网站上的资源，然后当用户想要访问相关资源时，直接从 CDN 服务器上取就可以了。这样不仅可以增加访问速度减少访问延迟，还可以减缓网站服务器上的压力。

世界上的 CDN 服务提供商有很多，七牛云、阿里云、腾讯云等等都提供了 CDN 服务，它们有的收费有的部分免费。我今天选择的 CDN 服务来自于 Cloudflare。
## Cloudflare

[Cloudflare](https://dash.cloudflare.com/)是全球最大的 DNS 服务提供商之一，号称是全球最快的 DNS 1.1.1.1 就是它们搞的。除此之外他们还提供 CDN、SSL 证书、DDos 保护等服务，并且 Cloudflare 与百度有合作，在国内也部署有大量的节点，还能顺便解决百度爬无法抓取 `GitHub` 的问题。我今天要使用的就是免费版的 SSL 证书以及 CDN 服务。

除了 `Cloudflare` 比较 NB 以外选择他的另一个更重要的原因是国内的 CDN 无一例外都要要求域名在公安局备过案。作为一个遵纪守法的好市民，我肯定是不怕什么公安局备案的，我主要是觉得太麻烦了。
# 配置步骤
---
## 站点添加

首先去[Cloudflare](https://dash.cloudflare.com/)注册账号。选择添加站点
![](1.png)
![](2.png)
然后`CF`会要求将你的 DNS 服务器替换为它提供的，接着去域名商处设置一下。 DNS 更新完之后`CF`会发送邮件通知。接着就能配置CDN加速了。
![](3.png)
![](4.png)

## CDN加速配置
设置完 DNS 后，将代理状态设置为已代理就行。此时`CDN`加速就已经开启了
![](5.png)
