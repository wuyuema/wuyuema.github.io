title: Make GithubPage Bound to a Free Domain
author: wuyuema
tags:
  - hexo
  - 网络
categories:
  - 随笔
date: 2019-05-11 23:57:00
---
新域名完成祭  
===
<!--more-->  
之前逛洛谷日报的时候，看到大佬发了一份贴域名的教程。（-->[原文](https://www.cokemine.com/wp-hxo.html)）  
本来抱着激动的心情来弄，结果中途由于咱太笨，遇到了一些没见过的错误。比如，以为A Record是自动生成的之类的，因为以前从来没有接触过DNS解析什么的，所以几乎理解不能。  
后来咱自觉地STFB，找了很多教程，但是大多步骤不全或有问题，导致一直没有弄好。经历了各种碰壁之后，咱终于成功把博客挂在了自己的域名上！  
  
以下正文  
***
原理  
===
阅读时间：30 sec  
咱有一个域名。  
咱有一个Github Page。  
咱的Github Page被塞在github的某一个服务器上。  
咱用DNS把这个域名解析到这个服务器。  
咱最后通过github内部的设置，把这个page拎出来，挂在你的域名上。  
Access!  
（然后，咱不明白为什么有了github自己的DNS解析，还要再弄一个第三方DNS...不管了，反正加一个又不会死人！）

步骤 
===
阅读时间：4 min  
预计操作时间：20 ~ 90(or 20 ~ 2147483647) min
Github Pages  
---
请自行查找文档。咱使用Github Pages + Hexo + nexT构建博客。  
域名  
---
在完成博客页面的初始化后，github的服务器会自动在一个ip上面挂上汝等的页面，并且在`github.io`这个顶级域名前面加上汝的nickname，这里假设汝名为`julao`，那么汝就可以在`julao.github.io`这个域名看到自己的网站了。  
而咱们今天的重点，就是把这个长得又丑又长的`\*.github.io`变得简明扼要，比如咱的[wuyuema.cf](https://wuyuema.cf)。  
首先，汝等想要有这样一行域名，没有几两银子是不行的。要是天底下的域名都免费，一个人只要从第一个字符到最后一个字符全排列一下，就没有空闲的域名给汝等用了。因此，几乎所有的域名，都__不是免费__的，也都__不是永久__的。  
然而如果汝等看到这里就打起了退堂鼓，可是会被咱好好嘲讽一番的。咱的标题都说了，咱有办法给汝的狗窝贴上免费的域名。 
[__Freenom__](https://www.freenom.com)是一个公益的网站，提供每12个月$0的域名。咱们今天就用这个网站注册域名。  
注册好账户然后登入进去。  
> 1. 在顶部的`Services-->Register a New Domain`里面，输入你想要的名字，比如`chickURSoBeautiful`，`Check Availability`。  
> 2. 在`.tk`、`.ml`、`.ga`、`.cf`、`gq`里面挑一个点`Get it now! `，`Checkout`。  
> 3. `Period`调成`12 Month @ FREE`，`Use your new domain`选择`Use DNS-->Use your own DNS`。  
> 4. 两个`Nameserver`分别填上`f1g1ns1.dnspod.net`和`f1g1ns2.dnspod.net`。（这两个是dnspod的ns服务器地址，先随便填两个，后面再改）  
> 5. `Continue`，在`Your Details`里面随便填上一些随机字符糊弄一下，勾上`I have read and agree to the Terms & Conditions`，`Complete Order`。  
> 6. 等一会儿，就可以在`Services-->My Domains`里面查看域名状态了。点`Manage Domain-->Manegement Tools-->Nameservers`，勾选`Use default nameservers (Freenom Nameservers)`。  

DNS  
---
咱们今天以[__Cloudflare__](www.cloudflare.com)为免费DNS解析服务商。何为而择其国外服务商焉？以国内须备案，弃之。  
注册好账号然后登录进去。  
> 1. `Add Site`，输入你刚刚注册的域名。  
> 2. 一路确认，注意要选择免费的选项。  
> 3. 在这里截图，复制框框里面的ns地址。  
![](https://ws1.sinaimg.cn/large/69bcb682gy1g2yvul93epj20nu0fy43t.jpg)  
> 4. 回到freenom的网站管理页面，`Manage Domain-->Manegement Tools-->Nameservers`，勾选`Use custom nameservers (enter below)`，把Nameserver 1和2换成你刚刚复制的地址。  
> 5. 回到cloudflare的操作页面，点`Continue`，进入解析管理。等一~~小~~会儿（几分钟~十几小时），刷新，直到——  
![](https://ws1.sinaimg.cn/large/69bcb682gy1g2yvukx8ryj20lt03iab2.jpg)  
> 6. 得到汝自己的xxx.github.io所在服务器的ip地址。具体操作：  
`ping julao.github.io`  </br>
![](https://ws1.sinaimg.cn/large/69bcb682gy1g2yvukr3nzj20el01fmxr.jpg)  
> 7. 添加A记录。像这样填：  
![](https://ws1.sinaimg.cn/large/69bcb682gy1g2yvul0v6hj20s406jju7.jpg)  ip地址从185.199.108.153到185.199.xxx+1.153(xxx是汝ping的数字)的A记录都加上最好，玄学。  
> 8. 添加CNAME。像这样填：  
![](https://ws1.sinaimg.cn/large/69bcb682gy1g2yvuknxvxj20s701oq3g.jpg)  填完了之后像这样子：  
![](https://ws1.sinaimg.cn/large/69bcb682gy1g2yvul4ph6j20t60afq5x.jpg)

Github Repo  
---
最后是github仓库的设置。打开汝等的\*\*\*.github.io的设置，找到`Custom Domain`，输入刚刚注册的域名，save，等一会儿，勾选下面的`Enforce HTTPS`。当看到这个提示的时候，操作成功。现在应该能够直接从新域名访问页面了！  
不过呢，如果就这么结束的话，以后的每一次hexo更新操作都会把Custom Domain重置。为了解决问题，需要在hexo中继续设置。  
> 1. 修改`~/_config.yml`，找到并将url改成自己的。
> 2. 在`~/source/`下，新建空白文件，命名为CNAME，内容如下：  
	```
	yoursite.xx
	www.yoursite.xx
	```  
然后`hexo clean`、`hexo g -d`。

***

完结撒花！！！  
P.S. PicGo真好用ωωω