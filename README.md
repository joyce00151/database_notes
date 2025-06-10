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
收获：
