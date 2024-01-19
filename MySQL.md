

# 《Navigating MySQL: A Step-by-Step Guide to Database Success》

这是我的学习 MySQL 过程中整理的笔记，主要涵盖了 MySQL 数据库的基础知识、使用技巧以及相关的实践经验。我将这些笔记分享在 GitHub 上，希望能够为其他学习者提供一些参考。

## 声明

1. **著作权声明：** 这份学习 MySQL 笔记的著作权归属于我，即 Miraitowa6。未经允许，禁止进行一切商业性质的复制、修改、发布、传播等活动。

2. **不搞商业用途：** 这份笔记不允许任何形式的商业用途。商业用途包括但不限于出售、用于盈利目的的培训、广告推广等。

3. **开源精神：** 笔记中可能涉及一些代码、图表等内容，遵循开源精神，我鼓励其他学习者在遵守相关法律法规的前提下，进行学习、分享、修改和改进。

4. **引用说明：** 如果你想引用这份笔记，请注明出处，并提供链接指向这个 GitHub 仓库。这有助于更多人找到原始的学习材料。

5. **内容说明：** 本书中有关查询所用的大多数表存在库 mysql 及 perfomance_schema 中，读者只需先安装完 mysql 即可，笔者所用版本为 8.0.26，读者可登录 MySQL 执行 SHOW variables LIKE 'version'; 查看版本。不同版本差异可能有所不同。

## 贡献

欢迎任何形式的贡献，包括但不限于提交 Issues、提供修正、改进内容等。如果你发现了错误或者有更好的学习方法，欢迎通过 Pull Request 进行贡献。

## 免责声明

这份笔记仅代表我个人的学习经验和理解，不对内容的准确性和完整性提供担保。在使用这份笔记的过程中，建议查阅官方文档和其他权威资料，以确保获取最新、正确的信息。

感谢你的阅读和理解！

作者：Miraitowa6
联系方式：ydd3327026244@163.com
日期：2023年1月

# 目录

## 第 1 章 了解 SQL

### 1.1 数据库基础 

```
在深入学习 MySQL 及其 SQL 语言 实现之前，应该对数据库及数据库技术的某些基本概念有所了解
```

#### 1.1.1 什么是数据库

```
数据库是一个以某种有组织的方式存储的数据集合
```

#### 1..1.2 表

```
某种特定类型数据的结构化清单
```

##### 表名

```
数据库中的每个表都有一个名字，用来标识自己，此名字是唯一的
```

##### 模式

```
描述表的信息
```

#### 1.1.3 列和数据类型

```sql
列：表中的一个字段，所有表都是由一个字段或多个字段组成的

数据类型：每个表列都有相对应的数据类型，它限制该列中存储的数据

整数类型（Integer Types）：
    TINYINT: 很小的整数，范围在 -128 到 127 或 0 到 255 之间（取决于是否有符号）。
    SMALLINT: 小整数，范围在 -32768 到 32767 或 0 到 65535 之间。
    MEDIUMINT: 中等大小整数，范围在 -8388608 到 8388607 或 0 到 16777215 之间。
    INT 或 INTEGER: 普通整数，范围在 -2147483648 到 2147483647 或 0 到 4294967295 之间。
    BIGINT: 大整数，范围在 -9223372036854775808 到 9223372036854775807 或 0 到 18446744073709551615 之间。
浮点数类型（Floating-Point Types）：
    FLOAT: 单精度浮点数。
    DOUBLE: 双精度浮点数。
    定点数类型（Fixed-Point Types）：
    DECIMAL 或 NUMERIC: 用于存储固定精度的小数，例如货币。
字符串类型（String Types）：
    CHAR: 固定长度字符串，最多 255 个字符。
    VARCHAR: 可变长度字符串，最多 65535 个字符。
    BINARY: 固定长度二进制字符串。
    VARBINARY: 可变长度二进制字符串。
    TINYBLOB: 非常小的二进制对象。
    TINYTEXT: 非常小的文本对象。
    BLOB: 二进制对象，最大大小为 65535 字节。
    TEXT: 文本对象，最大大小为 65535 字节。
    MEDIUMBLOB: 中等大小的二进制对象。
    MEDIUMTEXT: 中等大小的文本对象。
    LONGBLOB: 非常大的二进制对象。
    LONGTEXT: 非常大的文本对象。
    ENUM: 一个字符串对象，可以从预定义的值列表中选择一个。
    SET: 一个字符串对象，可以从预定义的值列表中选择零个或多个。
日期与时间类型（Date and Time Types）：
    DATE: 日期，格式为 'YYYY-MM-DD'。
    TIME: 时间，格式为 'HH:MM:SS'。
    DATETIME: 日期和时间，格式为 'YYYY-MM-DD HH:MM:SS'。
    TIMESTAMP: 类似于 DATETIME, 但是自动更新为当前时间戳。
    YEAR: 年份，存储 2 位或 4 位格式的年份。
其他类型（Other Types）：
    BOOL 或 BOOLEAN: 用于存储布尔值（真或假）。
    SERIAL: 自增长整数，通常用于创建主键。
```

#### 1.1.4 行

```
表格的数据是按行存储的，行是表格中的一个记录
```

#### 1.1.5 主键

```
一列（或一组列），其值能够唯一区分表中每个行

主键值规则：
    1. 任意两行都不具有相同的主键值
    2. 每个行都必须具有一个主键值
    3. 主键列不允许为空值
```

### 1.2 什么是 SQL

```
结构化查询语言

优点：
    1. 几乎所有重要的数据库都支持 SQL
    2. SQL 简单易学
```

## 第 2 章 MySQL 简介

### 2.1 什么是 MySQL

```
MySQL 是一种 DBMS（数据库管理系统）

成本：开源
性能：执行快
可信赖：某些非非常重要的公司都用 MySQL
简单：MySQL 很容易安装和使用
```

#### 2.1.1 客户机——服务器软件

```
DBMS 分为两类: 
	1. 基于共享文件系统的 DBMS
	2. 基于客户机——服务器的 DBMS
```

#### 2.1.2 MySQL版本

```
5.6		5.7		8.0
```

### 2.2 MySQL 工具

```
Mysql 是一个客户机-服务器 DBMS，因此，为了使用 MySQL，需要有一个客户机，即你需要用来与 MySQL 打交道的一个应用
```

#### 2.2.1 mysql 命令行实用程序

```
每个 MySQL 都用安装一个名为 mysql 的简单命令行实用程序，在终端输入 mysql -u root -p 即可登录使用
```

#### 2.2.2 MySQL Administrator

```
MySQL Administrator 是一个图形交互客户机，用来简化 MySQL 服务器的管理
```

#### 2.2.3 MySQL Query Browser

```
MySQL Query Browser 是一个图形交互客户机，用来编写和执行 MySQL 命令
```

## 第 3 章 使用 MySQL

### 3.2 选择数据库

```sql
使用数据库: 
    输入: USE 数据库名;
    输出: Database changed
    分析: 不返回任何结果，显示某种形式的通知

例如: 使用 crashcourse 数据库
use crashcourse;
```

### 3.3 了解数据库和表

```sql
列出所有的数据库: 
    输入: SHOW DATABASES;
    输出: 
    +--------------------+
    | Database           |
    +--------------------+
    | coldfusion         |
    | crashcourse        |
    | flex               |
    | forta              |
    | information_schema |
    | mysql              |
    | performance_schema |
    | study              |
    | sys                |
    | test               |
    +--------------------+
    分析: 返回可用数据库的一个列表

列出当前数据库中的所有表: 
    输入: SHOW TABLES;
    输出: 
    +------------------------------------------------------+
    | Tables_in_mysql                                      |
    +------------------------------------------------------+
    | columns_priv                                         |
    | component                                            |
    | db                                                   |
    | default_roles                                        |
    | engine_cost                                          |
    | func                                                 |
    | general_log                                          |
    | global_grants                                        |
    | gtid_executed                                        |
    | help_category                                        |
    | help_keyword                                         |
    | help_relation                                        |
    | help_topic                                           |
    | innodb_index_stats                                   |
    | innodb_table_stats                                   |
    | password_history                                     |
    | plugin                                               |
    | procs_priv                                           |
    | proxies_priv                                         |
    | replication_asynchronous_connection_failover         |
    | replication_asynchronous_connection_failover_managed |
    | replication_group_configuration_version              |
    | replication_group_member_actions                     |
    | role_edges                                           |
    | server_cost                                          |
    | servers                                              |
    | slave_master_info                                    |
    | slave_relay_log_info                                 |
    | slave_worker_info                                    |
    | slow_log                                             |
    | tables_priv                                          |
    | time_zone                                            |
    | time_zone_leap_second                                |
    | time_zone_name                                       |
    | time_zone_transition                                 |
    | time_zone_transition_type                            |
    | user                                                 |
    +------------------------------------------------------+
    分析: 返回当前选择的数据库内可用表的列表

显示指定表的列信息: 
    输入: SHOW COLUMNS FROM user;
    或者是: DESCRIBE user;
    输出: 
    +--------------------------+-----------------------------------+------+-----+-----------------------+-------+
    | Field                    | Type                              | Null | Key | Default               | Extra |
    +--------------------------+-----------------------------------+------+-----+-----------------------+-------+
    | Host                     | char(255)                         | NO   | PRI |                       |       |
    | User                     | char(32)                          | NO   | PRI |                       |       |
    | SELECT_priv              | enum('N','Y')                     | NO   |     | N                     |       |
    | Insert_priv              | enum('N','Y')                     | NO   |     | N                     |       |
    | Update_priv              | enum('N','Y')                     | NO   |     | N                     |       |
    | Delete_priv              | enum('N','Y')                     | NO   |     | N                     |       |
    | Create_priv              | enum('N','Y')                     | NO   |     | N                     |       |
    | Drop_priv                | enum('N','Y')                     | NO   |     | N                     |       |
    | Reload_priv              | enum('N','Y')                     | NO   |     | N                     |       |
    | Shutdown_priv            | enum('N','Y')                     | NO   |     | N                     |       |
    | Process_priv             | enum('N','Y')                     | NO   |     | N                     |       |
    | File_priv                | enum('N','Y')                     | NO   |     | N                     |       |
    | Grant_priv               | enum('N','Y')                     | NO   |     | N                     |       |
    | References_priv          | enum('N','Y')                     | NO   |     | N                     |       |
    | Index_priv               | enum('N','Y')                     | NO   |     | N                     |       |
    | Alter_priv               | enum('N','Y')                     | NO   |     | N                     |       |
    | SHOW_db_priv             | enum('N','Y')                     | NO   |     | N                     |       |
    | Super_priv               | enum('N','Y')                     | NO   |     | N                     |       |
    | Create_tmp_table_priv    | enum('N','Y')                     | NO   |     | N                     |       |
    | Lock_tables_priv         | enum('N','Y')                     | NO   |     | N                     |       |
    | Execute_priv             | enum('N','Y')                     | NO   |     | N                     |       |
    | Repl_slave_priv          | enum('N','Y')                     | NO   |     | N                     |       |
    | Repl_client_priv         | enum('N','Y')                     | NO   |     | N                     |       |
    | Create_view_priv         | enum('N','Y')                     | NO   |     | N                     |       |
    | SHOW_view_priv           | enum('N','Y')                     | NO   |     | N                     |       |
    | Create_routine_priv      | enum('N','Y')                     | NO   |     | N                     |       |
    | Alter_routine_priv       | enum('N','Y')                     | NO   |     | N                     |       |
    | Create_user_priv         | enum('N','Y')                     | NO   |     | N                     |       |
    | Event_priv               | enum('N','Y')                     | NO   |     | N                     |       |
    | Trigger_priv             | enum('N','Y')                     | NO   |     | N                     |       |
    | Create_tablespace_priv   | enum('N','Y')                     | NO   |     | N                     |       |
    | ssl_type                 | enum('','ANY','X509','SPECIFIED') | NO   |     |                       |       |
    | ssl_cipher               | blob                              | NO   |     | NULL                  |       |
    | x509_issuer              | blob                              | NO   |     | NULL                  |       |
    | x509_subject             | blob                              | NO   |     | NULL                  |       |
    | max_questions            | int unsigned                      | NO   |     | 0                     |       |
    | max_updates              | int unsigned                      | NO   |     | 0                     |       |
    | max_connections          | int unsigned                      | NO   |     | 0                     |       |
    | max_user_connections     | int unsigned                      | NO   |     | 0                     |       |
    | plugin                   | char(64)                          | NO   |     | caching_sha2_password |       |
    | authentication_string    | text                              | YES  |     | NULL                  |       |
    | password_expired         | enum('N','Y')                     | NO   |     | N                     |       |
    | password_last_changed    | timestamp                         | YES  |     | NULL                  |       |
    | password_lifetime        | smallint unsigned                 | YES  |     | NULL                  |       |
    | account_locked           | enum('N','Y')                     | NO   |     | N                     |       |
    | Create_role_priv         | enum('N','Y')                     | NO   |     | N                     |       |
    | Drop_role_priv           | enum('N','Y')                     | NO   |     | N                     |       |
    | Password_reuse_history   | smallint unsigned                 | YES  |     | NULL                  |       |
    | Password_reuse_time      | smallint unsigned                 | YES  |     | NULL                  |       |
    | Password_require_current | enum('N','Y')                     | YES  |     | NULL                  |       |
    | User_attributes          | json                              | YES  |     | NULL                  |       |
    +--------------------------+-----------------------------------+------+-----+-----------------------+-------+
    分析: SHOW columns 要求给出一个表名（例如 user），它对每个字段返回一行，行中包含字段名、数据类型、是否允许 NULL，键信息、默认值以及其他信息

其他支持 SHOW 的语句: 
	1. SHOW STATUS		用来显示广泛的服务器状态信息
	2. SHOW CREATE DATABASE 数据库名 和 SHOW CREATE TABLE 表名		分别用来显示创建特定数据库或表的 mysql 语句，包括表的结构、索引等
	3. SHOW GRANTS		用来显示授予用户（所有用户或特定用户）的安全权限
	4. SHOW ERRORS 和 SHOW WARNINGS		用来显示服务器错误或警告消息
	5. SHOW PROCESSLIST;		用来显示当前正在执行的进程列表
	6. SHOW VARIABLES;		用来显示数据库系统的配置变量
```

### 3.4 数据库的创建

```sql
输入: CREATE DATABASE <数据库名>;

例如: CREATE DATABASE clc;
输出: Query OK, 1 row affected (0.08 sec)
```

## 第 4 章 检索数据

### 4.1 SELECT 语句

```
用途是从一个或多个表中检索信息
```

### 4.2 检索单个列

```sql
输入: SELECT plugin FROM user;
输出: 
+-----------------------+
| plugin                |
+-----------------------+
| mysql_native_password |
| caching_sha2_password |
| caching_sha2_password |
| caching_sha2_password |
+-----------------------+
分析: 上述语句利用 SELECT 语句从 user 表中检索一个名为 plugin 的列
```

### 4.3 检索多个列

```sql
输入: SELECT Host,plugin FROM user;
输出: 
+-----------+-----------------------+
| Host      | plugin                |
+-----------+-----------------------+
| %         | mysql_native_password |
| localhost | caching_sha2_password |
| localhost | caching_sha2_password |
| localhost | caching_sha2_password |
+-----------+-----------------------+
分析: 与上一个例子一样，列名之间用逗号分隔
```

### 4.4 检索所有列

