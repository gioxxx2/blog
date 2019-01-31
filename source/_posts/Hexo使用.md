---
title: Hexo使用
date: 2019-01-25 18:50:26
categories: 工具
tags: Hexo
---


Hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Heroku上，是搭建博客的首选框架。

<!--more-->

## 搭建环境

* 安装Node.js
    到[这里](https://nodejs.org/en/)下载安装包，安装后，在命令行输入node -v检测是否安装成功。
    ![B84DE579-582A-44FF-9823-C9A8420C0055](media/B84DE579-582A-44FF-9823-C9A8420C0055.png)
    
* Git
   * [Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
   * [Git安装](https://git-scm.com/), 在Mac下可以使用Homebrew的brew install git来安装。
    
    配置git
    
    ```
    git config --global user.name "你的GitHub用户名"
    git config --global user.email "你的GitHub注册邮箱"
    ```
    生成SSH密钥文件
    
    ```
    ssh-keygen -t rsa -C "你的GitHub注册邮箱"
    ```
    找到生成的.ssh的文件夹中的id_rsa.pub密钥，将内容全部复制，打开[Github设置SSH Key页面](https://github.com/settings/keys) 将刚刚复制的id_rsa.pub内容粘贴进去。
    
    检测是否配置公钥成功：

    ```
    ssh git@github.com 
    ```
    
    
* Hexo
    这个就是我们的个人博客网站的框架， 这里需要自己在电脑常里创建一个文件夹，可以命名为Blog，Hexo框架与以后你自己发布的网页都在这个文件夹中。创建好后，进入文件夹中
    
    使用npm命令安装Hexo，输入：
    
    ```
    npm install -g hexo-cli 
    ```
    安装完成后，初始化博客，hexo接下来的命令都是作用于创建的blog文件夹中。
    
    ```
    $ hexo init <folder>
    $ cd <folder>
    $ npm install
    ```
    新建完成后，blog文件夹的目录如下：

![屏幕快照 2019-01-30 下午2.47.14](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-01-30%20%E4%B8%8B%E5%8D%882.47.14.png)

* _config.yml： 其中我们以后的大部分操作都会在_config.yml中进行，这个文件是我们的站点的配置文件。
* scaffolds： 模板文件，规定了我们创建一篇文章的时候最开始的样子。
* source： 可以暂时的理解成我们文章的存放处。
* themes： 主题文件。

现在就可以在本地预览网站博客的雏形了。输入以下命令：

```
hexo new test_my_site

hexo g

hexo s
```
完成后打开浏览器输入地址：localhost:4000 就可以看到了。
Hexo常用命令：

```
hexo n "我的博客"  # hexo new "我的博客"新建文章
hexo g   # hexo generate生成
hexo s   # hexo server启动服务预览
hexo d   # hexo deploy部署
hexo clean # 清除缓存
```
刚刚的三个命令依次是新建一篇博客文章、生成网页、在本地预览的操作。
若是发布到线上，一般使用

```
hexo clean
hexo g -d
```


## 部署到Git

登陆Github，创建名为：你的用户名.github.io 的仓库，因为只有这样的仓库名称最后才能以静态页面展示。    

![屏幕快照 2019-01-30 下午6.51.42](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-01-30%20%E4%B8%8B%E5%8D%886.51.42.png)

创建仓库后，在仓库设置里，找到pages选项，选择master branch作为主页。

![屏幕快照 2019-01-30 下午6.53.16](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-01-30%20%E4%B8%8B%E5%8D%886.53.16.png)

简单两步 yourname.github.io 这个域名就配置成功了。

### 本地操作
修改我们的的站点配置文件_config.yml中如下字段

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 这里填入你之前在GitHub上创建仓库的完整路径，记得加上 .git
  branch: master
```
保存站点配置文件。
其实就是给hexo d 这个命令做相应的配置，让hexo知道你要把blog部署在哪个位置，很显然，我们部署在我们GitHub的仓库里。最后安装Git部署插件，输入命令：

```
npm install hexo-deployer-git --save
```
安装完后，部署网站

```
hexo clean 
hexo g -d
```
完成后，打开浏览器，在地址栏输入你的放置个人网站的仓库路径，即 http://xxxx.github.io 你就会发现你的博客已经上线了，可以在网络上被访问了。

## 绑定域名
    
我们想使用我们自己的个性化域名，这就需要绑定我们自己的域名。登录到阿里云，进入管理控制台的域名列表，找到你的个性化域名，进入解析。

![v2-47323ad4490e206aef93a3d68f0670b6_hd](media/v2-47323ad4490e206aef93a3d68f0670b6_hd.jpg)

![v2-40222b3a295bb692aac22829a8ec3be2_hd](media/v2-40222b3a295bb692aac22829a8ec3be2_hd.jpg)

包括添加三条解析记录，192.30.252.153是GitHub的地址，你也可以ping你的 http://xxxx.github.io 的ip地址，填入进去。第三个记录类型是CNAME，CNAME的记录值是：你的用户名.http://github.io 这里千万别弄错了。第二步，登录GitHub，进入之前创建的仓库，点击settings，设置Custom domain，输入你的域名

![v2-85ba6dda906f22dea4c03df2b47d994b_hd](media/v2-85ba6dda906f22dea4c03df2b47d994b_hd.jpg)


点击save保存。第三步，进入本地博客文件夹 ，进入blog/source目录下，创建一个记事本文件，输入你的域名，对，只要写进你自己的域名即可。如果带有www，那么以后访问的时候必须带有www完整的域名才可以访问，但如果不带有www，以后访问的时候带不带www都可以访问。

![v2-79abfff91af3f520e24cb91acf6aa994_hd](media/v2-79abfff91af3f520e24cb91acf6aa994_hd.jpg)

保存，命名为CNAME ，注意保存成所有文件而不是txt文件。

完成这三步，进入blog目录中，部署网站。
这时候打开浏览器在地址栏输入你的个性化域名将会直接进入你自己搭建的网站。

## 替换主题

在[Hexo官方主题目录](https://hexo.io/themes/)寻找喜欢的主题。主题一般都是repo，只要讲起clone到博客目录themes/XXXX下就可了，XXXX对应的就是你给主题起的名字，直接

```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
这样就可以保证每次主题的作者有更新了我们就可以pull获取更新。

然后在**站点**的_config.yml修改如下字段，对应的名字就是你刚才那个主题文件夹的名字：我这边是next。

```
theme: next
```
打开**主题**的_config.yml配置文件，不是站点主题文件，找到Scheme Settings
![v2-1ac152c4aabe4c10b762ee27552f1105_hd](media/v2-1ac152c4aabe4c10b762ee27552f1105_hd.jpg)

next主题有三个样式，选择你自己喜欢的样式。

站点配置文件_config.yml是配置站点通用的东西，而主题配置文件_config.yml是配置一些主题的元素。虽然同名，但路径不同，不要弄混。

保存，部署，刷新网站可以看到效果了。

## 添加文章

创建一条博文，运行下面的命令，或者直接新建一个Markdown文件，如不了解Markdown语法，可[查阅](https://zh.mweb.im/markdown.html)，新建文件需要手动添加文章头部（注意目录source/_posts）

```
hexo n "your-post-name"
```
如果是外部引入Markdown文件，在文章开头配置如下格式：

```
---
layout: post
title: 标题
date: 2017-05-26 09:00
author: "Fenpho"
categories:
    - 目录名字 
tags:
    - 标签1
    - 标签2
---
```
如果想要在新建的同时生成对应的文件夹，用于存放文档的资源文件，如图片，音视频等：将配置文件中的post_asset_folder的值从false改为true即可

```
post_asset_folder: true
```
我们可以在文章的合适地方采用<!--more-->来截断,只显示文章部分内容，通过点击阅读更多按钮来进入文章详情。

### 配合MWeb(Markdown编辑器)使用

首先，MWeb默认是文档库模式，需要启用外部模式，可以通过”文件-打开外部模式”也可以直接用快捷键 command + E 来开启。如果你使用外部模式频率比较高，也可以直接在”偏好设置”中勾选”启动时默认打开外部模式”。

进入外部模式后，你需要首先配置文件夹。你可以点击MWeb左下角的加号，点击引入文件夹，把”blog/source”配置进去。

![v2-38d91ea4eeacb7b2ea2e8667f4e4a445_hd](/images/v2-38d91ea4eeacb7b2ea2e8667f4e4a445_hd.jpg)

现在你的MWeb就已经配置好了，你可以在文件夹下看到以前Hexo的文章，你可以用 command + N 新建一个文件，愉快地写文章了。


## NexT主题个性化配置

还有更多的进阶个性化设置，如SEO、评论系统、个人头像、博客分享、订阅功能、High功能、404网页设置等，可以参看：

[NexT主题配置文档](http://theme-next.iissnan.com/theme-settings.html)
[NexT主题优化](https://segmentfault.com/a/1190000013660164)


参考出处
<https://hexo.io/zh-cn/index.html>
<https://zhuanlan.zhihu.com/p/26625249>
<https://juejin.im/post/5c4dac03f265da613c0a2811>

    

