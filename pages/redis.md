---
layout: page
title: redis
description:
---

#### 问题集

1. redis集群有哪些特性？
* Redis 集群没有使用[一致性hash](http://www.zsythink.net/archives/1182), 而是引入了哈希槽的概念.
* 其使用主从复制模型
* Redis 并不能保证数据的强一致性
* 节点握手
* MOVED 转向
* ASK 转向

[参考资料](http://doc.redisfans.com/topic/cluster-spec.html#cluster-spec)
