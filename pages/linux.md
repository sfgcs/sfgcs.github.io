---
layout: page
title: redis
description:
---

#### 问题集

1. 工作中经常使用的linux命令有哪些？
* 文件夹类
  * ls
    * -l 详细信息
  * cd
    * ~ 主目录
    * - 上一个路径
  * rm
    * -r 递归处理
    * -f 强制删除文件或目录
    * -rf 
  * mkdir
    * -p 若所要建立目录的上层目录目前尚未建立，则会一并建立上层目录
  * rmdir 删除空目录
    * -p 若删除的目录的上层目录也为空，则一并删除
    * --ignore-fail-on-non-empty  忽略删除非空目录时的错误信息
* 文件类
  * cat
    * -n 由1开始对所有输出的行数编号
  * touch
  * grep
    * -A 10 顺便输出前十行
    * -b 10 顺便输出后十行
    * -i 忽略大小写
  * tail
    * -f 显示追加内容 tailf
  * head
    * -n<数字>：指定显示头部内容的行数；
  * sed
  * more
  * less
    * b 向后翻一页
    * 空格键 滚动一页
  * wc
    * -l 行数
    * -w 字数
    * -c 
  * mv 重命名文件或移动文件
  * cp 将指定文件或目录进行复制
    * -r
    * -f
* 系统工具类
  * df
  * du
    * -h
  * ps
  * kill
  * whereis
  * which
  * cal
  * top
  * crontab
  * chmod
  * chown
  * mail
  * echo
  * alias
  
2. shell脚本中单引号和双引号有什么区别？
  