```sql
输入: SELECT * FROM user;
输出: 
+-----------+------------------+-------------+-------------+-------------+-------------+-------------+-----------+-------------+---------------+--------------+-----------+------------+-----------------+------------+------------+--------------+------------+-----------------------+------------------+--------------+-----------------+------------------+------------------+----------------+---------------------+--------------------+------------------+------------+--------------+------------------------+----------+------------------------+--------------------------+----------------------------+---------------+-------------+-----------------+----------------------+-----------------------+------------------------------------------------------------------------+------------------+-----------------------+-------------------+----------------+------------------+----------------+------------------------+---------------------+--------------------------+-----------------+
| Host      | User             | SELECT_priv | Insert_priv | Update_priv | Delete_priv | Create_priv | Drop_priv | Reload_priv | Shutdown_priv | Process_priv | File_priv | Grant_priv | References_priv | Index_priv | Alter_priv | SHOW_db_priv | Super_priv | Create_tmp_table_priv | Lock_tables_priv | Execute_priv | Repl_slave_priv | Repl_client_priv | Create_view_priv | SHOW_view_priv | Create_routine_priv | Alter_routine_priv | Create_user_priv | Event_priv | Trigger_priv | Create_tablespace_priv | ssl_type | ssl_cipher             | x509_issuer              | x509_subject               | max_questions | max_updates | max_connections | max_user_connections | plugin                | authentication_string                                                  | password_expired | password_last_changed | password_lifetime | account_locked | Create_role_priv | Drop_role_priv | Password_reuse_history | Password_reuse_time | Password_require_current | User_attributes |
+-----------+------------------+-------------+-------------+-------------+-------------+-------------+-----------+-------------+---------------+--------------+-----------+------------+-----------------+------------+------------+--------------+------------+-----------------------+------------------+--------------+-----------------+------------------+------------------+----------------+---------------------+--------------------+------------------+------------+--------------+------------------------+----------+------------------------+--------------------------+----------------------------+---------------+-------------+-----------------+----------------------+-----------------------+------------------------------------------------------------------------+------------------+-----------------------+-------------------+----------------+------------------+----------------+------------------------+---------------------+--------------------------+-----------------+
| %         | root             | Y           | Y           | Y           | Y           | Y           | Y         | Y           | Y             | Y            | Y         | Y          | Y               | Y          | Y          | Y            | Y          | Y                     | Y                | Y            | Y               | Y                | Y                | Y              | Y                   | Y                  | Y                | Y          | Y            | Y                      |          | NULL                   | NULL                     | NULL                       |             0 |           0 |               0 |                    0 | mysql_native_password | *AE47E29BB2E9F8F1EEB97F5274458B7CBBFDDA41                              | N                | 2024-01-03 15:26:21   |              NULL | N              | Y                | Y              |                   NULL |                NULL | NULL                     | NULL            |
| localhost | mysql.infoschema | Y           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          | NULL                   | NULL                     | NULL                       |             0 |           0 |               0 |                    0 | caching_sha2_password | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED | N                | 2024-01-03 15:22:18   |              NULL | Y              | N                | N              |                   NULL |                NULL | NULL                     | NULL            |
| localhost | mysql.session    | N           | N           | N           | N           | N           | N         | N           | Y             | N            | N         | N          | N               | N          | N          | N            | Y          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          | NULL                   | NULL                     | NULL                       |             0 |           0 |               0 |                    0 | caching_sha2_password | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED | N                | 2024-01-03 15:22:18   |              NULL | Y              | N                | N              |                   NULL |                NULL | NULL                     | NULL            |
| localhost | mysql.sys        | N           | N           | N           | N           | N           | N         | N           | N             | N            | N         | N          | N               | N          | N          | N            | N          | N                     | N                | N            | N               | N                | N                | N              | N                   | N                  | N                | N          | N            | N                      |          | NULL                   | NULL                     | NULL                       |             0 |           0 |               0 |                    0 | caching_sha2_password | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED | N                | 2024-01-03 15:22:18   |              NULL | Y              | N                | N              |                   NULL |                NULL | NULL                     | NULL            |
+-----------+------------------+-------------+-------------+-------------+-------------+-------------+-----------+-------------+---------------+--------------+-----------+------------+-----------------+------------+------------+--------------+------------+-----------------------+------------------+--------------+-----------------+------------------+------------------+----------------+---------------------+--------------------+------------------+------------+--------------+------------------------+----------+------------------------+--------------------------+----------------------------+---------------+-------------+-----------------+----------------------+-----------------------+------------------------------------------------------------------------+------------------+-----------------------+-------------------+----------------+------------------+----------------+------------------------+---------------------+--------------------------+-----------------+
分析: 如果给定一个通配符（*），则返回表中所有列
```

### 4.5 检索不同的行

```sql
输入: SELECT plugin FROM user;
输出: 
+-----------------------+
| plugin                |
+-----------------------+
| mysql_native_password |
| caching_sha2_password |
| caching_sha2_password |
| caching_sha2_password |
+-----------------------+

输入: SELECT DISTINCT plugin FROM user;
输出: 
+-----------------------+
| plugin                |
+-----------------------+
| mysql_native_password |
| caching_sha2_password |
+-----------------------+
分析: SELECT DISTINCT plugin 告诉 MySQL 只返回不同（唯一）的行，因此只返回两行。如果使用 distinct 关键字必须放在列名前面
```

### 4.6 限制结果

```sql
输入: SELECT priv FROM global_grants LIMIT 12;
输出: 
+----------------------------+
| priv                       |
+----------------------------+
| SYSTEM_USER                |
| BACKUP_ADMIN               |
| CLONE_ADMIN                |
| CONNECTION_ADMIN           |
| PERSIST_RO_VARIABLES_ADMIN |
| SESSION_VARIABLES_ADMIN    |
| SYSTEM_USER                |
| SYSTEM_VARIABLES_ADMIN     |
| SYSTEM_USER                |
| APPLICATION_PASSWORD_ADMIN |
| AUDIT_ADMIN                |
| BACKUP_ADMIN               |
+----------------------------+
分析: 此语句使用 SELECT 语句检索单个列，LIMIT 12 指示 MySQL 返回不多于两行

输入: SELECT priv FROM global_grants LIMIT 3,8;
输出: 
+----------------------------+
| priv                       |
+----------------------------+
| CONNECTION_ADMIN           |
| PERSIST_RO_VARIABLES_ADMIN |
| SESSION_VARIABLES_ADMIN    |
| SYSTEM_USER                |
| SYSTEM_VARIABLES_ADMIN     |
| SYSTEM_USER                |
| APPLICATION_PASSWORD_ADMIN |
| AUDIT_ADMIN                |
+----------------------------+
分析: LIMIT 3,8 指示 MySQL 返回从行 3 开始的 8 行，第一个数为开始位置，第二个数为要检索的行数
注意: 第一行为行 0

输入: SELECT priv FROM global_grants LIMIT 8 OFFSET 3;
输出: 
+----------------------------+
| priv                       |
+----------------------------+
| CONNECTION_ADMIN           |
| PERSIST_RO_VARIABLES_ADMIN |
| SESSION_VARIABLES_ADMIN    |
| SYSTEM_USER                |
| SYSTEM_VARIABLES_ADMIN     |
| SYSTEM_USER                |
| APPLICATION_PASSWORD_ADMIN |
| AUDIT_ADMIN                |
+----------------------------+
分析: LIMIT 的另一种代替语法，意思为读取 8 行从第 3 行开始
```

### 4.7 使用完全限定的表名

```sql
输入: SELECT server_cost.cost_name FROM server_cost;
输出: 
+------------------------------+
| cost_name                    |
+------------------------------+
| disk_temptable_create_cost   |
| disk_temptable_row_cost      |
| key_compare_cost             |
| memory_temptable_create_cost |
| memory_temptable_row_cost    |
| row_evaluate_cost            |
+------------------------------+
分析: 使用完全表名是指在列名前面加上表名称，可以避免命令冲突

输入: SELECT server_cost.cost_name FROM mysql.server_cost;
输出: 
+------------------------------+
| cost_name                    |
+------------------------------+
| disk_temptable_create_cost   |
| disk_temptable_row_cost      |
| key_compare_cost             |
| memory_temptable_create_cost |
| memory_temptable_row_cost    |
| row_evaluate_cost            |
+------------------------------+
分析: 使用完全表名是指在表名前面加上数据库名称，可以避免命令冲突
```

## 第 5 章 排序检索数据

### 5.1 排序数据

```sql
输入: SELECT help_category.name FROM help_category ORDER BY help_category.name;
输出: 
+---------------------------------------+
| name                                  |
+---------------------------------------+
| Account Management                    |
| Administration                        |
| Aggregate Functions and Modifiers     |
| Bit Functions                         |
| Cast Functions and Operators          |
| Comparison Operators                  |
| Components                            |
| Compound Statements                   |
| Contents                              |
| Data Definition                       |
| Data Manipulation                     |
| Data Types                            |
| Date and Time Functions               |
| Encryption Functions                  |
| Enterprise Encryption Functions       |
| Flow Control Functions                |
| Functions                             |
| Geographic Features                   |
| Geometry Constructors                 |
| Geometry Property Functions           |
| Geometry Relation Functions           |
| GeometryCollection Property Functions |
| GROUP BY Functions and Modifiers      |
| GTID                                  |
| Help Metadata                         |
| Information Functions                 |
| Internal Functions                    |
| Language Structure                    |
| LineString Property Functions         |
| Loadable Functions                    |
| Locking Functions                     |
| Logical Operators                     |
| MBR                                   |
| MBR Functions                         |
| Miscellaneous Functions               |
| Numeric Functions                     |
| Performance Schema Functions          |
| Plugins                               |
| Point Property Functions              |
| Polygon Property Functions            |
| Prepared Statements                   |
| Replication Statements                |
| Spatial Functions                     |
| Storage Engines                       |
| String Functions                      |
| Table Maintenance                     |
| Transactions                          |
| Utility                               |
| Window Functions                      |
| WKB Functions                         |
| WKT                                   |
| WKT Functions                         |
| XML                                   |
+---------------------------------------+
分析: order by 子句用于对查询结果进行排序，默认升序
```

### 5.2 按多个列排序

```sql
输入: SELECT help_category_id,help_category.name,parent_category_id FROM help_category ORDER BY help_category.name;
输出: 
+------------------+---------------------------------------+--------------------+
| help_category_id | name                                  | parent_category_id |
+------------------+---------------------------------------+--------------------+
|               46 | Account Management                    |                  0 |
|                3 | Administration                        |                  0 |
|               34 | Aggregate Functions and Modifiers     |                  4 |
|               18 | Bit Functions                         |                  4 |
|               16 | Cast Functions and Operators          |                  4 |
|               10 | Comparison Operators                  |                  4 |
|               49 | Components                            |                  0 |
|               45 | Compound Statements                   |                  0 |
|                0 | Contents                              |                  0 |
|               40 | Data Definition                       |                  0 |
|               41 | Data Manipulation                     |                  0 |
|                2 | Data Types                            |                  0 |
|               14 | Date and Time Functions               |                  4 |
|               19 | Encryption Functions                  |                  4 |
|                5 | Enterprise Encryption Functions       |                  4 |
|               12 | Flow Control Functions                |                  4 |
|                4 | Functions                             |                  0 |
|                7 | Geographic Features                   |                  0 |
|               25 | Geometry Constructors                 |                 22 |
|               26 | Geometry Property Functions           |                 22 |
|               31 | Geometry Relation Functions           |                 22 |
|               30 | GeometryCollection Property Functions |                 22 |
|               35 | GROUP BY Functions and Modifiers      |                  4 |
|               33 | GTID                                  |                  4 |
|                1 | Help Metadata                         |                  0 |
|               21 | Information Functions                 |                  4 |
|               38 | Internal Functions                    |                  4 |
|                6 | Language Structure                    |                  0 |
|               28 | LineString Property Functions         |                 22 |
|               48 | Loadable Functions                    |                  0 |
|               20 | Locking Functions                     |                  4 |
|               11 | Logical Operators                     |                  4 |
|                8 | MBR                                   |                  7 |
|               32 | MBR Functions                         |                 22 |
|               39 | Miscellaneous Functions               |                  4 |
|               13 | Numeric Functions                     |                  4 |
|               37 | Performance Schema Functions          |                  4 |
|               50 | Plugins                               |                  0 |
|               27 | Point Property Functions              |                 22 |
|               29 | Polygon Property Functions            |                 22 |
|               44 | Prepared Statements                   |                  0 |
|               43 | Replication Statements                |                  0 |
|               22 | Spatial Functions                     |                  4 |
|               52 | Storage Engines                       |                  0 |
|               15 | String Functions                      |                  4 |
|               47 | Table Maintenance                     |                  0 |
|               42 | Transactions                          |                  0 |
|               51 | Utility                               |                  0 |
|               36 | Window Functions                      |                  4 |
|               24 | WKB Functions                         |                 22 |
|                9 | WKT                                   |                  7 |
|               23 | WKT Functions                         |                 22 |
|               17 | XML                                   |                  4 |
+------------------+---------------------------------------+--------------------+
```



### 5.3 指定排序方向

```sql
输入: SELECT help_category.name FROM help_category ORDER BY help_category.name DESC;
输出: 
+---------------------------------------+
| name                                  |
+---------------------------------------+
| XML                                   |
| WKT Functions                         |
| WKT                                   |
| WKB Functions                         |
| Window Functions                      |
| Utility                               |
| Transactions                          |
| Table Maintenance                     |
| String Functions                      |
| Storage Engines                       |
| Spatial Functions                     |
| Replication Statements                |
| Prepared Statements                   |
| Polygon Property Functions            |
| Point Property Functions              |
| Plugins                               |
| Performance Schema Functions          |
| Numeric Functions                     |
| Miscellaneous Functions               |
| MBR Functions                         |
| MBR                                   |
| Logical Operators                     |
| Locking Functions                     |
| Loadable Functions                    |
| LineString Property Functions         |
| Language Structure                    |
| Internal Functions                    |
| Information Functions                 |
| Help Metadata                         |
| GTID                                  |
| GROUP BY Functions and Modifiers      |
| GeometryCollection Property Functions |
| Geometry Relation Functions           |
| Geometry Property Functions           |
| Geometry Constructors                 |
| Geographic Features                   |
| Functions                             |
| Flow Control Functions                |
| Enterprise Encryption Functions       |
| Encryption Functions                  |
| Date and Time Functions               |
| Data Types                            |
| Data Manipulation                     |
| Data Definition                       |
| Contents                              |
| Compound Statements                   |
| Components                            |
| Comparison Operators                  |
| Cast Functions and Operators          |
| Bit Functions                         |
| Aggregate Functions and Modifiers     |
| Administration                        |
| Account Management                    |
+---------------------------------------+
分析: 如果你想按照降序顺序排序，可以添加 desc 关键字在列名后面

例如: 使用 order by 和 LIMIT 的组合，能够找到一个列中最高或最低值
```

## 第 6 章 过滤数据

### 6.1 使用 where 子句

```sql
输入: SELECT global_grants.USER,WITH_GRANT_OPTION FROM global_grants WHERE WITH_GRANT_OPTION = 'N';
输出: 
+------------------+-------------------+
| USER             | WITH_GRANT_OPTION |
+------------------+-------------------+
| mysql.infoschema | N                 |
| mysql.session    | N                 |
| mysql.session    | N                 |
| mysql.session    | N                 |
| mysql.session    | N                 |
| mysql.session    | N                 |
| mysql.session    | N                 |
| mysql.session    | N                 |
| mysql.sys        | N                 |
+------------------+-------------------+
分析: 这条语句从 global_grants 表中检索两个列，只返回  WITH_GRANT_OPTION 为 N 的行
注意: 同时使用 order by 和 where 语句时，应该让 order by 位于 where 之后，否则报错
```

### 6.2 WHERE 子句操作符

```
=				等于
<>				不等于
!=				不等于
<				小于
<=				小于等于
>				大于
>=				大于等于
BETWEEN AND 	 在指定的两个值之间
IS NULL			 空值
```

#### 6.2.1 检查单个值

```sql
输入: SELECT global_grants.USER,global_grants.PRIV FROM global_grants WHERE global_grants.USER = 'mysql.sys';
输出: 
+-----------+-------------+
| USER      | PRIV        |
+-----------+-------------+
| mysql.sys | SYSTEM_USER |
+-----------+-------------+
分析: 检查 where global_grants.USER = 'mysql.sys' 语句，它返回 global_grants.USER 值为 mysql.sys 的行
```

#### 6.2.2 不匹配检查

```sql
输入: SELECT global_grants.USER,global_grants.PRIV FROM global_grants WHERE global_grants.USER != 'root';
输出: 
+------------------+----------------------------+
| USER             | PRIV                       |
+------------------+----------------------------+
| mysql.infoschema | SYSTEM_USER                |
| mysql.session    | BACKUP_ADMIN               |
| mysql.session    | CLONE_ADMIN                |
| mysql.session    | CONNECTION_ADMIN           |
| mysql.session    | PERSIST_RO_VARIABLES_ADMIN |
| mysql.session    | SESSION_VARIABLES_ADMIN    |
| mysql.session    | SYSTEM_USER                |
| mysql.session    | SYSTEM_VARIABLES_ADMIN     |
| mysql.sys        | SYSTEM_USER                |
+------------------+----------------------------+
分析: 检查 where global_grants.USER != 'root' 语句，它返回 global_grants.USER 值不为 root 的行
```

#### 6.2.3 范围值检查

