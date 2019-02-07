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
* echo "str" | base64
* jps JDK 1.5提供的一个显示当前所有java进程pid的命令，简单实用，非常适合在linux/unix平台上简单察看当前java进程的一些简单情况

