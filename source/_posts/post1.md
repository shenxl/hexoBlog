title: 初探Cent OS 6.x基本环境搭建（一） #文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2015-3-17 15:47:08 #文章生成时间，一般不改，当然也可以任意修改
categories: 菜鸟起步 #分类
tags: [CentOS6.x,环境搭建,浏览器] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: Cent OS 如何安装 Chrome浏览器
---
安装系统之后，感觉还是有些不适应。习惯性的想安装一枚Chrome，结果发现安装Chrome本身就是一项不小的工程，记录以备查询：

## Chrome浏览器的安装
google `centos install chrome` 发现资料还是不少的，基本操作为：

1.  向yum的仓库描述中添加Google的记录信息  
    cd /etc/yum.repos.d
    vi google-chrome.repo

写入如下内容：  

    [google-chrome]
    name=google-chrome
    baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch
    enabled=1
    gpgcheck=1
    gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub

2.  使用yum命令直接安装即可：
     `# yum info google-chrome-stable`
    结果console中返回错误：
    **`centos install chrome requires libstdc++.so.6(glibcxx_3.4.15)(64bit)`**
    查询了一下，发现
    > **之前Google说了，由于CentOS/RHEL 6已经是过期的系统，所以不再会有Chrome了，虽然后来由于引起了社区的抗议，从而改口，不再提CentOS/RHEL 6是过期系统了；但是，目前在CentOS/RHEL 6上已经没有Chrome可以下载使用了**。

    其实，根本的原因不是CentOS/RHEL 6有多老，连Windows XP和停止更新的Ubuntu 10.04都能继续使用Chrome呢。实际的原因是，Chrome由于种种考虑，使用了CentOS/RHEL 6中所不支持的C++ 11，所以才不能继续更新CentOS/RHEL 6上的Chrome
    也就是说现在CentOS6.X的版本只能使用[Chromium](http://zh.wikipedia.org/wiki/Chromium)

    具体安装方式：[在CentOS/RHEL 6.4上安装Chromium](http://linux.cn/article-1550-1.html "在CentOS/RHEL 6.4上安装Chromium")

    以上信息是后续查阅到的，在安装的时候发现了第二种方式： 

##[使用Richard Lloyd的**sh**脚本安装](http://www.tecmint.com/install-google-chrome-on-redhat-centos-fedora-linux/)

{% blockquote RAVI SAIVE, http://www.tecmint.com/install-google-chrome-on-redhat-centos-fedora-linux %}
Luckily, there is a script developed by Richard Lloyd, that automatically download and install latest Google Chrome browser by picking libraries from a more recent released distro and put those libraries in (/opt/google/chrome/lib) directory and then you can able to run Google Chrome on RHEL/CentOS 6.x versions.
{% endblockquote %}
这个脚本可以自动的下载和安装Google Chrome 浏览器最新版本的依赖库。然后将他们放置在chrome/lib目录中，以便在CentOS 6.x中使用Chrome。具体操作：

    # wget http://chrome.richardlloyd.org.uk/install_chrome.sh
    # chmod u+x install_chrome.sh
    # ./install_chrome.sh

然后就是漫长的等待了，中间出了一个提示，应该是询问我是否升级内核，当时我在没过脑的情况下点了**`y`**，结果第二波漫长的等待开始了！要下载355个包！安装完成后，重启了一下系统，发现已经是6.6了，这个脚本直接升级了内核！

不过还好Chrome如期安装上了，使用`# google-chrome &` 后，熟悉的页面出现了，发现一个好的浏览器真的可以屏蔽掉操作系统的很多差异啊。小开心一下~