```sql
输入: SELECT server_cost.cost_name,server_cost.default_value FROM server_cost WHERE server_cost.default_value BETWEEN 0 AND 10;
输出: 
+------------------------------+---------------+
| cost_name                    | default_value |
+------------------------------+---------------+
| disk_temptable_row_cost      |           0.5 |
| key_compare_cost             |          0.05 |
| memory_temptable_create_cost |             1 |
| memory_temptable_row_cost    |           0.1 |
| row_evaluate_cost            |           0.1 |
+------------------------------+---------------+
分析: 在使用 BETWEEN 时，必须指定两个值——所需范围的最低值和最高值。这两个值必须用 AND 关键字分隔
```

#### 6.2.4 空值检查

```sql
输入: SELECT server_cost.cost_name,server_cost.cost_value FROM server_cost WHERE server_cost.cost_value IS NULL;
输出: 
+------------------------------+------------+
| cost_name                    | cost_value |
+------------------------------+------------+
| disk_temptable_create_cost   |       NULL |
| disk_temptable_row_cost      |       NULL |
| key_compare_cost             |       NULL |
| memory_temptable_create_cost |       NULL |
| memory_temptable_row_cost    |       NULL |
| row_evaluate_cost            |       NULL |
+------------------------------+------------+
分析: IS NULL 语句可用来检查具有 NULL 值的列
```

## 第 7 章 数据过滤

### 7.1 组合 WHERE 子句

```
MySQL 允许给出多个 WHERE 子句，这些子句可用用两种方式使用：AND 或 OR 操作符
```

#### 7.1.1 AND 操作符

```sql
输入: SELECT server_cost.cost_name,server_cost.cost_value,server_cost.default_value FROM server_cost WHERE server_cost.cost_value IS NULL AND server_cost.default_value < 1;
输出: 
+---------------------------+------------+---------------+
| cost_name                 | cost_value | default_value |
+---------------------------+------------+---------------+
| disk_temptable_row_cost   |       NULL |           0.5 |
| key_compare_cost          |       NULL |          0.05 |
| memory_temptable_row_cost |       NULL |           0.1 |
| row_evaluate_cost         |       NULL |           0.1 |
+---------------------------+------------+---------------+
分析: 这条 SELECT 语句包含两个条件，并且用 AND 关键字连接它们，用来指示检索满足所有给定条件的行
```

#### 7.1.2 OR 操作符

```sql
输入: SELECT server_cost.cost_name,server_cost.cost_value,server_cost.default_value FROM server_cost WHERE server_cost.default_value = 666 OR server_cost.default_value = 0.5;
输出: 
+-------------------------+------------+---------------+
| cost_name               | cost_value | default_value |
+-------------------------+------------+---------------+
| disk_temptable_row_cost |       NULL |           0.5 |
+-------------------------+------------+---------------+
分析: OR 操作符告诉 DBMS 匹配任一条件而不是同时匹配两个条件
```

#### 7.1.3 计算次序

```sql
输入: SELECT server_cost.cost_name,server_cost.cost_value,server_cost.default_value FROM server_cost WHERE server_cost.default_value = 666 OR server_cost.default_value = 0.5 AND server_cost.cost_value IS NULL;
输出: 结果有偏差
分析: AND 在计算次序中优先级更高，所以会优先处理 AND 操作符，所以会按照 WHERE server_cost.default_value = 666 AND server_cost.cost_value IS NULL  顺序来处理，应该使用圆括号明确地分组相应的操作符，如下

输入: SELECT server_cost.cost_name,server_cost.cost_value,server_cost.default_value FROM server_cost WHERE (server_cost.default_value = 666 OR server_cost.default_value = 0.5) AND server_cost.cost_value IS NULL;
输出: 
+-------------------------+------------+---------------+
| cost_name               | cost_value | default_value |
+-------------------------+------------+---------------+
| disk_temptable_row_cost |       NULL |           0.5 |
+-------------------------+------------+---------------+
```

### 7.2 IN 操作符

```sql
输入: SELECT server_cost.cost_name,server_cost.cost_value,server_cost.default_value FROM server_cost WHERE server_cost.default_value IN (0.5,1);
输出: 
+------------------------------+------------+---------------+
| cost_name                    | cost_value | default_value |
+------------------------------+------------+---------------+
| disk_temptable_row_cost      |       NULL |           0.5 |
| memory_temptable_create_cost |       NULL |             1 |
+------------------------------+------------+---------------+
分析: IN 操作符用来指定条件范围，范围中的每个条件都可以进行匹配。IN 取合法值由逗号分隔，全都包括在圆括号中

优点: 
	1. IN 的语法更清楚且更直观
	2. 计算的次序更容易管理
	3. IN 操作符比 OR 更快
	4. 可以包含其他 SELECT 语句
```

### 7.3 NOT 操作符

```sql
输入: SELECT server_cost.cost_name,server_cost.cost_value,server_cost.default_value FROM server_cost WHERE server_cost.default_value NOT IN (0.5,1);
输入: 
+----------------------------+------------+---------------+
| cost_name                  | cost_value | default_value |
+----------------------------+------------+---------------+
| disk_temptable_create_cost |       NULL |            20 |
| key_compare_cost           |       NULL |          0.05 |
| memory_temptable_row_cost  |       NULL |           0.1 |
| row_evaluate_cost          |       NULL |           0.1 |
+----------------------------+------------+---------------+
分析: NOT 否定跟在它之后的条件
```

## 第 8 章 用通配符进行过滤

### 8.1 LIKE 操作符

```
通配符: 用来匹配值的一部分的特殊字符
搜索模式: 由字面值、通配符或两者组合构成的搜索条件
为了在搜索子句中使用通配符，必须使用 LIKE 操作符
```

#### 8.1.1 百分号（%）通配符

```sql
输入: SELECT server_cost.cost_name,server_cost.last_update FROM server_cost WHERE server_cost.cost_name LIKE 'dis%';
输出: 
+----------------------------+---------------------+
| cost_name                  | last_update         |
+----------------------------+---------------------+
| disk_temptable_create_cost | 2024-01-03 15:22:15 |
| disk_temptable_row_cost    | 2024-01-03 15:22:15 |
+----------------------------+---------------------+
分析: 此例子使用了搜索模式 'dis%'。在执行这条子句时，将检索任意以 dis 开头的词。% 告诉 MySQL 接受 dis之后的任意字符且不管数量多少

输入: SELECT server_cost.cost_name,server_cost.last_update FROM server_cost WHERE server_cost.cost_name LIKE '%temptable%';
输出: 
+------------------------------+---------------------+
| cost_name                    | last_update         |
+------------------------------+---------------------+
| disk_temptable_create_cost   | 2024-01-03 15:22:15 |
| disk_temptable_row_cost      | 2024-01-03 15:22:15 |
| memory_temptable_create_cost | 2024-01-03 15:22:15 |
| memory_temptable_row_cost    | 2024-01-03 15:22:15 |
+------------------------------+---------------------+
分析: % 可以出现在任何位置
```

#### 8.1.2 下划线（_）通配符

```sql
输入: SELECT help_category.name FROM help_category WHERE help_category.name LIKE 'MB_';
输出: 
+------+
| name |
+------+
| MBR  |
+------+
分析: _ 只匹配一个字符，同样不限制出现位置
```

### 8.2 使用通配符的技巧

```
1. 不要过度使用通配符
2. 在确实需要使用通配符时，除非绝对有必要，否则不要把它们用在搜索模式的开始处，因为慢
3. 仔细注意通配符的位置
```

## 第 9 章 用正则表达式进行搜索

### 9.1 正则表达式介绍

```
正则表达式是用来匹配文本的特殊的串（字符集合）
```

### 9.2 使用 MySQL 正则表达式

```
MySQL 用WHERE 子句对正则表达式提供了初步的支持，允许你指定正则表达式，过滤 SELECT 检索出的数据
```

#### 9.2.1 基本字符匹配

```sql
输入: SELECT help_category_id,help_category.name FROM help_category WHERE help_category.name LIKE 'MBR';
输出: 
+------------------+------+
| help_category_id | name |
+------------------+------+
|                8 | MBR  |
+------------------+------+

输入: SELECT help_category_id,help_category.name FROM help_category WHERE help_category.name REGEXP 'MBR';
输出: 
+------------------+---------------+
| help_category_id | name          |
+------------------+---------------+
|                8 | MBR           |
|               32 | MBR Functions |
+------------------+---------------+
分析: 
	LIKE: 
		1. 适用于简单的模糊匹配，但功能相对较弱
		2. 在某些情况下，对于简单模式可能比较高效
		3. 使用通配符 % 和 _
	REGEXP: 
		1. 支持更强大的正则表达式，可以实现更复杂的匹配规则
		2. 对于复杂的正则表达式，可能会比 LIKE 更消耗计算资源
		3. 使用正则表达式语法
		
输入: SELECT server_cost.cost_name,server_cost.last_update FROM server_cost WHERE server_cost.cost_name REGEXP '.row';
输出: 
+---------------------------+---------------------+
| cost_name                 | last_update         |
+---------------------------+---------------------+
| disk_temptable_row_cost   | 2024-01-03 15:22:15 |
| memory_temptable_row_cost | 2024-01-03 15:22:15 |
+---------------------------+---------------------+
分析: 这里使用了正则表达式 .row，'.' 是正则表达式中的一个特殊字符，它表示匹配任意字符
```

#### 9.2.2 进行 OR 匹配

```sql
输入: SELECT help_category_id,help_category.name FROM help_category WHERE help_category.name REGEXP 'MBR|XML';
输出: 
+------------------+---------------+
| help_category_id | name          |
+------------------+---------------+
|                8 | MBR           |
|               32 | MBR Functions |
|               17 | XML           |
+------------------+---------------+
分析: 语句中使用了正则表达式 MBR|XML，表示匹配其中之一，因此都匹配返回。以下是 LIKE 的对比

输入: SELECT help_category_id,help_category.name FROM help_category WHERE help_category.name LIKE 'MBR' OR help_category.name LIKE 'XML';
输出: 
+------------------+------+
| help_category_id | name |
+------------------+------+
|                8 | MBR  |
|               17 | XML  |
+------------------+------+
```

#### 9.2.3 匹配几个字符之一

```sql
输入: SELECT server_cost.cost_name,server_cost.last_update FROM server_cost WHERE server_cost.cost_name REGEXP 'e[vmp]'
输出: 
+------------------------------+---------------------+
| cost_name                    | last_update         |
+------------------------------+---------------------+
| disk_temptable_create_cost   | 2024-01-03 15:22:15 |
| disk_temptable_row_cost      | 2024-01-03 15:22:15 |
| memory_temptable_create_cost | 2024-01-03 15:22:15 |
| memory_temptable_row_cost    | 2024-01-03 15:22:15 |
| row_evaluate_cost            | 2024-01-03 15:22:15 |
+------------------------------+---------------------+
分析: 这里使用了正则表达式 'e[vmp]'，[vm] 定义一组字符，它的意思是匹配 v 或 m 或 p，因此返回 ev 和 em（没有匹配到 ep）
```

#### 9.2.4 匹配范围

```sql
输入: SELECT help_category_id,help_category.name FROM help_category WHERE help_category_id REGEXP '[1-2]' ORDER BY help_category_id;
输出: 
+------------------+-------------------------------+
| help_category_id | name                          |
+------------------+-------------------------------+
|                1 | Help Metadata                 |
|                2 | Data Types                    |
|               10 | Comparison Operators          |
|               11 | Logical Operators             |
|               12 | Flow Control Functions        |
|               13 | Numeric Functions             |
|               14 | Date and Time Functions       |
|               15 | String Functions              |
|               16 | Cast Functions and Operators  |
|               17 | XML                           |
|               18 | Bit Functions                 |
|               19 | Encryption Functions          |
|               20 | Locking Functions             |
|               21 | Information Functions         |
|               22 | Spatial Functions             |
|               23 | WKT Functions                 |
|               24 | WKB Functions                 |
|               25 | Geometry Constructors         |
|               26 | Geometry Property Functions   |
|               27 | Point Property Functions      |
|               28 | LineString Property Functions |
|               29 | Polygon Property Functions    |
|               31 | Geometry Relation Functions   |
|               32 | MBR Functions                 |
|               41 | Data Manipulation             |
|               42 | Transactions                  |
|               51 | Utility                       |
|               52 | Storage Engines               |
+------------------+-------------------------------+
分析: 这里使用正则表达式 [1-2]，定义了一个范围
```

#### 9.2.5 匹配特殊字符

```sql
输入: SELECT database_name,table_name,stat_name FROM innodb_index_stats WHERE stat_name REGEXP '.';
输出: 
+---------------+------------+--------------+
| database_name | table_name | stat_name    |
+---------------+------------+--------------+
| mysql         | component  | n_diff_pfx01 |
| mysql         | component  | n_leaf_pages |
| mysql         | component  | size         |
| sys           | sys_config | n_diff_pfx01 |
| sys           | sys_config | n_leaf_pages |
| sys           | sys_config | size         |
+---------------+------------+--------------+
分析: 因为 . 匹配任意字符，所有每个行逗号被检索出来

输入: SELECT database_name,table_name,stat_name FROM innodb_index_stats WHERE stat_name REGEXP '\\.';
输出: Empty set (0.01 sec)
分析: 为了匹配特殊字符必须使用 \\ 为前导

元字符			说明
\\f			  换页
\\n			  换行
\\r			  回车
\\t			  制表
\\v			  纵向制表
```

#### 9.2.6 匹配字符类

```sql
类					说明
[:alnum:]			  任意字母和数字
[:alpha:]			  任意字符
[:blank:]			  空格和制表
[:cntrl:]			  ASCII 控制字符
[:digit:]			  任意数字
[:graph:]			  与 [:print:] 相同，但不包括空格
[:lower:]			  任意小写字母
[:print:]			  任意可打印字符
[:punct:]			  既不在 [:alnum:] 又不在 [:cntrl:] 中的任意字符
[:space:]			  包括空格在内的任意空白字符
[:upper:]			  任意大写字母
[:xdigit:]			  任意十六进制数字

输入: SELECT database_name,table_name,stat_name FROM innodb_index_stats WHERE stat_name REGEXP '[:alnum:]';
输出: 
+---------------+------------+--------------+
| database_name | table_name | stat_name    |
+---------------+------------+--------------+
| mysql         | component  | n_diff_pfx01 |
| mysql         | component  | n_leaf_pages |
| mysql         | component  | size         |
| sys           | sys_config | n_diff_pfx01 |
| sys           | sys_config | n_leaf_pages |
| sys           | sys_config | size         |
+---------------+------------+--------------+
```

#### 9.2.7 匹配多个实例

```sql
元字符			说明
*			  0 个或多个匹配
+			  1 个或多个匹配
?			  0 个或 1 个匹配
{n}			  指定数目的匹配
{n,}		  不少于指定数目的匹配
{n,m}		  匹配数目的范围（ m 不超过 255 ）

输入: SELECT help_topic_id FROM help_relation WHERE help_topic_id REGEXP '[[:digit:]]{4}' ORDER BY help_topic_id;
输出: Empty set (0.01 sec)
分析: [:digit:] 匹配任意数字，{4} 确切要求它前面的字符出现 4 次，所以连在一起的任意 4 位数字

输入: SELECT help_topic_id,help_topic.name FROM help_topic WHERE help_topic.name REGEXP 'HELP\\_?' ORDER BY help_topic_id;
输出: 
+---------------+----------------+
| help_topic_id | name           |
+---------------+----------------+
|             0 | HELP_DATE      |
|             1 | HELP_VERSION   |
|             3 | HELP COMMAND   |
|           697 | HELP STATEMENT |
+---------------+----------------+
分析: \\ 转义字符 _ ， ? 指示前面字符可出现 0 次 或者 1 次 
```

#### 9.2.8 定位符

```sql
元字符			说明
^			  文本的开始
$			  文本的结尾
[[:<:]]		  词的开始
[[:>:]]		  词的结尾

输入: SELECT help_category_id,help_category.name FROM help_category WHERE help_category.name REGEXP 'MBR';
输出: 
+------------------+---------------+
| help_category_id | name          |
+------------------+---------------+
|                8 | MBR           |
|               32 | MBR Functions |
+------------------+---------------+

输入: SELECT help_category_id,help_category.name FROM help_category WHERE help_category.name REGEXP '^MBR$';
输出: 
+------------------+------+
| help_category_id | name |
+------------------+------+
|                8 | MBR  |
+------------------+------+
分析: 利用 ^ 开头 $ 结尾定位
```

