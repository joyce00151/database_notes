《数据库原理与应用》课程学习记录

记录每周学习内容和收获

课件notes见[database notes](notes.pdf)

* Week1 intro

学习内容：

1.从文件处理系统到数据库系统，区别与联系，什么情境选用DBMS

2.常见的数据模型

3.数据库的schema

4.数据库语言可以分为DDL（data-definition-language，如CREATE TABLE）和DML（data-manipulation language，如SELECT-FROM-WHERE）

收获：

1.阅读《Database System Concepts》部分内容，了解文件处理系统的缺点
（数据冗余与不一致、数据隔离和并发访问异常等），认识这些问题如何推动数据库系统的发展

2.下载PG和Datagrip，编写简单的CREATE TABLE语句

3.了解原子性概念：原子的特性是不可再分，原子性保障了数据的一致性。

* Week2 relational model

学习内容：

1.理解关系数据库的结构，tuple，attribute和relation的对应关系（与table中row和column的概念作类比）

2.候选码和超码的区别，最小超码的唯一性确保数据可区分

3.理解关系代数中的select，project和join等操作，笔记见[relational model](relational-models-notes.pdf)

收获：
1.连接到PostgreSQL数据库，创建university schema中的instructor和department等关系

2.尝试定义主码和外码，解决外码引用时的错误

3.用SQL实现笛卡尔积和natural join，验证了union和difference的相容性要求

* Week3 SQL

学习内容：

1.常见的数据库定义和操作语句，如DDL的基本数据类型和模式定义

2.null的意义：未知或不存在

3.drop table 和 delete from 的区别

收获：

1.实践学习到的语句，练习DML中的select，from，where查询逻辑，尝试between，！=和order by等操作

2.使用as更名优化输出

* Week4 lab

实践：PostgreSQL 环境搭建与数据操作实验

成功在 Windows 系统中部署 PostgreSQL 环境，掌握了通过 SQL Shell 和 pgAdmin 操作数据库

实现内容：

1.数据导入（使用 COPY 命令完成大批量导入测试）

2.基本查询与高级查询：如嵌套查询、聚合函数结合 GROUP BY 和 HAVING

3.字符串处理、布尔值、模糊查询、连接符 || 等细节掌握

* Week 5 null-aggregate

学习内容：

1.Boolean中null表示unknown，在查询结果中false和unknown不出现

2.在PG中实践聚集函数（max、min、avg、count、sum）

3.练习group by和having，验证分组和条件筛选逻辑

4.嵌套子查询中，用 IN/NOT IN 和 >some/>all 编写查询，比较了 =some 与 in 的等价性，还尝试标量子查询和 EXISTS 优化复杂查询

收获：

1.用WITH子句定义临时关系可以简化多表查询

2.涉及到聚集函数有很多invalid的warning，可从底层逻辑理解为什么invalid，查询时需注意语法

* Week 6 change

学习内容：

1.SQL的增、删、改操作，理解DELETE、INSERT 和 UPDATE 的语法及应用场景，区分DELETE（删除数据）和 DROP（删除表）的差异。

2.使用UPDATE结合CASE语句，根据条件批量更新salary字段

3.使用ALTER TABLE为表添加description列并设置默认值null

收获：

1.可用COPY命令从csv文件批量导入数据，显著提升效率

2.掌握PG中的增删改操作

3.自行探索RANK函数，编写查询对课程学分credit进行排名
