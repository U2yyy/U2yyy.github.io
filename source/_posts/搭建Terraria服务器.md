---
title: 搭建Terraria服务器
date: 2022-09-03 21:53:43
tags:
categories:
- 个人博客
---
# 架设Terraria服务器
如何搭建一个Terraria服务器
<!-- more -->
> 今天有朋友找我咨询Terraria联机的事情，之前我们一起玩的时候都是我做主机，用内网穿透的方式让大家连接上服务器，体验还算不错，但我一直有搭一个公共服务器的想法。正好他现在需要一个服务器，我手头上又又有一个空闲的VPS可以用，于是说干就干，再加上我有那么一丁点儿的Linux终端语言基础，我直接开始Google教程，准备一步步地来搭建Terraria的服务器。

在搜索过程中，我看到一篇文章对小白非常友好，但又不是那么友好。

为什么说友好呢，因为文章从选购VPS开始，细微到Vim的使用都有讲解；但为什么说不友好呢，因为不知道是文章本身的排版有问题，还是文章转载后排版错乱了，很多代码有格式错误，并且有些命令的使用讲的比较摸棱两可，因此我想就着这篇教程把代码更新一下。

## 🎭直接从VPS入手

> 能摸索到这一步应该已经不是什么电脑小白了，因此我觉得原文里面的关于VPS的选择和介绍可以略过，甚至PUTTY的基本操作和Linux命令行的基本操作都是前置知识，我认为没有必要再提及了

### 🧀创建Swap分区

这一步的目的似乎是给内存一个缓冲空间，因为购买的VPS一般性能比较低（学生党嘛，一般内存也就能买个1G2G的）。

> 使用命令查看Swap分区

```shell
$ free -m
```

> 正常情况下应当是下图这样，swap分区空间为0

![1663270-20200729135637755-167658670.png](https://s2.loli.net/2022/09/03/svAlJLpSE6tqOKP.png)

> 删除原来的分区

```shell
$ swapoff –a
```

> 新建一个读写块大小为1M、块个数为1024的Swap分区（这里不一定要这么多，具体多少可以自己指定)

```shell
$ dd if=/dev/zero of=/root/swapfile bs=1M count=1024
```

> 格式化创建好的Swap交换分区

```shell
$ mkswap /root/swapfile
```

> 启动新建的Swap交换分区

```shell
$ swapon /root/swapfile
```

> 下面是给Swap交换分区添加到开机自启动挂载，可能步骤稍多

```shell
$ vim /etc/fstab
```

> 进入文档后，进入编辑模式，然后加入一行代码

```
/root/swapfile swap swap defaults 0 0
```

然后使用`reboot`命令或者其它办法重启实例即可，使用`free -m`查看`Swap`分区是否已经被分配内存了，然后决定是否进入下一步

### 🎨下载配置相关文件

> 在opt目录下创建`Terraria`文件夹，并在该文件夹下创建`bin,worlds,zip`三个子文件夹

```shell
$ mkdir /opt/terraria
$ mkdir /opt/terraria/{bin,worlds,zip}
```

> 进入`zip`文件夹，下载官方提供的服务器包

```shell
$ cd /opt/terraria/zip
$ wget https://terraria.org/api/download/pc-dedicated-server/terraria-server-{{这里是版本号，要随着游戏版本更新而变}}.zip
```

> 将下载好的文件解压到`bin`文件夹中

```shell
$ unzip terraria-server-{{你下载的版本号}}.zip -d/opt/terraria/bin
```

这里解压完之后可以把`zip`文件夹里面的压缩文件删除掉，不过你也可以不删除

> 将配置文件拷贝到泰拉瑞亚文件夹的根目录

```shell
$ cp -p /opt/terraria/bin/{{你的版本号}}/Windows/serverconfig.txt /opt/terraria/
```

> 编辑配置文档

```shell
$ vim /opt/terraria/serverconfig.txt
```

如果你的世界名字等需要用到中文，那么这里很可能需要改变文档的编码方式，不要进入编辑模式，手打这串字符并回车，没有出现红色警告则成功

```
: set fileencoding=utf-8
```

在文档的最后一段复制以下代码

```
world=/opt/terraria/Worlds/{{世界的名字}}.wld
worldname={{世界的名字}}
difficulty=0
autocreate=2
maxplayers=4
password={{设定的密码}}
worldpath=/opt/terraria/worlds
```

`difficulty` 是游戏的难度，对应的是0为普通，1为专家，如difficulty=0是普通模式

`autocreate `是自动生成的世界的大小，1是小世界，2是大世界，3是超大世界

`maxplayers`是最大同时游戏人数

### ✌启动服务器

> 使用下列命令赋予文件可执行权限

```shell
$ chmod 777 /opt/terraria/bin/{{你的版本号}}/Linux/TerrariaServer.bin.x86_64
```

> 启动服务器

```shell
$ cd /opt/terraria/bin/{{你的版本号}}/Linux&& ./TerrariaServer.bin.x86_64 -config/opt/terraria/serverconfig.txt
```

原文章在这里还退出了去修改原配置文件，我修改了之后出现了编码错误，因此这里就暂且不提了，服务器维护的相关指令和内容可以自行查询相关文档或者是去Google查找

### 🍟将服务器挂起

> 使用screen服务将服务器挂起，从而可以关闭PUTTY之后也能让服务器跑起来
>
> 首先创建该窗口

```shell
$ screen -S terraria
```

> 创建后会直接进入该窗口，然后我们直接启动服务器即可

```shell
$ cd /opt/terraria/bin/{{你的版本号}}/Linux&& ./TerrariaServer.bin.x86_64 -config/opt/terraria/serverconfig.txt
```

### ⛓使用安全组策略防止端口被拦截

这算是一个小坑，国内的三大VPS提供商应该都会提供一个安全组策略，设置了端口白名单。Terraria的Server启动端口默认是7777，这个端口应该是被安全组策略封锁的，因此需要手动去解除。

> 这里以阿里云为例
>
> 进入安全组并配置策略

[![vorcKx.md.png](https://s1.ax1x.com/2022/09/03/vorcKx.md.png)](https://imgse.com/i/vorcKx)

[![vorfaD.md.png](https://s1.ax1x.com/2022/09/03/vorfaD.md.png)](https://imgse.com/i/vorfaD)

> 将7777端口设置为白名单

[![vorhIe.md.png](https://s1.ax1x.com/2022/09/03/vorhIe.md.png)](https://imgse.com/i/vorhIe)

### 🎶后记

Terraria的更新速度可能有点快，这就意味着VPS持有者也要不断更新Server版本，确实是比较折磨的一件事，这只是最初级的配置教程，至于流程自动化，可能需要查阅更多资料后总结得出。