## 第 10 章 创建计算字段

### 10.1 计算字段

```
直接从数据库中检索出转换、计算或格式化过的数据
```

### 10.2 拼接字段

```sql
拼接: 将值联结到一起构成单个值

输入: SELECT CONCAT(database_name,' date:',last_update) FROM innodb_index_stats ORDER BY database_name;
输出: 
+--------------------------------------------+
| CONCAT(database_name,' date:',last_update) |
+--------------------------------------------+
| mysql date:2024-01-03 15:22:15             |
| mysql date:2024-01-03 15:22:15             |
| mysql date:2024-01-03 15:22:15             |
| sys date:2024-01-03 15:22:18               |
| sys date:2024-01-03 15:22:18               |
| sys date:2024-01-03 15:22:18               |
+--------------------------------------------+
分析: CONCAT() 拼接串，各个串之间用逗号分隔
```

### 10.3 使用别名

```sql
输入: SELECT CONCAT(database_name,' date:',last_update) AS '曹礼成是世界上最帅的男人' FROM innodb_index_stats ORDER BY database_name;
输出: 
+--------------------------------------+
| 曹礼成是世界上最帅的男人             |
+--------------------------------------+
| mysql date:2024-01-03 15:22:15       |
| mysql date:2024-01-03 15:22:15       |
| mysql date:2024-01-03 15:22:15       |
| sys date:2024-01-03 15:22:18         |
| sys date:2024-01-03 15:22:18         |
| sys date:2024-01-03 15:22:18         |
+--------------------------------------+
分析: 它指示 SQL 创建一个名为 '曹礼成是世界上最帅的男人' 的字段，任何客户机都可以引用这个列
```

### 10.4 执行算数计算

```sql
输入: SELECT vend_id,vend_city,vend_zip FROM vendors ORDER BY vend_id;
输出: 
+---------+-------------+----------+
| vend_id | vend_city   | vend_zip |
+---------+-------------+----------+
|    1001 | Southfield  | 48075    |
|    1002 | Anytown     | 44333    |
|    1003 | Los Angeles | 90046    |
|    1004 | New York    | 11111    |
|    1005 | London      | N16 6PS  |
|    1006 | Paris       | 45678    |
+---------+-------------+----------+

输入: SELECT vend_id,vend_city,vend_zip,vend_id+vend_zip AS sum FROM vendors ORDER BY vend_id;
输出: 
+---------+-------------+----------+-------+
| vend_id | vend_city   | vend_zip | sum   |
+---------+-------------+----------+-------+
|    1001 | Southfield  | 48075    | 49076 |
|    1002 | Anytown     | 44333    | 45335 |
|    1003 | Los Angeles | 90046    | 91049 |
|    1004 | New York    | 11111    | 12115 |
|    1005 | London      | N16 6PS  |  1005 |
|    1006 | Paris       | 45678    | 46684 |
+---------+-------------+----------+-------+
分析: sum 为一个新字段，客户机可以使用这个新字段
```

## 第 11 章 使用数据处理函数

### 11.1 函数

```
与其他大多数计算机语言一样，SQL 支持利用函数来处理数据
```

### 11.2 使用函数

```
大多数 SQL 支持文本函数、数值函数、日期和时间函数、系统函数
```

#### 11.2.1 文本处理函数

```sql
函数			说明
LEFT()		  返回串左边的字符
LENGTH()	  返回串的长度
LOCATE()	  找出串的一个小串
LOWER()		  将串转换为小写
LTRIM() 	  去掉串左边的空格
RIGHT()		  返回串右边的字符
RTRIM()		  去掉串右边的空格
SOUNDEX()	  返回串的 SOUNDEX 值
SUBSTRING()	  返回子串的字符
UPPER()		  将串转换为大写

输入: SELECT vend_name,UPPER(VEND_NAME) AS new_name FROM vendors ORDER BY vend_name;
输出: 
+----------------+----------------+
| vend_name      | new_name       |
+----------------+----------------+
| ACME           | ACME           |
| Anvils R Us    | ANVILS R US    |
| Furball Inc.   | FURBALL INC.   |
| Jet Set        | JET SET        |
| Jouets Et Ours | JOUETS ET OURS |
| LT Supplies    | LT SUPPLIES    |
+----------------+----------------+

输入: SELECT cust_name,cust_contact FROM customers WHERE SOUNDEX(cust_contact) = SOUNDEX('Y\\.Lie');
输出: 
+-------------+--------------+
| cust_name   | cust_contact |
+-------------+--------------+
| Coyote Inc. | Y Lee        |
+-------------+--------------+
分析: SOUNDEX() 函数转换值和搜索串为它们的 SOUNDEX 值，因为 Y.LEE 和 Y.Lie 相似，所以它们的 SOUNDEX 值相匹配
```

#### 11.2.2 日期和时间处理函数

```sql
函 数 			说 明
AddDate() 		  增加一个日期（天、周等）
AddTime() 		  增加一个时间（时、分等）
CurDate() 		  返回当前日期
CurTime() 		  返回当前时间
Date() 			  返回日期时间的日期部分
DateDiff() 		  计算两个日期之差
Date_Add() 		  高度灵活的日期运算函数
Date_Format() 	  返回一个格式化的日期或时间串
Day() 			 返回一个日期的天数部分
DayOfWeek() 	  对于一个日期，返回对应的星期几
Hour() 			 返回一个时间的小时部分
Minute() 		 返回一个时间的分钟部分
Month() 		 返回一个日期的月份部分
Now() 			 返回当前日期和时间
Second() 		 返回一个时间的秒部分
Time() 		 	 返回一个日期时间的时间部分
Year() 			 返回一个日期的年份部分

输入: SELECT database_name,last_update FROM innodb_index_stats WHERE DATE(last_update) = '2024-01-03';
输出: 
+---------------+---------------------+
| database_name | last_update         |
+---------------+---------------------+
| mysql         | 2024-01-03 15:22:15 |
| mysql         | 2024-01-03 15:22:15 |
| mysql         | 2024-01-03 15:22:15 |
| sys           | 2024-01-03 15:22:18 |
| sys           | 2024-01-03 15:22:18 |
| sys           | 2024-01-03 15:22:18 |
+---------------+---------------------+
分析: DATE() 指示 MySQL 仅提取列的日期部分如 2024-01-03，不管后面的具体时间，还可以用下面方法实现

输入: SELECT database_name,last_update FROM innodb_index_stats WHERE YEAR(last_update) = 2024 AND MONTH(last_update) = 01 AND DAY(last_update) = 03;
输出: 
+---------------+---------------------+
| database_name | last_update         |
+---------------+---------------------+
| mysql         | 2024-01-03 15:22:15 |
| mysql         | 2024-01-03 15:22:15 |
| mysql         | 2024-01-03 15:22:15 |
| sys           | 2024-01-03 15:22:18 |
| sys           | 2024-01-03 15:22:18 |
| sys           | 2024-01-03 15:22:18 |
+---------------+---------------------+
分析: 更复杂些而已
```

#### 11.2.3 数值处理函数

```sql
函 数 		说 明
Abs() 		  返回一个数的绝对值
Cos() 		  返回一个角度的余弦
Exp() 		  返回一个数的指数值
Mod() 		  返回除操作的余数
Pi() 		  返回圆周率
Rand() 		  返回一个随机数
Sin() 		  返回一个角度的正弦
Sqrt() 		  返回一个数的平方根
Tan() 		  返回一个角度的正切

使用不多，仅简要说明
```

## 第 12 章 汇总数据

### 12.1 聚集函数

```sql
运行在行组上，计算和返回单个值的函数

函 数 		说 明
AVG() 		  返回某列的平均值
COUNT() 	  返回某列的行数
MAX() 		 返回某列的最大值
MIN() 		 返回某列的最小值
SUM() 		 返回某列值之和
```

#### 12.1.1 AVG() 函数

```sql
输入: SELECT AVG(cust_zip) FROM customers;
输出: 
+---------------+
| AVG(cust_zip) |
+---------------+
|       54686.4 |
+---------------+

注意: AVG() 函数忽略列值为 NULL 的行
```

#### 12.1.2 COUNT() 函数

```sql
输入: SELECT COUNT(*) FROM customers;
输出: 
+----------+
| COUNT(*) |
+----------+
|        5 |
+----------+
分析: COUNT(*) 对表中行的数目进行计数，不管表列中的是空值还是非空值

输入: SELECT COUNT(cust_email) FROM customers;
输出: 
+-------------------+
| COUNT(cust_email) |
+-------------------+
|                 3 |
+-------------------+
分析: 只对有值的进行计算
```

#### 12.1.3 MAX() 函数

```sql
输入: SELECT MAX(cust_zip) FROM customers;
输出: 
+---------------+
| MAX(cust_zip) |
+---------------+
| 88888         |
+---------------+
分析: MAX() 忽略列值为 NULL 的行
```

#### 12.1.4 MIN() 函数

```sql
输入: SELECT MIN(cust_zip) FROM customers;
输出: 
+---------------+
| MIN(cust_zip) |
+---------------+
| 42222         |
+---------------+
分析: MIN() 忽略列值为 NULL 的行
```

#### 12.1.5 SUM() 函数

```sql
输入: SELECT SUM(cust_zip) FROM customers;
输出: 
+---------------+
| SUM(cust_zip) |
+---------------+
|        273432 |
+---------------+
分析: SUM() 忽略列值为 NULL 的行
```

### 12.2 聚集不同值

```sql
输入: SELECT AVG(stat_value) FROM innodb_index_stats;
输出: 
+-----------------+
| AVG(stat_value) |
+-----------------+
|          1.4571 |
+-----------------+

输入: SELECT AVG(DISTINCT stat_value) FROM innodb_index_stats;
输出: 
+--------------------------+
| AVG(DISTINCT stat_value) |
+--------------------------+
|                   3.2000 |
+--------------------------+
分析: DISTINCT 排除了重复值
```

### 12.3 组合聚集函数

```sql
输入: SELECT COUNT(*),AVG(stat_value),MIN(stat_value),MAX(stat_value) FROM innodb_index_stats;
输出: 
+----------+-----------------+-----------------+-----------------+
| COUNT(*) | AVG(stat_value) | MIN(stat_value) | MAX(stat_value) |
+----------+-----------------+-----------------+-----------------+
|       35 |          1.4571 |               0 |               6 |
+----------+-----------------+-----------------+-----------------+
```

## 第 13 章 分组数据

### 13.1 数据分组

```
分组允许把数据分为多个逻辑组，以便能对每个组进行聚集计算
```

### 13.2 创建分组

```sql
输入: SELECT COUNT(*) FROM global_grants;
输出: 
+----------+
| COUNT(*) |
+----------+
|       38 |
+----------+
分析: 输出所有行数

输入: SELECT USER,COUNT(*) FROM global_grants GROUP BY USER;
输出: 
+------------------+----------+
| USER             | COUNT(*) |
+------------------+----------+
| mysql.infoschema |        1 |
| mysql.session    |        7 |
| mysql.sys        |        1 |
| root             |       29 |
+------------------+----------+
分析: 通过 GROUP BY 分组的形式查询，对 USER 列的每个值计算一次而不是整个表

注意: 
	1. GROUP BY 子句可以包含任意数目的列
	2. 如果在 GROUP BY 子句中嵌套了分组，数据将在最后规定的分组上进行汇总
	3. GROUP BY 子句中列出的每个列都必须是检索列或有效的表达式（但不能是聚集函数）
	4. 除聚集计算语句外，SELECT 语句中的每个列都必须在 GROUP BY 子句中给出
	5. 如果分组列中有 NULL 值，则 NULL 将作为一个分组返回
	6. GROUP BY 子句必须在 WHERE 子句之后, ORDER BY 子句前
```

### 13.3 过滤分组

```sql
注意: WHERE 过滤行, HAVING 过滤分组

输入: SELECT USER,COUNT(*) FROM global_grants GROUP BY USER HAVING COUNT(*) >= 7;
输出: 
+---------------+----------+
| USER          | COUNT(*) |
+---------------+----------+
| mysql.session |        7 |
| root          |       29 |
+---------------+----------+
分析: HAVING 支持 WHERE 所有操作符，上面例子过滤 >= 7 的行数
```

### 13.4 SELECT 子句顺序

```sql
SELECT -> FROM -> WHERE -> GROUP BY -> HAVING -> ORDER BY -> LIMIT
```

## 第 14 章 使用子查询

### 14.1 子查询

```
嵌套在其他查询中的查询
```

### 14.2 利用子查询进行过滤

```sql
输入: SELECT database_name FROM innodb_table_stats WHERE table_name REGEXP 'orders';
输出:
+---------------+
| database_name |
+---------------+
| crashcourse   |
+---------------+

输入: SELECT database_name,last_update FROM innodb_index_stats WHERE database_name REGEXP 'crashcourse';
输出:
+---------------+---------------------+
| database_name | last_update         |
+---------------+---------------------+
| crashcourse   | 2024-01-09 17:24:26 |
| crashcourse   | 2024-01-09 17:24:26 |
| crashcourse   | 2024-01-09 17:24:26 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:24:16 |
| crashcourse   | 2024-01-09 17:24:16 |
| crashcourse   | 2024-01-09 17:24:16 |
+---------------+---------------------+

利用子查询结合:
	输入: SELECT database_name,last_update FROM innodb_index_stats WHERE database_name = (SELECT database_name FROM innodb_table_stats WHERE table_name REGEXP 'orders');
	输出:
+---------------+---------------------+
| database_name | last_update         |
+---------------+---------------------+
| crashcourse   | 2024-01-09 17:24:26 |
| crashcourse   | 2024-01-09 17:24:26 |
| crashcourse   | 2024-01-09 17:24:26 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:22:59 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:24:36 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:23:01 |
| crashcourse   | 2024-01-09 17:24:16 |
| crashcourse   | 2024-01-09 17:24:16 |
| crashcourse   | 2024-01-09 17:24:16 |
+---------------+---------------------+
分析: 在 SELECT 语句中，子查询总是从内向外处理
```

### 14.3 作为计算字段使用子查询

```sql
输入: SELECT COUNT(*) AS root FROM global_grants WHERE USER REGEXP 'root';
输出: 
+------+
| root |
+------+
|   29 |
+------+

输入: SELECT help_topic_id,help_topic.name FROM help_topic WHERE help_topic_id <= (SELECT COUNT(*) AS root FROM global_grants WHERE USER REGEXP 'root') ORDER BY help_topic_id;
输出:
+---------------+----------------------------+
| help_topic_id | name                       |
+---------------+----------------------------+
|             0 | HELP_DATE                  |
|             1 | HELP_VERSION               |
|             2 | AUTO_INCREMENT             |
|             3 | HELP COMMAND               |
|             4 | ASYMMETRIC_DECRYPT         |
|             5 | ASYMMETRIC_DERIVE          |
|             6 | ASYMMETRIC_ENCRYPT         |
|             7 | ASYMMETRIC_SIGN            |
|             8 | ASYMMETRIC_VERIFY          |
|             9 | CREATE_ASYMMETRIC_PRIV_KEY |
|            10 | CREATE_ASYMMETRIC_PUB_KEY  |
|            11 | CREATE_DH_PARAMETERS       |
|            12 | CREATE_DIGEST              |
|            13 | TRUE                       |
|            14 | FALSE                      |
|            15 | BIT                        |
|            16 | TINYINT                    |
|            17 | BOOLEAN                    |
|            18 | SMALLINT                   |
|            19 | MEDIUMINT                  |
|            20 | INT                        |
|            21 | INTEGER                    |
|            22 | BIGINT                     |
|            23 | DECIMAL                    |
|            24 | DEC                        |
|            25 | FLOAT                      |
|            26 | DOUBLE                     |
|            27 | DOUBLE PRECISION           |
|            28 | DATE                       |
|            29 | DATETIME                   |
+---------------+----------------------------+
分析：使用子查询的另一方法就是创建计算字段
```

## 第 15 章 联结表

### 15.1 联结

```
SQL 最强大的功能之一就是能在数据检索查询的执行中联结表
```

#### 15.1.1 关系表

```
关系表的设计就是要保证把信息分解成多个表，一类数据一个表。各表通过某些常用的值（即关系设计中的关系）互相关联

外键：为某个表中的一列，它包含另一个表的主键值，定义了两个表之间的关系

可伸缩性：能够适应不断增加的工作量而不失败
```

