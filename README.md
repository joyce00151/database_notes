《数据库原理与应用》课程学习记录

记录每周学习内容和收获

课件notes见[database notes](notes.pdf)

# Week1 intro

## 学习内容：

1.从文件处理系统到数据库系统，区别与联系，什么情境选用DBMS

2.常见的数据模型

3.数据库的schema

4.数据库语言可以分为DDL（data-definition-language，如CREATE TABLE）和DML（data-manipulation language，如SELECT-FROM-WHERE）

## 收获：

1.阅读《Database System Concepts》部分内容，了解文件处理系统的缺点
（数据冗余与不一致、数据隔离和并发访问异常和原子性问题），认识这些局限如何推动DBMS的发展，特别是在管理管理高价值、大规模、多用户访问数据时的必要性。

2.下载PostgreSQL和Datagrip，编写简单的CREATE TABLE语句，例如定义简单的university schema，调试过程中解决字段类型定义的错误。

3.了解原子性概念：原子的特性是不可再分，保障了数据的一致性。

## 拓展
阅读CSDN博客[数据库与文件系统](https://blog.csdn.net/hiddpy/article/details/80817184)

# Week2 relational model

## 学习内容：

1.理解关系数据库的结构，tuple，attribute和relation的对应关系（与table中row和column的概念作类比）

2.schema,例如instructor(ID, name, dept_name, salary)

2.key(超码、候选码、主码、外码），尤其是候选码和超码的区别，最小超码的唯一性确保数据可区分

3.理解关系代数中的select、project、笛卡尔积、join、natural join、union、intersect、difference等操作，笔记见[relational model](relational-models-notes.pdf)

## 收获：

1.连接到PostgreSQL数据库，创建university schema中的instructor和department等关系

2.尝试定义主码和外码，解决外码引用时的错误

3.用SQL实现笛卡尔积和natural join，验证了union和difference的相容性要求

## 拓展
阅读GeeksforGeeks上的关系代数文章[Introduction of Relational Algebra in DBMS](https://www.geeksforgeeks.org/introduction-of-relational-algebra-in-dbms/)，结合示例加深了对操作的理解

# Week3 SQL

## 学习内容：

1.SQL DDL：基本数据类型（数值、字符串、null），模式定义（CREATE TABLE），删除（DROP TABLE、DELETE FROM）

2.SQL DML：SELECT、FROM、WHERE子句，过滤（between、!=、<>、LIKE），排序（ORDER BY），更名（AS）

## 收获：

1.理解了DDL的基本数据类型（如数值、字符串、null）和模式定义

2.在DML部分，重点练习select、from、where的查询逻辑，尝试了between、!=和order by等操作，验证查询结果的正确性

3.理解null的意义：未知或不存在，如何影响查询

# Week4 lab

## 实践：PostgreSQL 环境搭建与数据操作实验

成功在 Windows 系统中部署 PostgreSQL 环境，掌握了通过 SQL Shell 和 pgAdmin 操作数据库

## 实现内容：

1.数据导入（使用 COPY 命令完成大批量导入测试）

2.基本查询与高级查询：如嵌套查询、聚合函数结合 GROUP BY 和 HAVING

3.字符串处理、布尔值、模糊查询、连接符 || 等细节掌握

# Week 5 null-aggregate

## 学习内容：

1.Boolean中null表示unknown，在查询结果中false和unknown不出现

2.在PG中实践聚集函数（max、min、avg、count、sum）

3.练习group by和having，验证分组和条件筛选逻辑

4.嵌套子查询中，用 IN/NOT IN 和 >some/>all 编写查询，比较了 =some 与 in 的等价性，还尝试标量子查询和 EXISTS 优化复杂查询

## 收获：

1.用WITH子句定义临时关系可以简化多表查询

2.涉及到聚集函数有很多invalid的warning，可从底层逻辑理解为什么invalid，查询时需注意语法

# Week 6 change

## 学习内容：

1.SQL的增、删、改操作，理解DELETE、INSERT 和 UPDATE 的语法及应用场景，区分DELETE（删除数据）和 DROP（删除表）的差异。

2.使用UPDATE结合CASE语句，根据条件批量更新salary字段

3.使用ALTER TABLE为表添加description列并设置默认值null

## 收获：

1.可用COPY命令从csv文件批量导入数据，显著提升效率

2.掌握PG中的增删改操作

3.自行探索RANK函数，编写查询对课程学分credit进行排名

# Week 7 join

## 学习内容：

1.理解NATURAL JOIN 的自动匹配机制和 JOIN USING/ON 的灵活性，INNER JOIN 与 OUTER JOIN 的区别。可以通过集合A和集合B交、并的关系理解join。

2.可创建索引优化查询速度

## 收获：

1.在PG中用join on连接instructor和department表，解决重复属性问题，并用left outer join保留未匹配数据。

2.创建视图faculty，通过CREATE VIEW简化查询，验证视图的虚拟表特性。

# week8-advanced
  
进入高级数据库的学习，包括高级数据类型和授权机制。

## 学习内容：

1.日期/时间类型

2.interval的用法

3.与AI讨论serial类型在自增主键中的应用，可以优化表设计

4.用GRANT语句为用户分配查询权限，用CREATE ROLE创建角色。

## 收获：

1.在PG中实践 EXTRACT(field FROM timestamp) 提取日期字段，并用 :: 进行类型转换，如 to_date('2025-05-11', 'YYYY-MM-DD')，解决了格式转换问题

2.针对精度问题，用numeric类型替代float，在小数点精度敏感的问题（如金融数据场景）比较重要。

3.to_char() 格式化日期输出，编写复杂查询结合 interval 统计时间跨度

# week9-advanced

## 学习内容：

1.函数、过程和触发器的应用，FUNCTION 返回结果与 PROCEDURE 执行操作的区别

2.与AI讨论SQL注入攻击

## 收获：

1.在PG中创建了 FUNCTION 计算课程平均学分

2.定义TRIGGER，自动记录 instructor 表薪资更新日志，验证触发器的自动化执行效果

3.用 Python 的 psycopg2 连接 PostgreSQL，编写脚本批量插入数据

# Week10-design

## 学习内容：

1.实体集（如 instructor、student）与联系集（如 advisor）的定义，以及属性类型（简单/复合、单值/多值、派生）

2.One-to-Many 和 Many-to-Many 映射的区别，箭头表示法

## 收获：

1.使用 draw.io 绘制 university 数据库的 E-R 图，并与datagrip中的E-R图进行比对

2.如何将E-R图转化为关系模式。去除冗余属性并合并模式

# week 11-norm

## 学习内容：

1.1NF、3NF 和 BCNF 的定义及无损分解的重要性

2.函数依赖（如 ID→name）和闭包推导（如 A→B，B→C 推 A→C）

## 收获：

1.学会验证是否满足BCNF

2.理解BCNF和3NF之间需要权衡

# week 12-theory

理论学习，数据库如何存储以及索引机制

## 学习内容：

1.磁盘存储模型，以及堆文件、树文件、顺序文件和哈希文件的组织方式

2.B+树索引，提升数据检索效率

3.稠密索引vs稀疏索引，聚集索引vs非聚集索引，不同的使用场景

## 收获：

1.理解DBMS 如何将数据组织为 pages

2.行存储和列存储在不同查询场景下的效率差异
