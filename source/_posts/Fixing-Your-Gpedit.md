title: Fix Your Gpedit
author: wuyuema
tags:
  - 组策略
  - 电脑
  - windows
categories:
  - 琐碎
date: 2020-03-16 22:59:00
---
众所周知，Windows家庭版没有组策略。这个文章使用dism安装组策略依赖包。  
<!--more-->
1. 在网上下载gpedit.msc，复制到`%SystemRoot%\Windows\system32`下。  
2. 创建一个批处理文件，文件具有以下内容：  
	``` bat  
	pushd "%~dp0"  
	dir /b C:\Windows\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~3*.mum >List.txt  
	dir /b C:\Windows\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~3*.mum >>List.txt  
	for /f %%i in ('findstr /i . List.txt 2^>nul') do dism /online /norestart /add-package:"C:\Windows\servicing\Packages\%%i"  
	```  
3. 以高权限运行之。接下来等待组策略依赖包下载安装完成即可。  