#### 15.1.2 为什么要使用联结

```sql
联结是一种机制，用来在一条 SELECT 语句中关联表，使用特殊语法可以联结多个表返回一组输出，联结在运行时关联表中正确的行
```

### 15.2 创建联结

```sql
输入: SELECT innodb_table_stats.database_name,n_rows,stat_name FROM innodb_table_stats,innodb_index_stats WHERE innodb_table_stats.table_name = innodb_index_stats.table_name;
输出:
+---------------+--------+--------------+
| database_name | n_rows | stat_name    |
+---------------+--------+--------------+
| crashcourse   |      5 | n_diff_pfx01 |
| crashcourse   |      5 | n_leaf_pages |
| crashcourse   |      5 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_diff_pfx02 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_diff_pfx02 |
| crashcourse   |      0 | n_diff_pfx03 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      5 | n_diff_pfx01 |
| crashcourse   |      5 | n_leaf_pages |
| crashcourse   |      5 | size         |
| crashcourse   |      5 | n_diff_pfx01 |
| crashcourse   |      5 | n_diff_pfx02 |
| crashcourse   |      5 | n_leaf_pages |
| crashcourse   |      5 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_diff_pfx02 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      6 | n_diff_pfx01 |
| crashcourse   |      6 | n_leaf_pages |
| crashcourse   |      6 | size         |
| mysql         |      0 | n_diff_pfx01 |
| mysql         |      0 | n_leaf_pages |
| mysql         |      0 | size         |
| sys           |      6 | n_diff_pfx01 |
| sys           |      6 | n_leaf_pages |
| sys           |      6 | size         |
+---------------+--------+--------------+
分析: FROM 列出了两个表，它们就是所联结的表，这两个表用 WHERE 子句正确联结
```

#### 15.2.1 WHERE 子句的重要性

```sql
笛卡儿积: 由没有联结条件的表关系返回的结果为笛卡儿积，检索出的行的数目将时第一个表中的行数乘第二个表中的行数。拿上面例子举例👇


输入: SELECT innodb_table_stats.database_name,n_rows,stat_name FROM innodb_table_stats,innodb_index_stats;
输出:
………………………………………………（此处省略返回结果）
245 rows in set (0.00 sec)
分析: 可以看到返回结果明显不同，数据多的多，这并不是我们所想要的，应该保证所有联结都有 WHERE 子句
```

#### 15.2.2 内部联结

```sql
目前为止所用的联结称为等值联结，它基于两个表之间的相等测试，也被称为内部联结。其实对于这种联结可以使用稍微不同的语法来明确指定联结的类型，如下所示

输入: SELECT innodb_table_stats.database_name,n_rows,stat_name FROM innodb_table_stats INNER JOIN innodb_index_stats ON innodb_table_stats.table_name = innodb_index_stats.table_name;
输出:
+---------------+--------+--------------+
| database_name | n_rows | stat_name    |
+---------------+--------+--------------+
| crashcourse   |      5 | n_diff_pfx01 |
| crashcourse   |      5 | n_leaf_pages |
| crashcourse   |      5 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_diff_pfx02 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_diff_pfx02 |
| crashcourse   |      0 | n_diff_pfx03 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      5 | n_diff_pfx01 |
| crashcourse   |      5 | n_leaf_pages |
| crashcourse   |      5 | size         |
| crashcourse   |      5 | n_diff_pfx01 |
| crashcourse   |      5 | n_diff_pfx02 |
| crashcourse   |      5 | n_leaf_pages |
| crashcourse   |      5 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      0 | n_diff_pfx01 |
| crashcourse   |      0 | n_diff_pfx02 |
| crashcourse   |      0 | n_leaf_pages |
| crashcourse   |      0 | size         |
| crashcourse   |      6 | n_diff_pfx01 |
| crashcourse   |      6 | n_leaf_pages |
| crashcourse   |      6 | size         |
| mysql         |      0 | n_diff_pfx01 |
| mysql         |      0 | n_leaf_pages |
| mysql         |      0 | size         |
| sys           |      6 | n_diff_pfx01 |
| sys           |      6 | n_leaf_pages |
| sys           |      6 | size         |
+---------------+--------+--------------+
分析：这里两个表之间的关系是 FROM 子句的组成部分，以 INNER JOIN 指定。在使用这种语法时，联结条件用特定的 ON 子句而不是 WHERE 子句给出。传递给 ON 的实际条件与传递给 WHERE 的相同

SQL 规范首选 INNER JOIN ON 语法
```

#### 15.2.3 联结多个表

```sql
输入: SELECT innodb_table_stats.database_name,n_rows,stat_name FROM innodb_table_stats INNER JOIN innodb_index_stats ON innodb_table_stats.table_name = innodb_index_stats.table_name INNER JOIN db ON db.Db = innodb_table_stats.database_name;
输出:
+---------------+--------+--------------+
| database_name | n_rows | stat_name    |
+---------------+--------+--------------+
| sys           |      6 | n_diff_pfx01 |
| sys           |      6 | n_leaf_pages |
| sys           |      6 | size         |
+---------------+--------+--------------+
```

## 第 16 章 创建高级联结

### 16.1 使用表别名

```sql
输入: SELECT a.Db,last_update FROM db AS a INNER JOIN innodb_table_stats AS b ON a.Db = b.database_name;
输出:
+-----+---------------------+
| Db  | last_update         |
+-----+---------------------+
| sys | 2024-01-03 15:22:18 |
+-----+---------------------+
分析:声明别名后必须使用别名，好像是这样的，因为鄙人曾将 a.Db 换成 db.Db 后报错，所以请注意
```

### 16.2 使用不同类型的联结

```
我们目前使用的只是称为内部联结的简单联结，下面将学习其他三种联结
```

#### 16.2.1 自联结

```sql
自联结是指在同一张表内进行联结操作

输入: SELECT parent_category_id AS end FROM help_category WHERE help_category_id = (SELECT help_category_id FROM help_category WHERE name = 'XML');
输出:
+------+
| end  |
+------+
|    4 |
+------+

现在来看使用联结的相同查询:

输入: SELECT a.parent_category_id AS end FROM help_category AS a INNER JOIN help_category AS b ON a.help_category_id = b.help_category_id AND a.name = 'XML';
输出:
+------+
| end  |
+------+
|    4 |
+------+

输入: SELECT a.parent_category_id AS end FROM help_category AS a,help_category AS b WHERE a.help_category_id = b.help_category_id AND a.name = 'XML';
输出:
+------+
| end  |
+------+
|    4 |
+------+
```

#### 16.2.2 自然联结

```sql
自然联结基于两个表之间的共同列名进行的，排除多次出现，使每个列只返回一次

输入: SELECT * FROM customers NATURAL JOIN orders;
输出:
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+-----------+------------+
| cust_id | cust_name      | cust_address        | cust_city | cust_state | cust_zip | cust_country | cust_contact | cust_email          | order_num | order_date |
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+-----------+------------+
|   10001 | Coyote Inc.    | 200 Maple Lane      | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com     |     20005 | 2005-09-01 |
|   10003 | Wascals        | 1 Sunny Place       | Muncie    | IN         | 42222    | USA          | Jim Jones    | rabbit@wascally.com |     20006 | 2005-09-12 |
|   10004 | Yosemite Place | 829 Riverside Drive | Phoenix   | AZ         | 88888    | USA          | Y Sam        | sam@yosemite.com    |     20007 | 2005-09-30 |
|   10005 | E Fudd         | 4545 53rd Street    | Chicago   | IL         | 54545    | USA          | E Fudd       | NULL                |     20008 | 2005-10-03 |
|   10001 | Coyote Inc.    | 200 Maple Lane      | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com     |     20009 | 2005-10-08 |
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+-----------+------------+
```

#### 16.2.3 外部联结

```sql
外部联结是 SQL 中的一种联结操作，它可以包括没有匹配行的表中数据

employees 表:
+-------------+-------------+--------+
| employee_id | employee_name| dept_id|
+-------------+-------------+--------+
| 1           | John        | 101    |
| 2           | Jane        | 102    |
| 3           | Bob         | 103    |
| 4           | Alice       | 101    |
+-------------+-------------+--------+

departments 表:
+--------+---------------+
| dept_id| department_name|
+--------+---------------+
| 101    | HR            |
| 102    | Finance       |
| 104    | Marketing     |
+--------+---------------+

左外部联结: 返回左边表中的所有行以及右表中匹配的行。如果右表没有匹配的行，那么相应的列值将被设置为 NULL

输入: SELECT employees.employee_id, employees.employee_name, departments.department_name FROM employees LEFT JOIN departments ON employees.dept_id = departments.dept_id;
输出:
+-------------+-------------+------------------+
| employee_id | employee_name| department_name  |
+-------------+-------------+------------------+
| 1           | John        | HR               |
| 2           | Jane        | Finance          |
| 3           | Bob         | NULL             |
| 4           | Alice       | HR               |
+-------------+-------------+------------------+

右外部联结: 返回右边表中的所有行以及左表中匹配的行。如果左表没有匹配的行，那么相应的列值将被设置为 NULL

输入: SELECT employees.employee_id, employees.employee_name, departments.department_name FROM employees RIGHT JOIN departments ON employees.dept_id = departments.dept_id;
输出:
+-------------+-------------+------------------+
| employee_id | employee_name| department_name  |
+-------------+-------------+------------------+
| 1           | John        | HR               |
| 2           | Jane        | Finance          |
| 4           | Alice       | HR               |
| NULL        | NULL        | Marketing        |
+-------------+-------------+------------------+

完整外部联结：返回左右两个表中的所有行，如果没有匹配的行，相应的列值将被设置为 NULL

输入: SELECT employees.employee_id, employees.employee_name, departments.department_name FROM employees FULL JOIN departments ON employees.dept_id = departments.dept_id;
输出:
+-------------+-------------+------------------+
| employee_id | employee_name| department_name  |
+-------------+-------------+------------------+
| 1           | John        | HR               |
| 2           | Jane        | Finance          |
| 3           | Bob         | NULL             |
| 4           | Alice       | HR               |
| NULL        | NULL        | Marketing        |
+-------------+-------------+------------------+
```

### 16.3 使用带聚集函数的联结

```sql
输入: SELECT COUNT(a.parent_category_id) AS end FROM help_category AS a INNER JOIN help_category AS b ON a.help_category_id = b.help_category_id WHERE a.name REGEXP 'XML|MBR';
输出:
+-----+
| end |
+-----+
|   3 |
+-----+
```

## 第 17 章 组合查询

### 17.1 组合查询

```
MySQL 允许执行多个查询（多条 SELECT 语句），并将结果作为单个查询集返回
```

### 17.2 创建组合查询

```
可用 UNION 操作符来组合数条 SQL 查询
```

#### 17.2.1 使用 UNION

```sql
输入: SELECT user.USER FROM user UNION SELECT global_grants.USER FROM global_grants;
输出:
+------------------+
| USER             |
+------------------+
| root             |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
+------------------+
分析: UNION 指示 MySQL 执行两条 SELECT 语句，并把输出组合成单个查询结果集
```

#### 17.2.2 UNION 规则

```
1. UNION 必须由两条或两条以上的 SELECT 语句组成，语句之间用 UNION 分隔
2. UNION 中的每个查询必须包含相同的列、表达式或聚集函数（不管各个列不需要以相同的次序列出）
3. 列数据类型必须兼容：类型不必完全相同，但必须是 DBMS 可用隐含地转换的类型（例如，不同的数值类型或不同的日期类型）
```

#### 17.2.3 包含或取消重复的行

```sql
输入: SELECT user.USER FROM user UNION ALL SELECT global_grants.USER FROM global_grants;
输出:
+------------------+
| USER             |
+------------------+
| root             |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| mysql.infoschema |
| mysql.session    |
| mysql.session    |
| mysql.session    |
| mysql.session    |
| mysql.session    |
| mysql.session    |
| mysql.session    |
| mysql.sys        |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
| root             |
+------------------+
分析: UNION 默认自动去除了重复的行，可使用 UNION ALL 返回所有匹配的行
```

#### 17.2.4 对组合查询结果排序

```sql
输入: SELECT user.USER FROM user UNION SELECT global_grants.USER FROM global_grants ORDER BY USER;
输出:
+------------------+
| USER             |
+------------------+
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
+------------------+
分析: 在用 UNION 组合查询时，只能使用一条 ODER BY 子句，它必须出现在最后一条 SELECT 语句之后。但实际上 MySQL 将用它来排序所有 SELECT 语句返回的所有结果
```

## 第 18 章 全文本搜索

### 18.1 理解全文本搜索

```
在使用全文本搜索时，MySQL 不需要分别查看每个行，不需要分别分析和处理每个词

事务支持：
    InnoDB： 提供事务支持，支持事务的原子性、一致性、隔离性和持久性（ACID 属性）。
    MyISAM： 不支持事务，因此在出现故障或错误时，可能导致数据不一致。
并发性：
    InnoDB： 支持高并发性，具有行级锁定能力，多个事务可以同时处理不同的行。
    MyISAM： 具有表级锁定能力，因此在高并发环境下可能会导致性能瓶颈，一个事务对表的写操作可能会阻塞其他事务。
崩溃恢复：
    InnoDB： 具有崩溃恢复的能力，能够在数据库重新启动后自动进行恢复。
    MyISAM： 在崩溃时可能会导致数据损坏，需要手动进行修复。
外键约束：
    InnoDB： 支持外键约束，可以定义和管理外键。
    MyISAM： 不支持外键约束，外键定义会被忽略。
全文本搜索：
    InnoDB： 支持全文本搜索，可以使用 FULLTEXT 索引进行高效的全文本搜索。
    MyISAM： 专门优化了全文本搜索，性能在这方面可能更好。
表级锁和行级锁：
    InnoDB： 支持行级锁，可以提高并发性，减小锁冲突。
    MyISAM： 支持表级锁，锁定整个表而不是单独的行。
存储方式和索引：
    InnoDB： 数据存储在聚簇索引（主键索引）上，辅助索引实际上是主键索引的一部分。支持自动增量的主键。
    MyISAM： 数据和索引是分开存储的，主键索引和辅助索引是分开的。自动增量的主键可以提高性能。
表空间和缓冲池：
    InnoDB： 具有表空间和缓冲池的概念，支持更精细的内存管理。
    MyISAM： 没有表空间的概念，使用操作系统缓存进行缓存。
```

### 18.2 使用全文本搜索

```
为了进行全文本搜索，必须索引被搜索的列，而且要随着数据的改变不断地重新索引。MySQL 会字段进行所有的索引和重新索引
```

#### 18.2.1 启用全文本搜索支持

```sql
输入: CREATE TABLE articles (id INT PRIMARY KEY, title VARCHAR(255), content TEXT, FULLTEXT(content)) ENGINE = InnoDB;
输出: Query OK, 0 rows affected (0.20 sec)
分析: 在这个案例中，我们创建了一个名为 articles 的表，包含了 id、title 和 content 列。通过在 content 列上使用 FULLTEXT 子句，我们启用了对该列的全文本搜索, ENGINE = InnoDB 是在 MySQL 数据库中用于指定存储引擎的一部分 SQL 语法

注意: 不要在导入数据时使用 FULLTEXT，应该先导入所有数据，然后修改定义表
```

#### 18.2.2 进行全文本搜索

