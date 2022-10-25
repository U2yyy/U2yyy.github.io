---
title: 使用GitPages和Hexo部署个人博客
date: 2022-08-22 22:24:30
categories:
- 个人博客
---
 有关站点诞生的一些随笔和教程
<!-- more -->
###  前言

之前多多少少有接触过如何去搭建个人博客，虽然在系统学习前端之前，是用的宝塔面板和`wordpress`去进行傻瓜式部署的，但是当时对于我一个萌新而言，购置VPS和使用SSH去进行连接都可以成为难点。总之最后算是艰难地把个人博客给搭建起来了，并且成功解析到自己的域名上面去了，当时还是有不小的成就感的，但是海外的服务器贵，一个月就要花五十多，这还是最最便宜的那种；国内的确实便宜很多，但是要备案，非常麻烦。因此没过多久也就不了了之了。这次的建站算是门外汉通过莽硬莽出来的站点，那个时候也不懂HTML，也不懂CSS，因此连背景图的透明化都不知道如何去处理，看到程序员贴的一些代码更是无从下手，因此给我的体验可能跟新浪微博差不多，不过是能在自己域名上的新浪微博。

### 建站契机

因为专业的没落以及个人喜好等综合原因，我开始自学计算机的知识，并且有跨考等等计划。截止到今日算是我自学计算机的五个月了，前后端算是初有涉猎。此次建站的契机是我加入了一个暑期前端训练营，而其中的文档是由我负责的。本以为就是提交Word文档之类就行，但是看了很多团队的文档都是用`GithubPages`或是`GiteePages`来写的，显得大气并且便捷。因此我想借这个机会用`Hexo`和`GithubPages`建站，作为个人博客使用，以后简历也能写上去，比较实用，而且经济。

### 如何使用`GitPages`和`Hexo`部署个人博客

#### 需要掌握的技术

- Git的基本使用
- 知道Node是什么，会使用npm包管理器(不会也没关系，跟着复制粘贴代码其实就行)
- Markdown基本语法
- 会正确使用搜索引擎
- 脑子

### 安装`Hexo`

> ##### 前提：安装好Git和Node

在命令行中输入如下指令安装`Hexo`

```shell
$ npm install -g hexo-cli
```

参考文档：https://hexo.io/zh-cn/docs/

### 本地建站

使用以下指令实现框架搭建：

```shell
$ hexo init <folder>
$ cd <folder>
$ npm install
```

当然还可以直接自己创建一个文件夹，然后右键该文件夹，选择`git bash here`，然后直接输入如下代码：

```shell
$ hexo init <folder>
$ npm install
```

这样做可以省去进入目标文件夹的步骤

---

建站之后需要做的就是修改配置文件，即目录下的`config.yml`，其实用记事本就能直接修改了，具体修改需要参考官方文档：

https://hexo.io/zh-cn/docs/configuration

---

如果不满意框架自带的风格，是可以去找你自己喜欢的主题的，https://hexo.io/themes/ 这个网站里面就有很多不错的主题文件，在目录下的`theme`文件夹里面`git clone`想要的主题，然后再在`config.yml`中修改应用的主题即可。

具体代码：

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
# 在这上面修改theme为下载的主题文件夹名称即可，一般的主题文件夹里面可能会还有一个config.yml，可以修改一些参数，如应用具体哪个主题等，可以自行查询文档
```

### 创建`GitPages`

创建`GitPages`比较简单，两步就能搞定：

1. 创建一个新的仓库，仓库名一定要是`username.github.io`，其中的username当然就是自己的用户名了，注意仓库一定要是公开的；
2. 测试一下`GitPages`是否创建成功，具体要干的事就是在master分支下创建一个HTML文件，随便写点什么即可，保存后访问username.github.io，这时大概率是404，并且`Github`会亲切地提醒你是否想启用`GitPages`服务，如果确信步骤没有错误，可以等待十分钟左右再打开，这时应该能看到自己写的页面了。

### 将本地的站点拉取到`GitPages`上去

修改配置文件，以使页面得到正确解析：

```
deploy:
  type: git
  repository: git@github.com:{yourname}/{yourname}.github.io.git  #你的仓库地址SSH 
  branch: master
```

这里有一个小坑，本人踩进去了，不知道有没有跟我同样问题的人：

一定要配置全局用户名和邮箱，仅仅使用`git config user.name `和`git config user.email`去配置当前仓库会报错。我是为了使用`Gitee`和`Github`方便所以删除了全局配置，没想到这里又必须要加上了，我在加上之后使用下列代码就没有出现过问题:

```shell
hexo clean   #清除缓存文件 db.json 和已生成的静态文件 public
hexo g       #生成网站静态文件到默认设置的 public 文件夹(hexo generate 的缩写)
hexo d       #自动生成网站静态文件，并部署到设定的仓库(hexo deploy 的缩写)
```

因为每次将代码上传到`Github`上后，打开页面是不能马上看到变化的，需要等待比较长的时间，因此我们可以用：

```shell
hexo s
```

这一行代码会生成本地网页，方便立即查看页面变化，建议在`hexo d`之前先检验一遍。

### 博客写作

使用下列代码可以快速创建一篇新的文章：

```shell
hexo new "My New Post"
```

创建出来的文档似乎是md格式的，这就意味着要熟悉Markdown基本语法，这是花个二三十分钟就能掌握的语法，非常便于写作。