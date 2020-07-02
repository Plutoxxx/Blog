---
title: Windows Terminal配置
top: false
cover: false
toc: true
mathjax: true
date: 2020-06-30 20:15:24
password:
summary: 推荐一下Windows自家推出的终端软件😍。
tags:
- Windows Terminal
- 工具
categories:
- 软件
---
<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=27583241&auto=1&height=66"></iframe></div>

>推荐一下Windows自家推出的终端软件😍。

`Windows Terminal`是微软发布的一款终端（简称WT）。与传统的`cmd`、`Powershell`相比，WT对定制的支持更好，同时又支持GPU对页面的渲染、emoji表情、多标签等的特点。[项目地址](https://github.com/microsoft/terminal)

由于WT的可定制化非常之高，只需要很简单的步骤就可以调节各种界面元素以及操作习惯，所以把它打造成最适合自己的Windows终端程序是完全做得到的。

![](1.png)

# 安装WT
---
在`Microsoft store`中搜素`Windows Terminal`安装即可。
![](2.png)

# 美化配置
---
## 安装oh-my-posh
1. 安装`scoop`
首先在`Powershell`中输入以下代码来保证允许本地脚本的执行：
```Powershell
set-executionpolicy remotesigned -scope currentuser
```
然后安装`scoop`：
```Powershell
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```
2. 更换字体
`Powerline`字体有很多种，这里使用了[Fira Code](https://github.com/tonsky/FiraCode/releases)，下载后安装即可。
3. 安装`choco`
```Powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
4. 安装`ConEmu`
```Powershell
choco install ConEmu
```
5. 安装`posh-git`、`oh-my-posh`和`Get-ChildItemColor`
前两个是`oh-my-posh`的必备组件，最后一个是美化`ls`命令的显示效果的插件，可以选装。
```Powershell
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
Install-Module -AllowClobber Get-ChildItemColor
```
6. 设置`Powershell`的`profile`
```Powershell
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
```
7. 打开上步创建的$PROFILE文件并粘贴以下内容
```Powershell
Import-Module posh-git
Import-Module oh-my-posh
Import-Module Get-ChildItemColor
Set-Theme Paradox
# Chocolatey profile
$ChocolateyProfile = "$env:ChocolateyInstall\helpers\chocolateyProfile.psm1"
if (Test-Path($ChocolateyProfile)) {
  Import-Module "$ChocolateyProfile"
}
```
至此，`oh-my-posh`的安装就完成了，打开`WT`的效果如下：
![](3.png)


## 定制settings.json
1. 打开设置，在`defaultProfile`中配置默认打开的终端程序。`copyOnSelect`选择`true`时可以右击实现`复制+粘贴`的功能。

2. 在`profiles`的中，可以单独为不同程序进行自定义设置。
    * 首先是毛玻璃效果，这个需要调节两个参数，第一个是把`useAcrylic`设置为`true`，这是必须的，第二个`acrylicOpacity`则是调节毛玻璃的透明度，取值范围为0-1，0为完全透明，1为完全不透明。
    
    * `fontFace`是设置字体，使用的是`font Face`属性，只需要把字体名称填入进去就可以了。如果没有这个字体，则自动替换成`Consolas`。除此之外还可以调节字体大小，使用的是`fontSize`属性。
    
    * `background`属性可以设置背景颜色，`backgroundImage`则可以设置背景图片。注意：`backgroundImage`在毛玻璃特效打开时不起作用。

    * `cursorColor`用于设置闪动的光标颜色，`cursorShape`则可以调节光标的样式。

    * `commandLine`属性的值为命令行程序的路径，如`cmd`的路径为`cmd.exe`，`Git Bash`的路径为`/Git/bin/bash.exe`等。对应的也可以设置程序的图标和标题名，对应属性为`icon`和`name`。

    * 关于`colorScheme`属性，这个属性用于修改配色方案，默认9种，可以在[官网](https://docs.microsoft.com/zh-cn/windows/terminal/customize-settings/color-schemes)中找到。当然也可以自己定义新的配色方案，在schemes中添加。更多的配色方案可以在[此处](https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/windowsterminal)找到

大功告成，来张效果图：
![](4.png)
# 功能配置
---
## 将WT添加到右键
1. 在Powershall中测试以下两个常量是否正常，若没有报错则继续
```Powershall
echo %USERPROFILE%
echo %LOCALAPPDATA%
```

2. 在Powshall行中执行以下命令：
```Powershall
mkdir "%USERPROFILE%\AppData\Local\terminal"
``` 

3. 将windows Terminal图标复制到`%USERPROFILE%\AppData\Local\terminal`文件夹中。图片自取：
![](terminal.ico)
3. 将下列代码复制保存为.reg注册表文件（WT的路径中用户名可能会不同需要修改），然后双击导入注册表即可。

```Powershall
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt]
@="Windows terminal here"
"Icon"="%USERPROFILE%\\AppData\\Local\\Terminal\\terminal.ico"
[HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command]
@="C:\\Users\\[用户名]\\AppData\\Local\\Microsoft\\WindowsApps\\wt.exe"
```
4. 检查Windows Terminal配置文件中是否有`startingDirectory `属性，若没有则将其添加为
```json
"startingDirectory": "."
```

5. 若出现错误，可能是用户名为中文导致出错。建议打开注册表编辑器，检查`HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command`这个路径下的配置是否和文件配置的一样。

6. 效果图：
![](5.png)

## 添加Git