```sql
前提条件创建索引: ALTER TABLE global_grants ADD FULLTEXT(PRIV);

输入: SELECT * FROM global_grants WHERE MATCH(PRIV) AGAINST('SET_USER_ID');
输出:
+------+-----------+-------------+-------------------+
| USER | HOST      | PRIV        | WITH_GRANT_OPTION |
+------+-----------+-------------+-------------------+
| root | localhost | SET_USER_ID | Y                 |
+------+-----------+-------------+-------------------+
分析: MATCH() 指示 MySQL 针对指定的列进行搜索, AGAINST() 指定词作为搜索文本

注意: 
	1. 传递给 MATCH() 的值必须与 FULLTEXT() 定义中的相同，如果指定多个列，则必须列出它们（而且次序正确）
	2. 除非使用 BINARY 方式，否则全文本搜索不区分大小写
	
匹配算法：
    全文本搜索： 使用更复杂的匹配算法，可以处理同义词、词干变化等，并考虑词的相关性。它不仅仅匹配关键词，还会提供相关性评分，使得搜索结果更加精准。
    LIKE 搜索： 使用简单的字符串匹配算法，基于通配符进行模式匹配。它只关注字符串的字面匹配，不考虑词语之间的语义关系。
排序方式：
    全文本搜索： 结果可以根据匹配度、相关性得分等进行排序，使得最相关的结果排在前面。这通常提供更有用和易读的搜索结果。
    LIKE 搜索： 结果的排序通常是按照数据库中存储的顺序，或者是根据索引的排序。不会根据匹配度或相关性对结果进行排序。
性能：
    全文本搜索： 在大型文本数据集中，全文本搜索通常具有更好的性能，因为它使用了全文本索引和高效的搜索算法。这使得全文本搜索适用于处理大量文本数据的场景。
    LIKE 搜索： 对于大型文本数据集，LIKE 搜索可能会导致性能问题，尤其是在没有索引支持的情况下，因为它需要逐行进行字符串匹配。
语义处理：
    全文本搜索： 具有一定的语义处理能力，能够理解词之间的关系，支持同义词、词干处理等。
    LIKE 搜索： 只是进行简单的字符串匹配，不具备语义处理的能力。
适用场景：
    全文本搜索： 适用于需要处理大量自然语言文本的场景，如文章搜索、博客搜索、全文检索等。
    LIKE 搜索： 适用于基于简单字符串模式匹配的场景，如查找以特定前缀或后缀开头的字符串。
```

#### 18.2.3 使用查询扩展

```
询扩展是一种用于改善搜索结果的技术，旨在通过添加或扩展用户原始查询中的相关术语，以提供更全面、准确或相关的搜索结果。该技术的目标是解决用户可能未考虑到的相关概念，从而提高搜索引擎的效果。

主要思想是在用户的查询中引入额外的关键词或术语，以使搜索更加全面，包括与用户原始查询相关的其他概念。这样可以避免搜索引擎仅依赖于用户输入的限定词，而能够更好地理解用户的意图并提供更丰富的搜索结果。

查询扩展的方法可以包括：
    同义词扩展： 引入与用户查询中的词汇相近或同义的其他词汇。
    相关主题扩展： 添加与用户查询相关但可能未明确提及的相关主题。
    近义词扩展： 引入与用户查询中的词汇在语义上相似但可能不完全相同的词汇。
    模糊查询扩展： 考虑到用户查询中可能存在的拼写错误或近似匹配。
    行业术语扩展： 根据用户查询的背景，引入相关领域内的专业术语。
    用户偏好扩展： 考虑用户的个人偏好，根据先前搜索历史或用户属性推断可能感兴趣的领域。
    地理位置扩展： 如果用户查询涉及地理位置，可以扩展为相关地理位置的查询。
    
查询扩展的实施可以基于自然语言处理、机器学习、统计分析等技术。通过这种方式，搜索引擎能够更好地适应用户的搜索需求，提供更丰富和有用的搜索结果。
```

#### 18.2.3 布尔文本搜索

```sql
IN BOOLEAN MODE 指定布尔模式

输入: SELECT * FROM documents WHERE MATCH(title, content) AGAINST('+"database" +"performance"' IN BOOLEAN MODE);
分析: 查找同时包含 "database" 和 "performance" 的文档，'+' 表示必须包含该词

输入: SELECT * FROM documents WHERE MATCH(title, content) AGAINST('+"database" OR +"sql"' IN BOOLEAN MODE);
分析: 查找包含 "database" 或 "sql" 的文档, OR 指示搜索引擎返回包含任一关键词的文档

输入: SELECT * FROM documents WHERE MATCH(title, content) AGAINST('+"database" -"mysql"' IN BOOLEAN MODE);
分析: 查找包含 "database" 但不包含 "mysql" 的文档, "-" 表示不包含该词

输出: SELECT * FROM documents WHERE MATCH(title, content) AGAINST('+"database" +("performance" OR "sql")' IN BOOLEAN MODE);
分析: 查找同时包含 "database" 和 ("performance" 或 "sql") 的文档, 使用括号指定运算符的优先级

其他布尔操作符		说明
>				 包含，而且增加等级值
<				 包含，且减少等级值
~				 取消一个词的排序值
*				 词尾的通配符
""				 定义一个短语（与单个词的列表不一样，它匹配整个短语以便包含或排除这个短语）
```

## 第 19 章 插入数据

### 19.1  数据插入

```
INSERT 是用来插入（或添加）行到数据库表的
```

### 19.2 插入完整的行

```sql
输入: INSERT INTO orders VALUES(22222, '2024-1-16', 10002);
输入: SELECT * FROM orders;
输出: 
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|     20005 | 2005-09-01 |   10001 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10004 |
|     20008 | 2005-10-03 |   10005 |
|     20009 | 2005-10-08 |   10001 |
|     22222 | 2024-01-16 |   10002 |
+-----------+------------+---------+
分析: INSERT INTO 后接表名和要插入的列名（可省略）, VALUES 后接要插入的值，如果某个列没有值则用 NULL 代替

输入: INSERT INTO orders (order_num, order_date, cust_id) VALUES(11111, '2024-1-16', 10002);
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|     11111 | 2024-01-16 |   10002 |
|     20005 | 2005-09-01 |   10001 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10004 |
|     20008 | 2005-10-03 |   10005 |
|     20009 | 2005-10-08 |   10001 |
|     22222 | 2024-01-16 |   10002 |
+-----------+------------+---------+
分析: 这种语法编写的语句更安全

输入: INSERT INTO orders (order_num, order_date, cust_id) VALUES(33333, '2024-1-16', NULL);
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|     11111 | 2024-01-16 |   10002 |
|     20005 | 2005-09-01 |   10001 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10004 |
|     20008 | 2005-10-03 |   10005 |
|     20009 | 2005-10-08 |   10001 |
|     22222 | 2024-01-16 |   10002 |
|     33333 | 2024-01-16 |    NULL |
+-----------+------------+---------+

如果表的定义允许，可用在 INSERT 操作中省略某些列，但必须具备以下条件：
	1. 该列定义为允许 NULL 值
	2. 在表定义中给出默认值
	
可以在 INSERT 和 INTO 之间添加关键字 LOW_PRIORITY，指示 MySQL 降低 INSERT 语句的优先级
```

### 19.3 插入多个行

```sql
输入: INSERT INTO orders (order_num, order_date, cust_id) VALUES(555555, '2024-1-16', NULL);INSERT INTO orders (order_num, order_date, cust_id) VALUES(66666, '2024-1-16', NULL);
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|     11111 | 2024-01-16 |   10002 |
|     20005 | 2005-09-01 |   10001 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10004 |
|     20008 | 2005-10-03 |   10005 |
|     20009 | 2005-10-08 |   10001 |
|     22222 | 2024-01-16 |   10002 |
|     33333 | 2024-01-16 |    NULL |
|     66666 | 2024-01-16 |    NULL |
|    555555 | 2024-01-16 |    NULL |
+-----------+------------+---------+
分析: 多条语句之间只需用分号结束即可

输入: INSERT INTO orders (order_num, order_date, cust_id) VALUES(777, '2024-1-16', 10005), (88888, '2024-1-16', 10005);
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|       777 | 2024-01-16 |   10005 |
|     11111 | 2024-01-16 |   10002 |
|     20005 | 2005-09-01 |   10001 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10004 |
|     20008 | 2005-10-03 |   10005 |
|     20009 | 2005-10-08 |   10001 |
|     22222 | 2024-01-16 |   10002 |
|     33333 | 2024-01-16 |    NULL |
|     66666 | 2024-01-16 |    NULL |
|     88888 | 2024-01-16 |   10005 |
|    555555 | 2024-01-16 |    NULL |
+-----------+------------+---------+
分析：单条语句有多组值，每组值用一对团括号括起来，用逗号分隔
```

### 19.4 插入检索出的数据

```sql
输入: INSERT INTO products (vend_id, prod_name) SELECT vend_id, vend_name FROM vendors;
输入: SELECT * FROM products;
输出:
+---------+---------+----------------+------------+-----------+
| prod_id | vend_id | prod_name      | prod_price | prod_desc |
+---------+---------+----------------+------------+-----------+
|       1 |    1001 | Anvils R Us    |       NULL | NULL      |
|       2 |    1002 | LT Supplies    |       NULL | NULL      |
|       3 |    1003 | ACME           |       NULL | NULL      |
|       4 |    1004 | Furball Inc.   |       NULL | NULL      |
|       5 |    1005 | Jet Set        |       NULL | NULL      |
|       6 |    1006 | Jouets Et Ours |       NULL | NULL      |
+---------+---------+----------------+------------+-----------+
```

## 第 20 章 更新和删除数据

### 20.1 更新数据

```sql
可使用 UPDATE 语句，采用两种方式:
	1. 更新表的特定行
	2. 更新表中所有行
	
UPDATE 语句由 3 部分组成:
	1. 要更新的表
	2. 列名和它们的新值
	3. 确定要更新行的过滤条件
	
输入: UPDATE orders SET cust_id = 10002 WHERE order_num = 66666;
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|       777 | 2024-01-16 |   10005 |
|     11111 | 2024-01-16 |   10002 |
|     20005 | 2005-09-01 |   10001 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10004 |
|     20008 | 2005-10-03 |   10005 |
|     20009 | 2005-10-08 |   10001 |
|     22222 | 2024-01-16 |   10002 |
|     33333 | 2024-01-16 |    NULL |
|     66666 | 2024-01-16 |   10002 |
|     88888 | 2024-01-16 |   10005 |
|    555555 | 2024-01-16 |    NULL |
+-----------+------------+---------+
分析:  UPDATE 后接更新的表名, SET 用来将新值赋给被更新的列

输入: UPDATE orders SET cust_id = 10002, order_date = '2005-02-15' WHERE order_num = 66666;
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|       777 | 2024-01-16 |   10003 |
|     11111 | 2024-01-16 |   10003 |
|     20005 | 2005-09-01 |   10003 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10003 |
|     20008 | 2005-10-03 |   10003 |
|     20009 | 2005-10-08 |   10003 |
|     22222 | 2024-01-16 |   10003 |
|     33333 | 2024-01-16 |   10003 |
|     66666 | 2005-02-15 |   10002 |
|     88888 | 2024-01-16 |   10003 |
|    555555 | 2024-01-16 |   10003 |
+-----------+------------+---------+
分析: 更新多个列时，只需要使用单个 SET 命令，每个 "列 = 值" 对之间用逗号分隔

输入: UPDATE IGNORE orders SET cust_id = 10002, order_date = 2005-02-15 WHERE order_num = 777;
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|       777 | 0000-00-00 |   10002 |
|     11111 | 2024-01-16 |   10003 |
|     20005 | 2005-09-01 |   10003 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10003 |
|     20008 | 2005-10-03 |   10003 |
|     20009 | 2005-10-08 |   10003 |
|     22222 | 2024-01-16 |   10003 |
|     33333 | 2024-01-16 |   10003 |
|     66666 | 2005-02-15 |   10002 |
|     88888 | 2024-01-16 |   10003 |
|    555555 | 2024-01-16 |   10003 |
+-----------+------------+---------+
分析: 如果在更新时出现错误则会取消操作，为即使发生错误也要继续更新可使用关键字 IGNORE, 例如上面的日期 order_date
```

### 20.2 删除数据

```sql
可使用 DELETE 语句，采用两种方法:
	1. 删除特定的行
	2. 删除所有行
	
输入: DELETE FROM orders WHERE order_num = 555555;
输入: SELECT * FROM orders;
输出:
+-----------+------------+---------+
| order_num | order_date | cust_id |
+-----------+------------+---------+
|       777 | 0000-00-00 |   10002 |
|     11111 | 2024-01-16 |   10003 |
|     20005 | 2005-09-01 |   10003 |
|     20006 | 2005-09-12 |   10003 |
|     20007 | 2005-09-30 |   10003 |
|     20008 | 2005-10-03 |   10003 |
|     20009 | 2005-10-08 |   10003 |
|     22222 | 2024-01-16 |   10003 |
|     33333 | 2024-01-16 |   10003 |
|     66666 | 2005-02-15 |   10002 |
|     88888 | 2024-01-16 |   10003 |
+-----------+------------+---------+
```

## 第 21 章 创建和操纵表

### 21.1 创建表

```
一般创建表有两种方式:
	1. 使用具有交互式创建和管理表的工具
	2. 表也可以直接用 MySQL 语句创建
```

#### 21.1.1 表创建基础

```sql
创建新表必须给出以下信息:
	1. 新表的名字，在关键字 CREATE TABLE 之后
	2. 表列的名字和定义，用逗号分隔
	
输入: CREATE TABLE students (student_id INT PRIMARY KEY, name VARCHAR(20), age INT, email VARCHAR(100));
输入: DESCRIBE students;
输出:
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| student_id | int          | NO   | PRI | NULL    |       |
| name       | varchar(20)  | YES  |     | NULL    |       |
| age        | int          | YES  |     | NULL    |       |
| email      | varchar(100) | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
分析:
    CREATE TABLE：这个SQL语句用于创建一个新表。
    students：正在创建的表的名称。在这种情况下，它的名字是students。
    student_id INT PRIMARY KEY：定义一个名为student_id的列，数据类型为INT（整数），并将其指定为主键。主键唯一标识表中的每条记录。
    name VARCHAR(20)：定义一个名为name的列，数据类型为VARCHAR(20)。它可以存储长度最多为20个字符的可变长度字符串，表示学生的名字。
    email VARCHAR(100)：定义一个名为email的列，数据类型为VARCHAR(100)。它可以存储长度最多为100个字符的可变长度字符串，表示学生的电子邮件地址。
    age INT：定义一个名为age的列，数据类型为INT（整数），表示学生的年龄。
```

#### 21.1.2 使用 NULL 值

```sql
输入: CREATE TABLE fool (fool_id INT PRIMARY KEY, name VARCHAR(20) NOT NULL, age INT);
输入: DESCRIBE fool;
输出:
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| fool_id | int         | NO   | PRI | NULL    |       |
| name    | varchar(20) | NO   |     | NULL    |       |
| age     | int         | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
分析：因为 name 列被指定为 NOT NULL, 表示这列不能为空。而 age 未指定所以可以为空， NULL 为默认设置，如果不指定 NOT NULL，则指定为 NULL
```

#### 21.1.3 主键再介绍

```sql
为创建由多个列组成的主键，应该以逗号分隔的列表给出各列名

输入: CREATE TABLE terchar (t_id INT, t_num INT, name VARCHAR(20), PRIMARY KEY(t_id, t_num));
输入: DESCRIBE terchar;
输出: 
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| t_id  | int         | NO   | PRI | NULL    |       |
| t_num | int         | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
```

#### 21.1.4 使用 AUTO_INCREMENT

```sql
AUTO_INCREMENT 告诉 MySQL，本列每当增加一行时自动增量

输入: CREATE TABLE example (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50));
输入: INSERT INTO example (name) VALUES ('John Doe');
输入: INSERT INTO example (name) VALUES ('Jane Smith');
+----+------------+
| id | name       |
+----+------------+
|  1 | John Doe   |
|  2 | Jane Smith |
+----+------------+
分析：在上述例子中，id 列被定义为 INT AUTO_INCREMENT PRIMARY KEY。这意味着每当你插入一行数据时，id 列将自动递增，并且你不需要为它提供值，数据库会自动分配一个唯一的整数。每次插入新的数据行时，id 列都会自动增加，确保每一行都有一个唯一的标识符。
```

#### 21.1.5 指定默认值

```sql
输入: CREATE TABLE clc (id INT PRIMARY KEY, name VARCHAR(20), age INT DEFAULT 18);
输入: INSERT INTO clc (id, name) VALUES(1, '向盼');
输入: SELECT * FROM clc;
输出:
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | 向盼   |   18 |
+----+--------+------+
```

#### 21.1.6 引擎类型

