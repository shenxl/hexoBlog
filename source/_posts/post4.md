title: 初探Cent OS 6.x基本环境搭建（四）
date: 2015-3-19 22:28:36 
categories: 菜鸟起步
tags: [CentOS6.x,环境搭建,JRE,webStrom]
description: Cent OS 如何安装WebStrom
---
如第二篇所述，CentOS上目前使用Atom还有些不便，所以我选择了另一款IDE—— webStrom
找到官方站点：[Web Strom 安装指南][1] 一步步跟随着完成吧。

## webStrom的安装

根据系统需求 我们先要安装Oracle的JDK。
> System Requirements   Installation 
Oracle JDK/Open JDK 1.7.0_51 is required. GCC/G++ or Clang
 
### Java环境的搭建 
[JDK 安装参考][2]
- 现将下载好的`jre-8u40-linux-x64.rpm`文件移动到`/opt`目录
然后安装即可：
     `yum install jre-8u40-linux-x64.rpm`
     
### webStrom的安装
- 安装也比较简单，在过程中没有出现问题:
  1. 下载WebStorm-*.tar.gz文件[下载位置][3]
  2. 执行解压缩命令： 
     `tar xfz WebStorm-*.tar.gz`
  3. 进入bin目录，执行webstrom.sh文件即可。
    {% codeblock lang:txt  %} 
    cd my/desired/location/WebStorm-*/bin
    ./WebStorm.sh
    {% endcodeblock%}
  4. *补充一句，webstrom是有使用许可的，下载后30天可以免费试用，如果不够的话、、貌似这种问题国内的解决速度与效果真的很好啊。*

      

[1]:https://www.jetbrains.com/webstorm/help/system-requirements-and-installation.html#d140006e223
[2]:http://tecadmin.net/steps-to-install-java-on-centos-5-6-or-rhel-5-6/
[3]:https://www.jetbrains.com/webstorm/download/