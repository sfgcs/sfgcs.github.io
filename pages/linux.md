---
layout: page
title: linux
description:
---

#### 问题集

##### 有哪些好用的linux命令?
* wget -r --no-parent --reject "index.html*" http://hostname/ -P /home/user/dirs 用 wget 抓取完整的网站目录结构，存放到本地目录中
* time command 查看命令的运行时间
* sed -i 's/被替换字符/替换字符/g' filename
* lsof -i:22 查看 22 端口现在运行的程序
  lsof -c abc 显示 abc 进程现在打开的文件
  lsof -p 12 看进程号为 12 的进程打开了哪些文件
  