```
1. InnoDB：
事务支持： 提供事务支持，支持 ACID 特性（原子性、一致性、隔离性、持久性）。
行级锁定： 提供行级别的锁定，有助于减小锁定冲突的可能性。
外键支持： 支持外键关系。
崩溃恢复： 具有崩溃恢复能力，数据库崩溃后可以进行恢复。
2. MyISAM：
性能： 对于读操作具有较好的性能，适合读密集型的应用。
全文本索引： 支持全文本索引，适合需要全文搜索功能的应用。
表级锁定： 使用表级锁定，可能导致并发写操作效率较低。
不支持事务： 不支持事务和外键。
3. MEMORY：
内存表： 数据存储在内存中，适合对速度要求很高、但数据量较小的表。
临时表： 通常用于存储临时数据，表在服务器重启时数据丢失。
4. NDB（MySQL Cluster）：
集群： 适用于分布式集群环境，提供高可用性和横向扩展。
分片： 支持数据分片，可以在多个节点上存储数据。
实时性能： 面向实时性能的 OLTP（联机事务处理）工作负载。
5. ARCHIVE：
压缩： 数据以压缩格式存储，适用于存储大量历史数据。
只读： 适合只读的归档数据，不支持更新和删除操作。
6. BLACKHOLE：
转发引擎： 接收写操作但不存储数据，用于转发数据到其他 MySQL 实例。
7. CSV：
CSV 格式： 数据存储在 CSV（逗号分隔值）格式文件中，方便导入导出。
8. FederatedX：
联邦表： 允许查询远程数据库中的表，通过联邦表引擎实现数据访问。
```

### 21.2 更新表

```sql
为更新表定义，可使用 ALTER TABLE 语句

输入: ALTER TABLE clc ADD love VARCHAR(20);
输入: DESCRIBE clc;
输出:
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int         | YES  |     | 18      |       |
| love  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+

另一种用途是定义外键

假设有两个表 orders 和 customers，其中 orders 表包含订单信息，customers 表包含客户信息。我们希望在 orders 表中添加一个外键，将 customer_id 列与 customers 表的 customer_id 列关联起来。

输入: CREATE TABLE customers (customer_id INT PRIMARY KEY, customer_name VARCHAR(50));

输入: CREATE TABLE orders (order_id INT PRIMARY KEY, order_number VARCHAR(20), customer_id INT, FOREIGN KEY (customer_id) REFERENCES customers(customer_id));

上述 SQL 语句中，我们首先创建了 customers 表，然后创建了 orders 表。在 orders 表的 customer_id 列上定义了一个外键，该外键引用了 customers 表的 customer_id 列。这样，orders 表的 customer_id 就成为一个外键，与 customers 表的 customer_id 形成关联，确保在插入或更新数据时，orders 表中的 customer_id 值必须在 customers 表中存在。

如果你已经有了这两个表，可以使用 ALTER TABLE 语句添加外键。假设 orders 表已经存在，你可以这样做：

输入: ALTER TABLE orders ADD CONSTRAINT fk_customer FOREIGN KEY (customer_id) REFERENCES customers(customer_id);

这将在 orders 表上添加一个名为 fk_customer 的外键，与 customers 表的 customer_id 列关联。
```

### 21.3 删除表

```sql
使用 DROP TABLE 即可

输入: DROP TABLE terchar;
输出: Query OK, 0 rows affected (0.09 sec)
```

### 21.4 重命名表

```sql
使用 RENAME TABLE 语句可以重命名一个表

输入: RENAME TABLE clc TO xp;
输入: SHOW TABLES;
输出:
+-----------------------+
| Tables_in_crashcourse |
+-----------------------+
| customers             |
| fool                  |
| orderitems            |
| orders                |
| productnotes          |
| products              |
| students              |
| vendors               |
| xp                    |
+-----------------------+
```

## 第 22 章 使用视图

### 22.1 视图

```
视图是虚拟的表，与包含数据的表不一样，视图只包含使用时动态检索数据的查询
```

#### 22.1.1 为什么使用视图

```
1. 重用 SQL 语句
2. 简化复杂的 SQL 操作
3. 使用表的组成部分而不是整个表
4. 保护数据
5. 更改数据格式和表示
```

#### 22.1.2 视图的规则和限制

```
1. 与表一样，视图必须唯一命名
2. 对于可以创建的视图数目没有限制
3. 为了创建视图，必须具有足够的访问权限
4. 视图可以嵌套，即可以从其他视图中检索数据的查询来构造一个视图
5. ORDER BY 可以用在视图中，但如果从该视图检索数据 SELECT 中也有 ORDER BY，那么该视图中的 ORDER BY 被覆盖
6. 视图不能索引，也不能有关联的触发器或默认值
7. 视图可以和表一起使用
```

### 22.2 使用视图

```
1. 使用 CREATE VIEW 创建视图
2. 使用 SHOW CREATE VIEW 视图名; 查看创建视图的语句
3. DROP VIEW 视图名; 删除视图
4. 更新视图时，可以先 DROP 再用 CREATE 。也可以直接用 CREATE OP REPLACE VIEW, 推荐第二个
```

#### 22.2.1 利用视图简化复杂的联结

```sql
输入: CREATE TABLE orders (order_id INT PRIMARY KEY, order_number VARCHAR(20), customer_name VARCHAR(50));
输入: CREATE TABLE order_items (item_id INT PRIMARY KEY, order_id INT, product_name VARCHAR(50), quantity INT, price DECIMAL(10, 2));

现在，我们可以创建一个视图，将订单信息、商品项以及订单总金额合并：

输入: CREATE VIEW order_summary_view AS SELECT o.order_id, o.order_number, o.customer_name, i.product_name, i.quantity, i.price, i.quantity * i.price AS item_total, SUM(i.quantity * i.price) OVER (PARTITION BY o.order_id) AS order_total FROM orders o JOIN order_items i ON o.order_id = i.order_id;

分析: 
    item_total 计算每个商品项的总金额, SUM(i.quantity * i.price) OVER (PARTITION BY o.order_id) 计算每个订单的总金额
    
    CREATE VIEW order_summary_view AS: 这部分开始创建一个名为 order_summary_view 的新视图。
    
    o.order_id, o.order_number, o.customer_name: 从 orders 表中选择这些列（o 是 orders 表的别名）。
    
    i.product_name, i.quantity, i.price: 从 order_items 表中选择这些列（i 是 order_items 表的别名）。
    
    i.quantity * i.price AS item_total: 计算每个订单中每个商品的总费用。
    
    SUM(i.quantity * i.price) OVER (PARTITION BY o.order_id) AS order_total: 使用窗口函数 SUM 计算每个订单的所有商品的总费用。
    
    FROM orders o JOIN order_items i ON o.order_id = i.order_id: 这指定了用于合并数据的表（orders 和 order_items）和连接条件（o.order_id = i.order_id）。
```

#### 22.2.2 用视图重新格式化检索出的数据

```sql
输入: CREATE TABLE employees (employee_id INT PRIMARY KEY, employee_name VARCHAR(50), department VARCHAR(50), salary DECIMAL(10, 2));

输入: INSERT INTO employees VALUES (1, 'John Doe', 'Sales', 50000.00), (2, 'Jane Smith', 'HR', 60000.00), (3, 'Bob Johnson', 'IT', 75000.00), (4, 'Alice Brown', 'Finance', 55000.00), (5, 'Charlie Davis', 'Sales', 60000.00);

输入: CREATE VIEW formatted_employee_view AS SELECT employee_name AS Name, department AS Department, salary, CASEWHEN salary < 60000 THEN 'Low Salary' WHEN salary >= 60000 AND salary < 70000 THEN 'Medium Salary' ELSE 'High Salary' END AS Salary_Category FROM employees;

分析: 
    CREATE VIEW formatted_employee_view AS: 这部分开始创建一个名为 formatted_employee_view 的新视图。

    employee_name AS Name：将 employee_name 列重命名为 Name。

    department AS Department：将 department 列重命名为 Department。

    salary：保留原始的 salary 列。

    CASE ... END AS Salary_Category：使用 CASE 表达式创建一个新的列 Salary_Category，该列根据工资的不同范围进行分类。

    FROM employees: 这部分指定了数据来源，即我们要从 employees 表中提取数据。

    CASE 表达式:
        WHEN salary < 60000 THEN 'Low Salary'：如果工资小于 60000，则将 Salary_Category 设置为 'Low Salary'。

        WHEN salary >= 60000 AND salary < 70000 THEN 'Medium Salary'：如果工资介于 60000 到 69999 之间，则将 Salary_Category 设置为 'Medium Salary'。

        ELSE 'High Salary'：如果以上条件都不满足，则将 Salary_Category 设置为 'High Salary'。

    最终，这个视图提供了一个新的数据视图，其中包含了重新格式化后的员工信息。Name 和 Department 列提供了更直观的列名，而 Salary_Category 则根据工资范围对员工进行了分类。通过使用视图，我们可以在不修改原始表结构的情况下，轻松地访问经过处理和分类的数据。
```

#### 22.2.3 用视图过滤不想要的数据

```sql
输入: CREATE TABLE products (product_id INT PRIMARY KEY, product_name VARCHAR(50), supplier VARCHAR(50), price DECIMAL(10, 2));

输入: INSERT INTO products VALUES (1, 'Laptop', 'ABC Electronics', 1200.00), (2, 'Smartphone', 'XYZ Tech', 800.00), (3, 'Headphones', 'Audio Co.', 50.00), (4, 'Tablet', 'ABC Electronics', 500.00), (5, 'Camera', 'Phototech', 700.00);

输入: CREATE VIEW filtered_products_view AS SELECT product_id, product_name, supplier, price FROM products WHERE price BETWEEN 500.00 AND 1000.00;

分析: 
    product_id, product_name, supplier, price：选择要包含在视图中的列。

    FROM products：指定了数据来源，即我们要从 products 表中提取数据。

    WHERE price BETWEEN 500.00 AND 1000.00：使用 WHERE 子句过滤价格，只选择价格在 500 到 1000 之间的产品。
    
    这个视图提供了一个过滤后的产品列表，只包含价格在指定范围内的产品。通过使用视图，我们可以轻松地创建一个过滤后的数据视图，以便更方便地获取所需的信息。
```

#### 22.2.4 使用视图与计算字段

```sql
输入: CREATE TABLE sales (sale_id INT PRIMARY KEY, sale_date DATE, product_name VARCHAR(50), quantity INT, unit_price DECIMAL(10, 2));

输入: INSERT INTO sales VALUES (1, '2023-01-01', 'Laptop', 3, 1200.00), (2, '2023-01-02', 'Smartphone', 5, 800.00), (3, '2023-01-02', 'Tablet', 2, 500.00), (4, '2023-01-03', 'Laptop', 1, 1200.00), (5, '2023-01-03', 'Camera', 4, 700.00);

输入: CREATE VIEW sales_summary_view AS SELECT sale_id, sale_date, product_name, quantity, unit_price, quantity * unit_price AS transaction_total, SUM(quantity * unit_price) OVER (PARTITION BY product_name) AS product_total FROM sales;

分析: 
    sale_id, sale_date, product_name, quantity, unit_price：选择要包含在视图中的基本销售信息列。

    quantity * unit_price AS transaction_total：计算每个销售事务的总销售额。

    SUM(quantity * unit_price) OVER (PARTITION BY product_name) AS product_total：使用窗口函数 SUM 计算每个产品的总销售额。
    
    这个视图提供了每个销售事务的总销售额和每个产品的销售总额。通过使用视图，我们可以方便地在数据中添加计算字段，而不必在每次查询时都进行繁琐的计算操作。
```

## 第 23 章 使用存储过程

### 23.1 存储过程

```
存储过程简单来说，就是为一行的使用而保存的一条或多条 MySQL 语句的集合
```

### 23.2 为什么要使用存储过程

```
1. 通过把处理封装在容易使用的单元中，简化了复杂的操作
2. 由于不要求反复建立一系列处理步骤，这保证了数据的完整性
3. 简化对变动的管理
4. 提高性能
5. 存在一些只能用在单个请求中的 MySQL 元素和特性，存储过程可以使用它们来编写功能更强更灵活的代码
```

### 23.3 使用存储过程

```
使用存储过程需要知道如何执行（运行）它们
```

#### 23.3.1 执行存储过程

```sql
输入: CALL GetEmployeesByDepartment('Sales');
分析: 
    CALL 语句：用于调用存储过程的 SQL 关键字。
    存储过程名称：即被调用的存储过程的名称，这里是 GetEmployeesByDepartment。
    参数传递：如果存储过程定义了参数，你需要提供相应的参数值。在这个例子中，存储过程接受一个名为 department_name 的参数，我们将 'Sales' 作为参数传递给它。
    执行这个 CALL 语句后，存储过程会执行其定义的逻辑，即在 employees 表中选择符合指定部门的员工列表。结果将被返回，你可以看到符合条件的员工信息。
```

#### 23.3.2 创建存储过程

```sql
输入: DELIMITER // CREATE PROCEDURE AddTwoNumbers(IN num1 INT, IN num2 INT, OUT result INT) BEGIN SET result = num1 + num2; END // DELIMITER ;
分析:
    CREATE PROCEDURE AddTwoNumbers(：这是创建存储过程的开始部分，定义了存储过程的名称为 AddTwoNumbers。

    IN num1 INT, IN num2 INT, OUT result INT：在括号中定义了存储过程的参数列表。IN 表示输入参数，OUT 表示输出参数。我们有两个输入参数 num1 和 num2，以及一个输出参数 result。

    BEGIN：表示存储过程的开始，后面是存储过程的实际逻辑。

    SET result = num1 + num2;：在存储过程的逻辑部分，执行了一个简单的加法操作，将输入参数 num1 和 num2 的和赋值给输出参数 result。

    END //：表示存储过程的结束。

    DELIMITER ;：将语句分隔符恢复为默认的分号，以结束 DELIMITER // 设置。

    这个存储过程非常简单，它的作用是接受两个整数参数，将它们相加，并将结果存储在输出参数中。这只是一个演示用例，实际中的存储过程可能包含更复杂的业务逻辑、条件判断、循环等。
```

#### 23.3.3 删除存储过程

```sql
输入: DROP PROCEDURE IF EXISTS AddTwoNumbers;
分析: 这个语句用于删除存储过程。IF EXISTS 部分是可选的，它确保只有在存在该存储过程时才尝试删除，防止出现错误
```

#### 23.3.4 使用参数

```sql
输入: CREATE TABLE employees (employee_id INT PRIMARY KEY, employee_name VARCHAR(50), department VARCHAR(50), salary DECIMAL(10, 2));
输入: INSERT INTO employees VALUES(1, 'John Doe', 'Sales', 60000.00), (2, 'Jane Smith', 'HR', 55000.00), (3, 'Bob Johnson', 'IT', 70000.00), (4, 'Alice Brown', 'Finance', 65000.00), (5, 'Charlie Davis', 'Sales', 62000.00);
输入: DELIMITER // CREATE PROCEDURE GetEmployees(IN department_name VARCHAR(50), IN salary_range DECIMAL(10, 2)) BEGIN SELECT * FROM employees WHERE department = department_name AND salary >= salary_range; END // DELIMITER ;
分析: 
    IN department_name VARCHAR(50)：表示输入参数，用于传递部门名称。
    IN salary_range DECIMAL(10, 2)：表示输入参数，用于传递薪水范围。
```

#### 23.3.5 建立智能存储过程

```sql
输入: CREATE TABLE orders (order_id INT PRIMARY KEY, order_date DATE, total_amount DECIMAL(10, 2));
输入: INSERT INTO orders VALUES(1, '2023-01-01', 1200.00), (2, '2023-01-02', 800.00), (3, '2023-01-03', 500.00), (4, '2023-01-04', 1500.00), (5, '2023-01-05', 900.00);
输入: DELIMITER // CREATE PROCEDURE SmartOrderStatus(IN order_id INT, OUT status_message VARCHAR(100)) BEGIN DECLARE order_total DECIMAL(10, 2); SELECT total_amount INTO order_total FROM orders WHERE order_id = order_id; IF order_total >= 1000.00 THEN SET status_message = 'High value order. Expedited processing.'; ELSE SET status_message = 'Standard processing for regular order.'; END IF;
END // DELIMITER ;
分析: 在存储过程中，我们首先声明了一个局部变量 order_total 用于存储订单总额。然后，通过查询从 orders 表中获取相应订单号的订单总额。最后，根据订单总额的不同，设置不同的状态消息

输入: CALL SmartOrderStatus(4, @status_message);
输入: SELECT @status_message AS StatusMessage;
分析: 在这个例子中，我们使用 CALL 语句调用 SmartOrderStatus 存储过程，传递订单号为 4 的参数。存储过程会根据订单总额的不同设置相应的状态消息，并将消息存储在输出参数 status_message 中。最后，我们通过 SELECT 语句查询输出参数的值
```

#### 23.3.6 检查存储过程

```sql
输入: SHOW CREATE PROCEDURE 存储名

获得更加详细信息: SHOW PROCEDURE STATUS
```

## 第 24 章 使用游标

### 24.1 游标

```
主要用于交互式应用，其中用户需要滚动屏幕上的数据，并对数据进行浏览或做出更改
```

