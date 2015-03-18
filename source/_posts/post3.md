title: 初探Cent OS 6.x基本环境搭建（三）
date: 2015-3-19 00:03:15 
categories: 菜鸟起步
tags: [CentOS6.x,环境搭建,node.js,express.js]
description: Cent OS 如何搭建node.js环境
---

终于到node.js的安装了，随着搜索的进行，发现baidu与google在计算机方面的搜索结果，质量上差距很大啊，推荐还是在墙外世界的进行探索吧、、、

## 安装node.js

### 前期准备[参考资料][1]
在开始之前，建议先更新一下软件库。
`yum -y update`
更新完成后，我们需要为软件的安装再做一些准备工作。我们希望构建node的最新代码，为了完成这个目的，我们需要**"Development Tools"**，这是一个编译源代码的工具集。
`yum -y groupinstall "Development Tools"`
这条命令可以将编译node.js的工具都下载下来。
> note :yum -y 代表安装的时候全自动（当有询问产生时自动确认。）

### NodeJS安装
首先，我们先进入`/usr/src`目录，这个目录一般都是存放程序源代码的。

    cd /usr/src
然后将下载好的`node.tar.gz`移动到这个文件夹中：

    mv /home/shenxl/Downloads/node-v0.12.0.tar.gz /usr/src/
解压缩

    tar zxf node-v0.12.0.tar.gz
    cd node-v0.12.0
现在Node.js的所有源代码已经提取出来了，我们可以执行配置脚本来编译源代码。

    ./configure
他将会根据系统的信息准备编译标识符，比如操作系统的位数。执行此操作后，我们要真正的准备编译源代码了。只需要输入：

    make
这个时间比较长，我用了大概10分钟。当我们完成后，我们还需要进行安装。

    make install
这个命令会将编译好的二进制文件放置到系统目录。以便让所有人都可以访问，默认情况下，node会安装在`/usr/local/bin/node`

## 安装Express.js

为了通过`sudo`命令可以在`/usr/local/bin`路径下正常执行，我们需要使用`visudo`将这个路径添加到`secure_path`下面。

    sudo visudo

找到`secure_path`,加入`":/usr/local/bin"`。然后就可以使用`npm`安装Express与supervisor(安装之后 妈妈再也不用担心我的<KBD>F5</KBD>)了

    npm -g install express express-generator supervisor

### 添加一个普通用户
安全起见，我们创建一个普通用户来使用Node.js 首先，我们添加一个用户

    useradd nodeuser

然后，我们来设置以下他的密码

    passwd nodeuser
    **********
注销、使用这个用户登录系统。

### 创建一个Express应用
Express 创建node项目非常简单，我们可以使用命令:

    express hello
    cd hello && npm install
我们可以新建一个窗口来让node应用一直启动

    screen

最后，我们使用工具`supervisor`来监视代码的修改状态

    supervisor ./bin/www

现在，访问地址`http://localhost:3000/`就可以开始我们的node之旅了！

[1]: https://www.digitalocean.com/community/tutorials/how-to-install-and-run-a-node-js-app-on-centos-6-4-64bit
[2]: http://lifegoo.pluskid.org/wiki/Screen.html