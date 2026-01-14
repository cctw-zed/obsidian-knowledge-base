# MySQL 知识地图

> MySQL 数据库核心知识体系，从存储引擎到性能优化的完整知识网络

## 🗄️ 存储引擎

### InnoDB 核心架构
- [[InnoDB 架构]] - 整体架构与组件
- [[MySQL Buffer Pool]] - 缓冲池机制
- [[InnoDB 表空间]] - 数据文件组织

### 存储结构
- [[MySQL B+树索引]] - 索引底层实现
- [[MySQL 页结构]] - 数据页的组织方式
- [[MySQL 行格式]] - COMPACT、DYNAMIC 等行格式

## 📝 日志系统

### 事务日志
- [[MySQL Undo Log]] - 回滚日志（原子性 + MVCC）
- [[MySQL Redo Log]] - 重做日志（持久性 + 崩溃恢复）
- [[MySQL 两阶段提交]] - Redo Log 与 Binlog 的协调

### 复制日志
- [[MySQL Binlog]] - 二进制日志（主从复制）
- [[MySQL Relay Log]] - 中继日志（从库应用）

### 其他日志
- [[MySQL Error Log]] - 错误日志
- [[MySQL Slow Query Log]] - 慢查询日志
- [[MySQL General Log]] - 查询日志

## 🔒 事务与并发控制

### 事务特性（ACID）
- [[MySQL 事务隔离级别]] - RU、RC、RR、Serializable
- [[MySQL MVCC 实现原理]] - 多版本并发控制
- [[MySQL 一致性读与锁定读]] - 快照读 vs 当前读

### 锁机制
- [[MySQL 表锁]] - 表级锁
- [[MySQL 行锁]] - 记录锁、间隙锁、临键锁
- [[MySQL 意向锁]] - 表级意向锁
- [[MySQL 死锁检测]] - 死锁产生与避免

## 🚀 索引与查询优化

### 索引类型
- [[MySQL 主键索引]] - 聚簇索引
- [[MySQL 二级索引]] - 非聚簇索引
- [[MySQL 覆盖索引]] - 避免回表
- [[MySQL 联合索引]] - 最左前缀原则

### 查询优化
- [[MySQL 执行计划]] - EXPLAIN 详解
- [[MySQL 索引优化实践]] - 索引设计原则
- [[MySQL Join 优化]] - 多表关联优化
- [[MySQL 子查询优化]] - 子查询改写技巧

### 性能分析
- [[MySQL 慢查询分析]] - 定位性能瓶颈
- [[MySQL Performance Schema]] - 性能监控
- [[MySQL 执行计划成本分析]] - Cost Model

## ⚙️ 配置与调优

### 内存配置
- [[MySQL Buffer Pool 调优]] - 缓冲池大小设置
- [[MySQL Sort Buffer]] - 排序缓冲区
- [[MySQL Join Buffer]] - 关联缓冲区

### 日志配置
- [[MySQL Redo Log 配置]] - innodb_log_file_size
- [[MySQL Binlog 配置]] - 格式与过期策略

### 其他配置
- [[MySQL 连接数配置]] - max_connections
- [[MySQL 线程池]] - thread_pool

## 🔧 运维与管理

### 备份与恢复
- [[MySQL 逻辑备份]] - mysqldump
- [[MySQL 物理备份]] - Xtrabackup
- [[MySQL 崩溃恢复机制]] - Crash Recovery

### 主从复制
- [[MySQL 主从复制原理]] - 异步复制
- [[MySQL 半同步复制]] - Semi-sync
- [[MySQL GTID 复制]] - 全局事务标识符

### 高可用
- [[MySQL 主从切换]] - MHA、Orchestrator
- [[MySQL 双主架构]] - Dual Master
- [[MySQL 分库分表]] - Sharding 策略

## 📊 监控与排查

### 性能监控
- [[MySQL 关键指标监控]] - QPS、TPS、连接数
- [[MySQL 锁等待排查]] - information_schema
- [[MySQL 慢查询排查]] - pt-query-digest

### 问题诊断
- [[MySQL 死锁排查]] - show engine innodb status
- [[MySQL 主从延迟排查]] - seconds_behind_master
- [[MySQL 磁盘空间问题]] - ibdata1 膨胀

## 📚 学习路径建议

### 初级（基础概念）
1. [[MySQL 事务隔离级别]]
2. [[MySQL Undo Log]]、[[MySQL Redo Log]]
3. [[MySQL B+树索引]]

### 中级（原理深入）
1. [[MySQL MVCC 实现原理]]
2. [[MySQL 锁机制]]
3. [[MySQL 执行计划]]

### 高级（性能优化）
1. [[MySQL 索引优化实践]]
2. [[MySQL 慢查询分析]]
3. [[MySQL 主从复制原理]]

---

**使用说明：**
- 🔗 点击蓝色链接跳转到对应笔记
- 📝 方括号中的是待创建的笔记占位符
- 🏷️ 使用标签 #mysql-map 可快速定位到本地图

标签: #mysql #database #tech-map #moc