### 24.2 使用游标

```
1. 使用前必须定义它
2. 一旦声明后，必须打开游标使用
3. 对于填有数据的游标，必须检索各行
4. 在结束游标使用时，必须关闭游标
```

#### 24.2.1 创建游标

```sql
输入: CREATE PROCEDURE processorders() BEGIN DECLARE ordernumbers CURSOR FOR SELECT order_num FROM orders; END;
分析: DECLARE 语句用来定义和命名游标，这里为 ordernumbers。存储过程处理完成后，游标就消失（因为它局限于存储过程）
```

#### 24.2.2 打开和关闭游标

```sql
输入: OPEN ordernumbers;
分析: 在处理 OPEN 语句时执行查询，存储检索出的数据以供浏览和滚动

输入: CLOSE ordernumbers;
分析: CLOSE 释放游标使用的所有内部内存和资源，因此在每个游标不再需要时都应该关闭
```

#### 24.2.3 使用游标数据

```sql
输入: CREATE TABLE orders (order_id INT PRIMARY KEY, order_num INT, customer_id INT, order_date DATE, total_amount DECIMAL(10, 2));
输入: INSERT INTO orders VALUES(1, 101, 1, '2023-01-01', 1200.00), (2, 102, 2, '2023-01-02', 800.00), (3, 103, 1, '2023-01-03', 500.00), (4, 104, 3, '2023-01-04', 1500.00), (5, 105, 2, '2023-01-05', 900.00);
输入: DELIMITER // CREATE PROCEDURE CalculateCustomerTotalAmount() BEGIN DECLARE done INT DEFAULT FALSE; DECLARE customer_id INT; DECLARE total_amount DECIMAL(10, 2); DECLARE customer_orders CURSOR FOR SELECT DISTINCT customer_id FROM orders; DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE; CREATE TEMPORARY TABLE IF NOT EXISTS temp_customer_totals (customer_id INT, total_amount DECIMAL(10, 2)); OPEN customer_orders; customer_loop: LOOP FETCH customer_orders INTO customer_id; IF done THEN LEAVE customer_loop; END IF; SELECT SUM(total_amount) INTO total_amount FROM orders WHERE customer_id = customer_id; INSERT INTO temp_customer_totals VALUES (customer_id, total_amount); END LOOP; CLOSE customer_orders; SELECT * FROM temp_customer_totals; DROP TEMPORARY TABLE IF EXISTS temp_customer_totals;
END // DELIMITER ;
分析:
    DELIMITER //：设置语句定界符为 //，用于处理存储过程中的分号问题。

    CREATE PROCEDURE CalculateCustomerTotalAmount()：创建存储过程，命名为 CalculateCustomerTotalAmount。

    DECLARE done INT DEFAULT FALSE;：声明变量 done，用于检测游标是否遍历结束。

    DECLARE customer_id INT;：声明变量 customer_id，用于存储从游标中获取的客户ID。

    DECLARE total_amount DECIMAL(10, 2);：声明变量 total_amount，用于存储计算的订单总金额。

    DECLARE customer_orders CURSOR FOR SELECT DISTINCT customer_id FROM orders;：声明游标 customer_orders，遍历不同的客户ID。

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;：声明异常处理条件，当游标遍历结束时，设置 done 变量为 TRUE。

    CREATE TEMPORARY TABLE IF NOT EXISTS temp_customer_totals (...)：创建临时表 temp_customer_totals，用于存储计算结果。

    OPEN customer_orders;：打开游标。

    customer_loop: LOOP：开始一个带标签的循环，标签为 customer_loop。

    FETCH customer_orders INTO customer_id;：从游标中获取客户ID。

    IF done THEN LEAVE customer_loop; END IF;：检查是否遍历结束，如果是，跳出循环。

    SELECT SUM(total_amount) INTO total_amount FROM orders WHERE customer_id = customer_id;：计算每个客户的订单总金额。

    INSERT INTO temp_customer_totals VALUES (customer_id, total_amount);：将计算结果插入到临时表。

    END LOOP;：结束循环。

    CLOSE customer_orders;：关闭游标。

    SELECT * FROM temp_customer_totals;：输出计算结果。

    DROP TEMPORARY TABLE IF EXISTS temp_customer_totals;：删除临时表。

    DELIMITER ;：恢复语句定界符为分号。

存储过程的执行流程：
	1. 打开游标。
	2. 通过循环遍历不同的客户ID。
	3. 对于每个客户ID，计算其订单总金额并插入临时表。
	4. 关闭游标。
	5. 输出计算结果。
	6. 删除临时表。
```

## 第 25 章 使用触发器

### 25.1 触发器

```
触发器是 MySQL 响应以下任意语句而自动执行的一条 MySQL 语句
```

### 25.2 创建触发器

```sql
在创建触发器时，需要给出 4 条信息:
	1. 唯一的触发器名
	2. 触发器关联的表
	3. 触发器应该响应的活动
	4. 触发器何时执行

输入: CREATE TRIGGER newproduct AFTER INSERT ON products FOR EACH ROW SELECT 'Product added';
分析: 
	CREATE TRIGGER 创建名为 newproduct 
	
	AFTER INSERT ON products：指定触发器在 products 表插入操作之后触发。

	FOR EACH ROW：表示触发器对每一行进行操作。
	
	SELECT 'Product added';：在每次插入后执行的逻辑，即输出字符串 'Product added'。
```

### 25.3 删除触发器

```sql
输入: DROP TRIGGER newproduct;
分析: 触发器不能更新或覆盖，为了修改一个触发器必须先删除它
```

### 25.4 使用触发器

```
有了前面的基础后，我们现在来看所支持的每种触发器类型以及它们的差别
```

#### 25.4.1 INSERT 触发器

```sql
输入: DELIMITER // CREATE TRIGGER after_insert_product AFTER INSERT ON products FOR EACH ROW BEGIN INSERT INTO audit_log (action_type, product_id) VALUES ('INSERT', NEW.product_id); END // DELIMITER ;
分析:
    AFTER INSERT ON products：指定触发器在 products 表插入操作之后触发。
    
    FOR EACH ROW：表示触发器对每一行进行操作。
    
    BEGIN ... END：包裹触发器的执行逻辑。
    
    INSERT INTO audit_log ...：在每次插入后执行的逻辑，即将插入操作记录到 audit_log 表中。
```

#### 25.4.2 DELETE 触发器

```sql
输入: DELIMITER // CREATE TRIGGER after_delete_product AFTER DELETE ON products FOR EACH ROW BEGIN INSERT INTO audit_log (action_type, product_id) VALUES ('DELETE', OLD.product_id); END // DELIMITER ;
分析:
    AFTER DELETE ON products：指定触发器在 products 表删除操作之后触发。
    
    FOR EACH ROW：表示触发器对每一行进行操作。
    
    BEGIN ... END：包裹触发器的执行逻辑。
    
    INSERT INTO audit_log ...：在每次删除后执行的逻辑，即将删除操作记录到 audit_log 表中。
```

#### 25.4.3 UPDATE 触发器

```sql
输入: DELIMITER // CREATE TRIGGER after_update_product AFTER UPDATE ON products FOR EACH ROW BEGIN INSERT INTO audit_log (action_type, product_id) VALUES ('UPDATE', NEW.product_id); END // DELIMITER ;
分析:
    AFTER UPDATE ON products：指定触发器在 products 表更新操作之后触发。
    FOR EACH ROW：表示触发器对每一行进行操作。
    BEGIN ... END：包裹触发器的执行逻辑。
    INSERT INTO audit_log ...：在每次更新后执行的逻辑，即将更新操作记录到 audit_log 表中。
```

## 第 26 章 管理事务处理

### 26.1 事务处理

```
事务处理可以用来维护数据库的完整性，它保证成批的 MySQL 操作要么完全执行，要么完全不执行
```

### 26.2 控制事务处理

```sql
管理事务处理的关键在于将 SQL 语句分解为逻辑块，并明确规定数据何时应该回退，何时不应该回退。使用下面语句标识事务的开始

输入: START TRANSACTION
```

#### 26.2.1 使用 ROLLBACK 及 COMMIT

```sql
-- 开始事务
START TRANSACTION;

-- 在事务中执行一系列 SQL 语句
INSERT INTO products (product_id, product_name, price) VALUES (1, 'Product A', 100.00);
UPDATE products SET price = 120.00 WHERE product_id = 1;

-- 检查是否满足某个条件，如果不满足则回滚事务
IF some_condition THEN
  ROLLBACK;
ELSE
  -- 提交事务
  COMMIT;
END IF;

分析:
    使用 START TRANSACTION; 开始一个事务。

    执行一系列 SQL 语句，包括插入和更新。

    检查某个条件（some_condition），如果条件不满足，则执行 ROLLBACK; 将事务回滚。

    如果条件满足，则执行 COMMIT; 提交事务，使之前的 SQL 操作生效。
```

#### 26.2.2 使用保留点

```sql
输入: SAVEPOINT delect1;
分析: 每个保留点都取标识它的唯一名字

输入: ROLLBACK TO delect1;
分析: 回退到保留点
```

#### 26.2.3 更改默认的提交行为

```sql
输入: SET AUTOCOMMIT = 0;
分析: AUTOCOMMIT 标志决定是否自动提交更改，不管有没有 COMMIT 语句。0 为不自动提交
```

## 第 27 章 全球化和本地化

### 27.1 字符集和校对顺序

```
字符集为字母和符合的集合
编码为某个字符集成员的内部表示
校对为规定字符如何比较的指令
```

### 27.2 使用字符集和校对顺序

```sql
输入: SHOW CHARACTER SET;
分析: 这条语句显示所有可用的字符集以及每个字符集的描述和默认校对

输入: SHOW COLLATION;
分析: 此语句显示所有可用的校对，以及它们适用的字符集

可在表创建时指定字符集和校对
```

## 第 28 章 安全管理

### 28.1 访问控制

```
MySQL 服务器的安全基础是: 用户应该对他们需要的数据具有适当的访问权，既不能多也不能少
```

### 28.2 管理用户

```
MySQL 用户账号和信息存储在名为 mysql 的库中
```

#### 28.2.1 创建用户账号

```sql
输入: CREATE USER ben IDENTIFIED BY "passwd";
分析: 
    CREATE USER 创建一个新用户账号名为 ben。
    IDENTIFIED BY "passwd"：指定用户的密码为 "passwd"。用户在连接到 MySQL 时需要提供这个密码以进行身份验证。
    
输入: RENAME USER ben TO xp;
分析: RENAME USER 重命名用户账号
```

#### 28.2.2 删除用户账号

```sql
输入: DROP USER xp;
分析: DROP USER 删除用户账号
```

#### 28.2.3 设置访问权限

```sql
输入: SHOW GRANTS FOR xp;
分析: SHOW GRANTS FOR 查看用户权限

为设置权限，使用 GRANT 语句至少给出以下信息:
	1. 要授予的权限
	2. 被授予访问权限的数据库或表
	3. 用户名

输入: GRANT SELECT ON crashcourse.* TO xp;
分析: 此 GRANT 允许用户在 crashcourse 库上所有表使用 SELECT 。只有通过 SELECT 才有只读权限

输入: REVOKE SELECT ON crashcourse.* FROM xp;
分析: 这条 REVOKE 语句取消刚赋予用户 xp 的 SELECT 权限

全局权限：
    ALL PRIVILEGES：赋予用户所有权限，相当于 GRANT ALL.

    CREATE USER：允许用户创建、更改和删除账户。

    FILE：允许用户读写文件。

    PROCESS：允许用户查看和终止其他用户的进程。

    RELOAD：允许用户使用 FLUSH 命令。

    SHOW DATABASES：允许用户查看所有数据库。

    SHUTDOWN：允许用户关闭数据库服务器。

    SUPER：允许用户执行一些特殊的管理操作，如更改全局系统变量。

数据库权限：
    CREATE：允许用户创建新的数据库。

    ALTER：允许用户修改数据库结构，例如添加或删除列。

    DROP：允许用户删除数据库。

    INDEX：允许用户创建和删除索引。

    SELECT：允许用户查询数据库中的数据。

    INSERT：允许用户向数据库中插入新的行。

    UPDATE：允许用户更新数据库中的数据。

    DELETE：允许用户删除数据库中的行。

    REFERENCES：允许用户在外键中使用表。

表权限：
    CREATE：允许用户创建新的表。

    ALTER：允许用户修改表结构，例如添加或删除列。

    DROP：允许用户删除表。

    INDEX：允许用户创建和删除索引。

    SELECT：允许用户查询表中的数据。

    INSERT：允许用户向表中插入新的行。

    UPDATE：允许用户更新表中的数据。

    DELETE：允许用户删除表中的行。

    REFERENCES：允许用户在外键中使用表。

列权限：
    SELECT：允许用户查询特定列的数据。

    INSERT：允许用户向特定列插入新的值。

    UPDATE：允许用户更新特定列的值。

    REFERENCES：允许用户在外键中引用特定列。
```

#### 28.2.4 更改口令

```sql
输入: SET PASSWORD FOR xp = Password("new_passwd");
分析: SET PASSWORD FOR 更新用户口令，新口令必须传递到 Password() 函数进行加密
```

## 第 29 章 数据库维护

### 29.1 备份数据

```sql
1. 使用命令行实用程序 mysqldump 转储所有数据库内容到某个外部文件
2. 可以使用命令行 MySQL 的 BACKUP TABLE 或 SELECT INTO OUTFILE 转储所有数据到某个外部文件
3. 可用命令行实用程序 mysqlhotcopy 从一个数据库复制所有数据
```

### 29.2 进行数据库维护

```sql
输入: ANALYZE TABLE xp;
输出:
+----------------+---------+----------+----------+
| Table          | Op      | Msg_type | Msg_text |
+----------------+---------+----------+----------+
| crashcourse.xp | analyze | status   | OK       |
+----------------+---------+----------+----------+
分析: ANALYZE TABLE 用来检查表键是否正确

输入: CHECK TABLE xp;
输出:
+----------------+-------+----------+----------+
| Table          | Op    | Msg_type | Msg_text |
+----------------+-------+----------+----------+
| crashcourse.xp | check | status   | OK       |
+----------------+-------+----------+----------+
分析: CHECK TABLE 用来针对许多问题对表进行检查
```

### 29.3 诊断启动问题

```sql
服务器启动问题通常在对MySQL配置或服务器本身进行更改时出现。
MySQL在这个问题发生时报告错误，但由于多数MySQL服务器是作为系统进程或服务自动启动的，这些消息可能看不到。
在排除系统启动问题时，首先应该尽量用手动启动服务器。
MySQL 服务器自身通过在命令行上执行mysqld启动。
下面是几个重要的mysqld 命令行选项：
    --help			显示帮助
    --safe-mode		装载减去某些最佳配置的服务器
    --verbose		显示全文本消息
    --versionn		显示版本信息然后退出
```

### 29.4 查看日志文件

```
错误日志（Error Log）：
    文件名：通常为 hostname.err，例如 myserver.err。
    作用：记录 MySQL 服务器在启动、运行过程中的错误信息，包括警告和致命错误。

查询日志（Query Log）：
    文件名：通常为 hostname.log，例如 myserver.log。
    作用：记录所有 MySQL 服务器接收到的每个查询语句，对于分析和调试查询性能非常有用。

慢查询日志（Slow Query Log）：
    文件名：通常为 hostname-slow.log，例如 myserver-slow.log。
    作用：记录执行时间超过阈值的查询语句，用于识别和优化性能较差的查询。

二进制日志（Binary Log）：
    文件名：通常为 hostname-bin.nnnnnn，例如 myserver-bin.000001。
    作用：记录对数据库的更改，包括插入、更新和删除操作，用于主从复制和点播恢复。

中继日志（Relay Log）：
    文件名：通常为 hostname-relay-bin.nnnnnn，例如 myserver-relay-bin.000001。
    作用：在主从复制中，中继日志用于保存主服务器上二进制日志的副本，用于从服务器的复制进程。

错误追踪日志（General Query Log）：
    文件名：通常为 hostname.log，例如 myserver.log。
    作用：记录所有连接和执行的查询，适用于排查数据库连接问题。
```



## 第 30 章 训练场

### 30.1 刷题网站

```
1. SQLZoo			https://sqlzoo.net
2. SQLBolt			https://sqlbolt.com
3. SQL Fiddle		https://sqlfiddle.com
4. 力扣			  https://leetcode/cn
5. 牛客网			 https://www.nowcoder.com
```

