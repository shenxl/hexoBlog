
title: 搭建MEAN项目手脚架及WebStorm调试Nodejs的环境
date: 2015年5月4日21:25:17
categories: MEAN 学习系列
tags: [Mean,webstorm,debug,nodejs]
description:  webstorm 9.0 上调试nodejs
---
关于全栈工程师，读到了一个比较喜欢的观点：
> Engineer 的本质工作是设计，开发出应用于大众的产品。一个真正的 Full Stack 
> Engineer ，他从生活中发现问题，洞察需求，他设计解决方案，并开发出初始版本的产
> 品。为了达到目标，他愿意去学习任何领域的技能和知识。同时他不追求一个人完成所
> 有工作，如果有人可以比他在某方面做得更出色，便会十分热情的邀请他们加入。
[知乎:怎样成为全栈工程师（Full Stack Developer）](http://www.zhihu.com/question/22420900)

觉得说的很好，能够独立的完成一个自己的想法，对我而言诱惑是非常大的。但是我总是一个喜欢想啊想，但是却不知道如何动手的人，可以说是勤于思考的人吧。鉴于MEAN架构是全栈由JavaScript实现的，而且环境的搭建也很简单，所以决定抽出一定的时间好好研究一下，看能不能成为实现自己想法的利器。  

##MEAN 
MEAN is an acronym for Mongo, Express.js , Angular.js and Node.js  

###MongoDB  
>Go through MongoDB Official Website and proceed to its Great Manual, which 
>should help you understand NoSQL and MongoDB better.  

###Express  
>The best way to understand express is through its Official Website, 
>particularly The Express Guide; you can also go through this StackOverflow 
>thread for more resources.  

###AngularJS  
>Angular’s Official Website is a great starting point. CodeSchool and google 
>created a great tutorial for beginners, and the angular videos by Egghead.  

###Node.js  
>Start by going through Node.js Official Website and this StackOverflow 
>thread, which should get you going with the Node.js platform in no time.

今天发现了一个搭建MEAN项目的手脚架，[mean.io](http://mean.io/#!/ "mean.io")。代码很规整，是学习MEAN的整体构架的一个很好的入口。  

##安装过程
具体的项目安装也很简单： 

    $ npm install -g mean-cli
    $ mean init <myApp>
    $ cd <myApp> && npm install

安装过程中如果没有自动启动`bower`,那么手动执行一下`bower install`就可以了，官网给出的解决方案

##Web Storm 调试 nodejs
以前使用webStorm一直是开发angularjs，因为使用chrome调试起来非常方便，就一直没研究过webStorm调试的方法，但对于刚刚接触nodejs，了解如何调试是了解整个程序如何工作的先决条件。现将解决方法记录如下：  

cmder中，找到需要调试的nodejs项目，执行：
`node --debug-brk server`

在WebStorm中，Run->Edit Configurations...在弹出的对话框中执行`ALT+Insert`,选择Node.js。命名、选择JavaScript file(即server的路径)后保存即可。

执行Debug。再需要的位置设置断点，当执行到相应逻辑时就会发现断点生效了。
后续加油咯！

