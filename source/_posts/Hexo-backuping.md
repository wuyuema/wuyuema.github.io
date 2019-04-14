title: Hexo backuping!
author: wuyuema
tags:
  - 随笔
categories: []
date: 2019-04-14 23:41:00
---
备份基于hexo的博客，使用github
<!--more-->

初始化  
--
1.在你的博客仓库创建一个分支`Hexo`（这个命名随意）；  
2.设置`Hexo`为默认分支（不知道怎么设的可以百度）；  
3.将博客仓库clone至本地，将之前的Hexo文件夹中的  
`_config.yml`，`themes/`，`source`，`scffolds/`，`package.json`，`.gitignore`复制到你克隆下来的仓库文件夹，即Username.github.io；（Username是你自己的用户名）  
4.将themes/next/(我用的是NexT主题)中的`.git/`删除，否则无法将主题文件夹push；  
5.在Username.github.io；文件夹执行`npm install`，`npm install hexo-deployer-git`(这里可以看看分支是不是显示为Hexo) 
6.执行`git add`，`git commit -m "提交文件"`，`git push origin Hexo`来提交Hexo网站源文件； 
7、执行`hexo g -d` 生成静态网页部署到github上。
这样，Username.github.io仓库就有`master`分支保存静态网页，`hexo`分支保存源文件。

</br>

修改
--
在本地对博客修改（包括修改主题样式、发布新文章等）后
1、执行`git add`，`git commit -m "提交文件"`，`git push origin Hexo`来提交Hexo网站源文件；
2、执行`hexo g -d `生成静态网页部署到github上；
（每次发布重复这两步，它们之间没有严格的顺序）  

恢复  
--
换电脑想改博客：  
1、安装git；  
2、安装Nodejs和npm；  
3、使用克隆命令将仓库拷贝至本地；  
4、在文件夹内执行命令`npm install hexo-cli -g`、`npm install`、`npm install hexo-deployer-git`；  

附录  
--
Hexo的源文件说明：  
1、`_config.yml`站点的配置文件，需要拷贝；  
2、`themes/`主题文件夹，需要拷贝；  
3、`source`博客文章的.md文件，需要拷贝；  
4、`scaffolds/`文章的模板，需要拷贝；  
5、`package.json`安装包的名称，需要拷贝；  
6、`.gitignore`限定在`push`时哪些文件可以忽略，需要拷贝；  
7、`.git/`主题和站点都有，标志这是一个git项目，不需要拷贝；  
8、`node_modules/`是安装包的目录，在执行`npm install`的时候会重新生成，不需要拷贝；  
9、`public`是`hexo g`生成的静态网页，不需要拷贝；  
10、`.deploy_git`同上，`hexo g`也会生成，不需要拷贝；  
11、`db.json`文件，不需要拷贝。  
不需要拷贝的文件正是`.gitignore`中所忽略的。  



作者：Lucky锦  
链接：https://www.jianshu.com/p/baab04284923  
来源：简书  
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。  