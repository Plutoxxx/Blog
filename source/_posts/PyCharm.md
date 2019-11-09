---
title: PyCharm配置远程连接
top: false
cover: false
toc: true
mathjax: true
date: 2019-11-09 13:39:19
password:
summary:
tags:
- PyCharm
- 服务器配置
categories:
- 环境搭建
---

>主要讲解PyCharm远程连接服务器时的相关配置😝。

# 简介
---
基本上我们使用PyCharm都是在本地进行开发，但是当我们需要在服务器上调试代码时咋办呢？一种是将服务器上的程序下载到本地，调试编写完后上传，这种方法可行，但是每次都要上传下载，较为繁琐。另一种方法就是利用PyCharm远程调试代码咯，只需稍稍配置一下就能实现。

# 配置步骤
---
## SFTP配置
打开PyCharm，选择`Tools/Deployment/Configuration`选项
![](1.png)
配置连接服务器
![](2.png)
点击`Test Connection`，显示成功，表明配置正确
![](7.png)
选择文件传输对应的位置
![](3.png)
选择不需要同步的文件
![](4.png)
文件可以手动上传，也可以自动上传
![](10.png)

## Interpreter配置
打开`File/Settings/Project Interpreter`选项，点击`add`
![](5.png)
添加服务器解释器
![](6.png)
选择解释器的位置，以及文件夹的映射关系
![](8.png)
解释器配置完成后就能看到环境下包含的`package`
![](9.png)
此时就能愉快的使用PyCharm进行`DeBug`啦!