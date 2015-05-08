title: 初探Cent OS 6.x基本环境搭建（五）
date: 2015-3-19 22:55:32
categories: 菜鸟起步
tags: [CentOS6.x,环境搭建,第三方程序安装]
description: Cent OS 如何安装WebStrom
---

随着学习的深入，了解到了CentOS上安装软件的基本方式，也了解到了[RPMForge仓库][1]的知识:
> **RPMForge**仓库是一个用于在Red Hat Enterprise Linux (RHEL) 和Community ENTerprise Operating System (CentOS)中安装第三方软件包的工具。它提供了超过5000个rpm格式的软件包。
> RPMForge本身并不属于RHEL或CentOS系统的一部分，不过其设计意图即是为这些系统服务。可以在 http://packages.sw.be/ 浏览所有的RPMForge包列表。

## 安装RPMForge仓库 
[参考文档][2]  \\ [译文][3]  

1. 首先要确认当前系统的版本：
  通过` uname -a`命令可以查看系统的相关信息，以得知自己是32位还是64位系统。32位系统将会打印出`i686 i686 i386 GNU/Linux`，而64位则是`x86_64 x86_64 x86_64 GNU/Linux`。
2. 安装并启用RPMForge仓库
  选择与自己所使用的系统相对应的rpm包，下载并安装。
  CentOS 32位系统  

    {% codeblock lang:txt %} 
    wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm  
    rpm -Uvh rpmforge-release-0.5.2-2.el6.rf.i686.rpm
    {% endcodeblock %}  

  CentOS 64位系统  

    {% codeblock lang:txt %}
    wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm  
    rpm -Uvh rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
    {% endcodeblock %}

  安装完成后，会在`/etc/yum.repos.d`目录下生成文件`rpmforge.repo`
3. 导入密钥  

  下面向系统安装`DAG’s GPG key`
  {% codeblock lang:txt %}
    wget http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt  
    rpm --import RPM-GPG-KEY.dag.txt
  {% endcodeblock %}
注：导入的GPG key将会放在/etc/pki/rpm-gpg下的RPM-GPG-KEY-rpmforge-dag文件中。

4. 下面就可以通过仓库来安装软件了  
  目前我写东西需要一个截屏软件，以此为例

## 安装Scrot截屏工具
[参考文档][4]

1. 使用刚刚新安装的RPM 仓库安装[**giblib-devel**][5]，这是Scrot的依赖库
`yum install giblib-devel`
2. 下载并安装Scrot  
    {% codeblock lang:txt %}
        # wget http://linuxbrit.co.uk/downloads/scrot-0.8.tar.gz  
        # tar xvfvz scrot-0.8.tar.gz  
        # cd scrot-0.8  
        # ./configure  
        # make  
        # sudo make install    
    {% endcodeblock %}
 
3. 当make的时候，发现shell抛出error:
    {% codeblock lang:cmd %}
    error /usr/bin/ld: cannot find -lfreetype  
    error /usr/bin/ld: cannot find -lXext  
    {% endcodeblock %}

  gcc的编译参数为：  
   {% codeblock lang:txt %}
gcc  -g -O2 -L/usr/X11R6/lib -o scrot  main.o getopt.o getopt1.o options.o imlib.o -lX11 -L/usr/lib64 -lgiblib -L/usr/lib64 -lImlib2 -lfreetype -L/usr/X11R6/lib64 -lX11 -lXext -ldl -lm -lm
    {% endcodeblock %}

    搜索网上的资源了解到：
gcc 编译库时的简写规则为： l + 库名 => lib + 库名 + . + so
所以 lfreetype 在库中表现即为：libfreetype.so
查找目录`/usr/lib64` **注意，64位版本的Lib目录为lib64!** 发现编译的目标类库分别命名为：
`libfreetype.so.6` 、 `libXext.so.6` 。找到问题的原因后，使用`ln -s`命令建立编译的软链接即可：
    {% codeblock lang:cmd %}
        ln -s libfreetype.so.6 libfreetype.so  
        ln -s libXext.so.6 libXext.so  
    {% endcodeblock %}

4. 至此，截屏软件已经可以使用了。具体的使用方式可以参考:[scrot 从入门到精通][6]

[1]: http://packages.sw.be/
[2]: http://www.tecmint.com/enable-rpmforge-repository/ 
[3]: http://www.dannysite.com/blog/170/
[4]: http://www.centoscn.com/image-text/install/2014/1023/3995.html 
[5]: https://packages.debian.org/zh-tw/wheezy/giblib-dev
[6]: https://linuxtoy.org/archives/mastering-scrot.html