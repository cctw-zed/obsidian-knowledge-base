# MySQL Buffer Pool LRU

## 定义

MySQL Buffer Pool LRU 是 InnoDB 默认使用的内存淘汰算法。其基于原本的 LRU(Least Recent Used)，针对 InnoDB 的特点进行了特殊优化。

## 为什么重要
好的LRU算法可以将热点数据页缓存下来，可以提升缓存命中率。
### 1. 提升响应速度
命中缓存可以提升响应速度。
### 2. 提升吞吐量
缓存命中率高可以承载更高的TPS。
## 如何应用
### 1. 
### 2. 

## 相关概念


## 参考来源


---
创建时间: 2026-01-14 20:07
标签: #concept
