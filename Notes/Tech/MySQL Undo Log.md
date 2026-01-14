# MySQL Undo Log

## 定义

Undo Log（回滚日志）是 InnoDB 存储引擎用于保证事务原子性和实现 MVCC（多版本并发控制）的关键机制。它记录了事务对数据的修改前的旧版本，用于事务回滚和提供一致性读。

**核心作用：**
- 事务回滚：当事务失败或执行 ROLLBACK 时，利用 Undo Log 恢复到修改前的状态
- MVCC 实现：为其他事务提供历史版本数据，实现非锁定读

## 为什么重要

### 1. 保证事务原子性
当事务执行失败需要回滚时，InnoDB 通过 Undo Log 将数据恢复到事务开始前的状态，确保"要么全部成功，要么全部失败"的原子性特性。

### 2. 实现 MVCC 多版本并发控制
在 Read Committed 和 Repeatable Read 隔离级别下，InnoDB 使用 Undo Log 中的历史版本数据为其他事务提供一致性读，避免读操作阻塞写操作。

### 3. 提高并发性能
通过 MVCC 机制，读操作不会阻塞写操作，写操作也不会阻塞读操作，大幅提升数据库并发处理能力。

## 如何应用

### Undo Log 的生成过程

```sql
-- 示例：更新操作
UPDATE users SET age = 25 WHERE id = 1;

-- InnoDB 的处理流程：
-- 1. 在 Undo Log 中记录旧值：id=1, age=24
-- 2. 在数据页中更新数据：age=25
-- 3. 在 Redo Log 中记录新值（用于崩溃恢复）
```

### Undo Log 的存储结构

- **存储位置**：存储在系统表空间（ibdata1）或独立 Undo 表空间
- **组织方式**：以 Undo Segment 和 Undo Page 的形式组织
- **版本链**：通过 DB_ROLL_PTR 字段形成版本链表，指向上一个版本

### Undo Log 的清理机制

InnoDB 的 purge 线程负责清理不再需要的 Undo Log：
- 当事务提交后，且没有其他事务需要访问其产生的历史版本时
- 通过 `innodb_max_undo_log_size` 参数控制 Undo 表空间大小
- 通过 `innodb_purge_batch_size` 控制每次清理的页数

### 实际应用场景

**场景 1：事务回滚**
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
-- 发现错误，需要回滚
ROLLBACK;  -- InnoDB 使用 Undo Log 恢复 balance 原值
```

**场景 2：MVCC 一致性读**
```sql
-- 会话 A（时间：T1）
START TRANSACTION;
SELECT * FROM users WHERE id = 1;  -- age = 24

-- 会话 B（时间：T2）
UPDATE users SET age = 25 WHERE id = 1;
COMMIT;

-- 会话 A（时间：T3，仍在同一事务中）
SELECT * FROM users WHERE id = 1;  -- age 仍为 24（RR 隔离级别）
-- 通过 Undo Log 读取历史版本
```

### 相关配置参数

```ini
# Undo 表空间数量（MySQL 8.0+）
innodb_undo_tablespaces = 2

# Undo 日志最大大小（触发截断）
innodb_max_undo_log_size = 1G

# 清理线程数量
innodb_purge_threads = 4

# 回滚段数量
innodb_rollback_segments = 128
```

## 相关概念

- [[MySQL Redo Log]] - 保证事务持久性的重做日志
- [[MySQL Binlog]] - 用于主从复制的二进制日志
- [[MySQL MVCC 实现原理]] - 多版本并发控制机制
- [[MySQL 事务隔离级别]] - RR 和 RC 级别下 Undo Log 的使用
- [[MySQL 两阶段提交]] - Redo Log 和 Binlog 的协同机制
- [[InnoDB 架构]] - Undo Log 在 InnoDB 中的位置

## 参考来源

- 《MySQL 技术内幕：InnoDB 存储引擎》第 6 章
- MySQL 官方文档：InnoDB Undo Logs
- 《高性能 MySQL》第 1 章 - 事务与 MVCC

---
创建时间: 2026-01-14 22:30
标签: #mysql #innodb #transaction #mvcc #database
