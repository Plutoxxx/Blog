---
title: Hexo-Github-Netlify博客搭建教程
<!-- img: https://image-1300514593.cos.ap-shanghai.myqcloud.com/featureimages/0.jpg -->
top: true
cover: true
toc: true
mathjax: true
date: 2019-09-25 08:27:14
password:
summary: 主要讲解本blog的搭建过程😁
tags:
- Hexo 
- GitHub 
- Netlify 
- 博客
categories:
- 环境搭建

---
<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=538882&auto=1&height=66"></iframe></div>

>主要讲解本blog的搭建过程，如有不详之处，可以联系我，或者在下方评论，我都会解答哒😁。

# 我的博客源代码地址
---
大家有需要的可以star&fork我的[博客代码](https://github.com/Plutoxxx/Blog)，修改一些配置就可以写文章了。

# 快速搭建
---
如果你不想重新自定义主题的话，可以直接下载我已经修改过的主题，只要稍微修改一些地方就行：
* 在根目录配置文件_config.yml和themes config.yml中修改个人信息。
* 在/_config.yml中修改deploy下的repository。
* 在/_config.yml中修改baidu_url_submit下的host。
* 在themes/_config.yml中修改gitalk。

**当然在个性化设置前环境要先配置好**

平时常用的命令有：
```java
hexo n "博客名称"  => hexo new "博客名称"   #这两个都是创建新文章，前者是简写模式
hexo p  => hexo publish   
hexo g  => hexo generate  #生成静态网页
hexo s  => hexo server    #启动服务预览
hexo d  => hexo deploy    #部署
hexo clean   #清除缓存，网页正常情况下可以忽略此条命令
ctrl + c     #关闭本地服务器
```

# 安装Node.js
---
首先下载稳定版本[Node.js](https://nodejs.org/en/)。

安装选项默认就行，一路Next。

最后安装好之后，按Win+R打开命令提示符，输入`node -v`和`npm -v`，如果出现版本号，那么就安装成功了。

**添加国内镜像源**

如果没梯子可以使用阿里的国内镜像进行加速
```js
npm config set registry https://registry.npm.taobao.org
```
# 安装Hexo
---
安装完Node.js后，打开终端，输入以下命令：
```hexo
npm install -g hexo-cli
hexo -v  #查看是否安装成功
```
在合适的位置新建文件夹，用来存放blog文件，比如我的博客文件在 F:\Project\GitHub\Blog 目录下。

在该目录下初始化网站，输入 `hexo init` 初始化文件夹，接着输入 `npm install` 安装必要组件。 

到这里，本地网站已经配置结束，输入 `hexo g` 生成静态网页，然后输入 `hexo s` 打开本地服务器，

最后在浏览器中打开: http://localhost:4000/ 就能看到初始化的blog啦。

最后按 `ctrl+c` 就能关闭本地服务器了

# 安装Git和创建GitHub仓储
---
**安装Git**

先到[Git官网](https://git-scm.com/download/win)下载软件。

安装选项还是全部默认，只不过最后一步添加路径时选择Use Git from the Windows Command Prompt，这样我们就可以直接在命令提示符里打开git了。

安装完成后在命令提示符中输入 `git --version` 验证是否安装成功。

**创建GitHub仓储**

到[GitHub](https://github.com)注册一个账号，相信小伙伴们都有吧。然后新建一个项目，如图所示：
![](1.png)

然后设置一下Repository的名字，如图所示，不要勾选下边的 `Initalize this repository with a README`如下图所示，点击完成就行。
![](2.png)

# 本地连接GitHub
---
右击打开 `Git Bash here` ，输入:ssh，如图所示，说明配置好了：
![](3.png)

接着输入 `ssh-keygen -t rsa` （(主要是生成你跟github联系的秘钥key)）连续三个回车，key就生成了。打开C盘用户下的.ssh文件，其中 `id_rsa` 代表私钥， `id_rsa.pub` 代表公钥。

将id_rsa.pub下的内容复制出来，打开GitHub下的Settings
![](4.png)

选择 `SSH and GPG keys` 中的 `New SSH key`粘贴进去就行了
![](5.png)

测试连接 `ssh -T git@github.com`，弹出警告后，填写yes，然后回车，出现以下则表示成功
![](6.png)

在Blog目录下，右击打开Git，输入命令： `git init`，会出现一个 `.git` 文件夹

在项目根目录下,将你的本地项目和新建的repository联系起来:
```git
git remote add origin https://github.com/your-name/your-Repository.git
```
完成后到根目录下：
```git	
git add .                       # 添加文件到暂缓区
git commit -m 'First commit'    # 将刚刚添加到暂缓区的内容提交到本地仓库.git
git push --set-upstream origin master #上传到远程仓库(由于是第一次push,所以是这个命令)
```
到这里,我们已经将我们的项目推送到GitHub的master分支下面了.接下来我们要对hexo进行一些配置:

打开博客根目录下的_config.yml文件，这是博客的配置文件，在这里你可以修改与博客相关的各种信息。
修改最后一行的配置：
```config
deploy:
 type: git #部署方式
 repository: git@github.com:you-name/your-Repository.git #关联github仓库
 branch: run-page #部署分支
```
在这里,我们将在这个项目仓库下新建一个run-page分支,至于有什么用,我等一下解释,先跟着我操作起来.

在当前根目录下将不需要同步的文件和目录写到 `.gitignore` :
```name
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
themes/
.deploy*/
```

配置好了之后,保存退出,我们重新执行一下:
```hexo
$ hexo clean #清理各种缓存和旧文件
$ hexo g     #生成静态文件
```

最后,我们将public目录同步到Github:
```hexo
$ hexo d #部署应用
```

在执行这个命令的时候,我们可能会出现如下错误：
```error
$ ERROR Deployer not found: git
```
那是因为我们缺少一个依赖,我们安装一下:
```npm
npm install hexo-deployer-git --save
```
然后再次执行一下,执行完成我们到Github，神奇的的事发生了，我们的项目多了一个(run-page),这个分支就是我们后面要用来生成我们到静态页面的。

# 部署到Netlify
---
我们先到[Netlify](https://www.netlify.com)官网注册一下账号,因为我们是将项目托管到GitHub的,所以我们选择GitHub登录：
![](7.png)
点击网站新建：
![](8.png)

选择GitHub来源：
![](9.png)

选择刚建的项目：
![](10.png)

进行下一步配置：
![](11.png)

等待一会，Netlify会帮我们生成网站：
![](12.png)

第一次新建的时候,它会随机生成一个Netlify的二级域名,我们可以进行自定义二级域名,点击("Change site name")即可进行设置,像这样：
![](14.png)
![](15.png)

点击Save,等待Netlify进行热部署即可.

然后点击创建好的二级域名,成功访问✌️！！！

以后我们写好博客之后,直接执行：
```hexo
$ hexo clean #清理各种缓存和旧文件
$ hexo g     #生成静态文件
$ hexo s     #在本地查看生成网页（取消用ctrl+c）
$ hexo d     #推送到GitHub
# 写完blog不需要清除缓存，直接生成静态文件即可
```
我们的个人博客就会自动进行刷新,是不是超厉害！！

# 思路
---
部署完成之后,可能有的同学会觉得很晕,我画了一个部署的流程图：
![](13.png)
这就是我们为什么要利用两个分支的原因,我们将我们的项目分支托管到 `master` ,然后将生成的 `public` 目录,托管到 `run-page` 分支,以后我们可以写完博客以后,就可以直接输入：
```hexo
$ hexo clean #清理各种缓存和旧文件
$ hexo g     #生成静态文件
$ hexo s     #在本地查看生成网页（取消用ctrl+c）
$ hexo d     #推送到GitHub
# 写完blog不需要清除缓存，直接生成静态文件即可
```

进行我们博客的推送,一旦我们推送到run-page分支,Netlify监测到我们的仓库发生了变化,就会根据这个分支的变化进行实时拉取并部署。

