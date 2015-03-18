title: 初探Cent OS 6.x基本环境搭建（二）
date: 2015-3-18 22:52:40 
categories: 菜鸟起步
tags: [CentOS6.x ,环境搭建 ,git ,ibus ,Atom ]
description: Cent OS 如何安装 Atom Cent OS 如何安装 输入法 Cent OS 如何配置Git 
---


浏览器已经安装完成了，书签等信息也已经同步过来，对于我来说，装机的第二步就应该是输入法了，继续开始。
## 输入法的安装

1.  `yum install "@Chinese Support"`提示权限不足，所以执行 `su` 进入root用户，再次执行`yum` ,此时就用正常安装下载了。大概有22M的文档需要下载，耐心等待中。 
2.  注销一下当前用户，然后在System -&gt; Preferences -&gt; 中会出现 Input Method 选项，点击进入。 
3.  出现以下弹出框，选择 USE  IBUS （recommended），点击 Input Method Preferences  选项进入。
4.  出现以下弹出框，General 选项包含 快捷键等设置，Input Method 中选择常用输入法，在Select an  input method中选择Chinese，会出现右边的中文输入法列表，这里选择Pinyin，然后点击add,关闭窗口，即设置成功
5.  使用 <kbd>Ctrl</kbd> + <kbd>Space</kbd>即可以完成输入法的切换。
[参考资料](http://blog.163.com/xueling1231989@126/blog/static/10264080720137139524666)

## git的安装

在等待输入法下载的时候，想起了Git，这是我等感受世界技术前沿的窗口啊。
记录安装配置如下：

### 安装Git

这里有个很权威的介绍：[起步 - 安装git](http://git-scm.com/book/zh/v1/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

1.  执行`$ yum install curl-devel expat-devel gettext-devel \
openssl-devel zlib-devel` 后，需要安装15个包，共计23M
2.  在root权限下执行`yum install git` 下载并安装最新的git源代码
3.  可以享受git的世界了。

### 连接 Github

## Atom的安装

Atom是Github开源的文档编辑器，github给他的评价是：

> A hackable text editor for the 21st Century

以下摘自[wiki](http://zh.wikipedia.org/wiki/Atom_(%E6%96%87%E5%AD%97%E7%B7%A8%E8%BC%AF%E5%99%A8)

> Atom是由GitHub开发的自由及开放源代码的文字与代码编辑器，支持OS X、Windows和Linux操作系统，支持Node.js所写的插件，并内置Git版本控制系统。多数的延伸包皆为开放源代码授权，并由社区建置与维护。Atom基于Chromium并使用CoffeeScript撰写。Atom也可当作IDE使用。
> 自2014年5月6日起，Atom的核心程序、包管理器、以及Atom基于Chromium的桌面程序框架皆使用MIT授权条款发布。

### Atom的安装

目前只支持 64位系统
1.  从[atom发布页面](https://github.com/atom/atom/releases/latest)下载`atom.x86_64.rpm`。
2.  运行`sudo yum localinstall atom.x86_64.rpm`

> 我在使用sudo时，发生错误：`xxx is not in the sudoers file.  This incident will be reported。`
> 出现这个问题，是因为执行sudo命令的用户不在sudoers文件的列表中。可以通过编辑sudoers文件，来解决这个问题。编辑sudoers文件有两种办法，一种是以root帐号执行vi sudo，另一种是root帐号执行vi /etc/sudoers.其实两者都是修改/etc/sudoers  

可以在sudoers添加下面四行中任意一条

{% codeblock lang:txt  %}
    youuser            ALL=(ALL)                ALL
    %youuser           ALL=(ALL)                ALL
    youuser            ALL=(ALL)                NOPASSWD: ALL
    %youuser           ALL=(ALL)                NOPASSWD: ALL
{% endcodeblock %}

第一行:允许用户youuser执行sudo命令(需要输入密码).
第二行:允许用户组youuser里面的用户执行sudo命令(需要输入密码).
第三行:允许用户youuser执行sudo命令,并且在执行的时候不输入密码.
第四行:允许用户组youuser里面的用户执行sudo命令,并且在执行的时候不输入密码。

1.  使用`atom`命令启动atom编辑器
2.  当我最后愉快的启动时，发生了这个错误：[#issue:2177](https://github.com/atom/atom/issues/2177)。看了一下讨论：   
{% blockquote paulcbetts https://github.com/atom/atom-shell/issues/259 commented 12 days ago %}
@gliurn I don't think anyone's saying that, only that building on Linux right now is Hard™, because part of the build is a compiled binary (libchromiumcontent), and that binary ends up being compatible with only a few distros in source form. The alternative is to make every Atom Shell user wait for a 2+ hour build and download 2+ GB of data
{% endblockquote %}
看样子在CentOS上安装atom还需要耐心等待了... T.T