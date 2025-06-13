# 《数据库原理与应用》课程学习记录
- 记录每周学习内容和收获
- 课件notes见[database notes](notes.pdf)
- 作业见[DB homework](https://github.com/joyce00151/database_homework))

# 参考材料
- [Database-System-Concepts-7th-Edition](Database-System-Concepts-7th-Edition.pdf)
- [Database Systems
CMU 15-445/645 — Spring 2025](https://15445.courses.cs.cmu.edu/spring2025/)

# Week1 intro

## 学习内容：
- 1.从文件处理系统到数据库系统，区别与联系，什么情境选用DBMS
- 2.常见的数据模型
- 3.数据库的schema
- 4.数据库语言可以分为DDL（data-definition-language，如CREATE TABLE）和DML（data-manipulation language，如SELECT-FROM-WHERE）

## 收获：
- 1.阅读《Database System Concepts》部分内容，了解文件处理系统的缺点
（数据冗余与不一致、数据隔离和并发访问异常和原子性问题），认识这些局限如何推动DBMS的发展，特别是在管理管理高价值、大规模、多用户访问数据时的必要性。
- 2.下载PostgreSQL和Datagrip，编写简单的CREATE TABLE语句，例如定义简单的university schema，调试过程中解决字段类型定义的错误。
- 3.了解原子性概念：原子的特性是不可再分，保障了数据的一致性。

## 拓展
阅读CSDN博客[数据库与文件系统](https://blog.csdn.net/hiddpy/article/details/80817184)

# Week2 relational model

## 学习内容：
- 1.理解关系数据库的结构，tuple，attribute和relation的对应关系（与table中row和column的概念作类比）
- 2.schema,例如instructor(ID, name, dept_name, salary)
- 3.key(超码、候选码、主码、外码），尤其是候选码和超码的区别，最小超码的唯一性确保数据可区分
- 4.理解关系代数中的select、project、笛卡尔积、join、natural join、union、intersect、difference等操作，笔记见[relational model](relational-models-notes.pdf)

## 收获：
- 1.连接到PostgreSQL数据库，创建university schema中的instructor和department等关系
- 2.尝试定义主码和外码，解决外码引用时的错误
- 3.用SQL实现笛卡尔积和natural join，验证了union和difference的相容性要求

## 拓展
阅读GeeksforGeeks上的关系代数文章[Introduction of Relational Algebra in DBMS](https://www.geeksforgeeks.org/introduction-of-relational-algebra-in-dbms/)，结合示例加深了对操作的理解

# Week3 SQL

## 学习内容：
- 1.SQL DDL：基本数据类型（数值、字符串、null），模式定义（CREATE TABLE），删除（DROP TABLE、DELETE FROM）
- 2.SQL DML：SELECT、FROM、WHERE子句，过滤（between、!=、<>、LIKE），排序（ORDER BY），更名（AS）

## 收获：
- 1.理解了DDL的基本数据类型（如数值、字符串、null）和模式定义
- 2.在DML部分，重点练习select、from、where的查询逻辑，尝试了between、!=和order by等操作，验证查询结果的正确性
- 3.理解null的意义：未知或不存在，如何影响查询

## 拓展
- [聊聊SQL语句中 DDL 、DML 、DQL 、DCL 分别是什么](https://blog.csdn.net/qq_45069279/article/details/115270096)
除了课上讲过的DDL和DML以外，还有DQL和DCL，分别代表Query和Control，DQL专注于数据查询；DCL则用于设置和撤销用户权限。

- 除了课上讲授的LIKE以外，了解PG中的字符串匹配[Pattern Matching Notes](Pattern Matching.md)

# Week4 lab

## 实践：PostgreSQL 环境搭建与数据操作实验
- 成功在 Windows 系统中部署 PostgreSQL 环境，掌握了通过 SQL Shell 和 pgAdmin 操作数据库

## 实现内容：
- 0.Windows环境下PostgreSQL搭建（新建数据库、连接数据库、导入数据、编写query）
- 1.数据导入（使用 COPY 命令完成大批量导入测试）
- 2.基本查询与高级查询：如嵌套查询、聚合函数结合 GROUP BY 和 HAVING
- 3.字符串处理、布尔值、模糊查询、连接符 || 等细节掌握

# Week 5 null-aggregate

## 学习内容：
- 1.布尔类型（boolean）：true、false、unknown（SQL中由null表示），在查询结果中false和unknown不出现
- 2.在PG中实践聚集函数（max、min、avg、count、sum）
- 3.练习group by和having，验证分组和条件筛选逻辑
- 4.嵌套子查询（Nested sub-queries）中，用 IN/NOT IN 和 >some/>all 编写查询，比较了 =some 与 in 的等价性，还尝试标量子查询和 EXISTS 优化复杂查询

## 收获：
- 1.理解SQL查询执行逻辑：
```SQL
SELECT…
FROM…
WHERE…
GROUP BY…
HAVING…
```
- 2.用WITH子句定义临时关系可以简化多表查询
- 3.涉及到聚集函数有很多invalid的warning，可从底层逻辑理解为什么invalid，查询时需注意语法

## 拓展
学习order by random()：notes[order by random() notes](order by random().pdf)
group by和having讲解：[SQL Course for Beginners](https://www.youtube.com/watch?v=7S_tz1z_5bA&t=62s)

# Week 6 change

## 学习内容：
- 1.删：DELETE FROM…WHERE…
- 2.增：INSERT INTO…VALUES…；批量导入（COPY）
- 3.改：UPDATE…SET…（WHERE…）；update+case
- 4.修改关系（ALTER TABLE）：新增属性、删除属性
- 5.完整性约束：默认值、CHECK约束、UNIQUE约束
- 6.SQL排名：RANK

## 收获：
- 1.可用COPY命令从csv文件批量导入数据，显著提升效率
- 2.DELETE、INSERT和UPDATE的语法及应用场景，区分了DELETE（删除数据）和DROP（删除表）的差异
- 3.自行探索RANK函数，编写查询对课程学分credit进行排名
- 4.尝试UPDATE结合CASE语句，根据条件批量更新salary字段

## 拓展
- 5月8日lab 使用python访问数据库，实现增、删、改操作。代码如下：
```python
import psycopg
#Update theconnasyouneed
with psycopg.connect("dbname=mydb user=postgres port=5432 password=Joyce.2911") as conn:
    with conn.cursor() as cur:
        cur.execute("SELECT * FROM department")
        records = cur.fetchall()
        print(records)

# 数据库的增删改操作

# 连接字符串，替换为你自己的参数
conn_str = "dbname=mydb user=postgres port=5432 password=Joyce.2911 host=localhost"

with psycopg.connect(conn_str) as conn:
    with conn.cursor() as cur:
        
        # 创建 department_new 表（如果不存在）
        cur.execute("""
            CREATE TABLE IF NOT EXISTS department_new (
                id   INT PRIMARY KEY,
                name TEXT NOT NULL
            )
        """)

        # 插入新数据（INSERT）
        cur.execute(
            "INSERT INTO department_new (id, name) VALUES (%s, %s)",
            (4, 'HR')
        )

        # 更新数据（UPDATE）
        cur.execute(
            "UPDATE department_new SET name = %s WHERE id = %s",
            ('Human Resources', 4)
        )

        # 删除数据（DELETE）
        cur.execute(
            "DELETE FROM department_new WHERE id = %s",
            (4,)
        )

        # 提交事务
        conn.commit()

```

# Week 7 join

## 学习内容：
- 1.natural join：所有相同名称属性的值相等；使用join using (属性)去除-- 2.重复属性；使用on指定任意条件
- 3.默认inner join；outer join：可包含null，不丢失数据
- 4.视图（view）：虚拟的表
- 5.事务（transaction）：查询和更新语句序列
- 6.索引：提高查询效率的数据结构

## 收获：
- 1.理解inner join和outer join的区别。在PG中用join on连接instructor和department表，解决重复属性问题，并用left outer join保留未匹配数据。
- 2.创建视图faculty，通过CREATE VIEW简化查询，验证视图的虚拟表特性。

# week8-advanced
进入高级数据库的学习，包括高级数据类型和授权机制。

## 学习内容：
- 1.高级数据类型：日期、时间、interval
- 2.interval表示时间间隔：SELECT time/date ‘’ + interval ‘’
- 3.extract()从timestamp或interval中抽取字段
- 4.类型转换：cast (e as t)、PG中::符号、to_xxx()方法
- 5.授权：GRANT <权限列表> ON <关系或视图名> TO <用户或角色>

## 收获：
- 1.在PG中实践 EXTRACT(field FROM timestamp) 提取日期字段，并用 :: 进行类型转换，如 to_date('2025-05-11', 'YYYY-MM-DD')，解决了格式转换问题
- 2.针对精度问题，用numeric类型替代float，在小数点精度敏感的问题（如金融数据场景）比较重要。
- 3.to_char() 格式化日期输出，编写复杂查询结合 interval 统计时间跨度

## 拓展
- 探究数据库的备份 [数据库的备份](数据库的备份.pdf)


# week9-advanced

## 学习内容：
- 1.定义函数（function）：返回结果
- 2.定义过程（procedure）：执行操作
- 3.触发器（trigger）：自动执行
- 4.使用Python（psycopg2）访问数据库
- 5.SQL注入攻击

## 收获：
- 1.在PG中创建了 FUNCTION 计算课程平均学分
- 2.定义TRIGGER，自动记录 instructor 表薪资更新日志，验证触发器的自动化执行效果
- 3.用 Python 的 psycopg2 连接 PostgreSQL，编写脚本批量插入数据

## 拓展：
除了关系型数据库，对常见的非关系型数据库进行了解（文档存储、键值存储和宽列存储等类型），下载文档存储类数据库MongoDB，执行基本的增、删、改、查操作，见[作业7](7.md)

# Week10-design

## 学习内容：
- 1.E-R模型：实体-联系模式，将现实世界需求映射到概念模式
- 2.实体集和联系集
- 3.属性：简单vs复合、单值vs多值、派生属性
- 4.映射：One-to-One、One-to-Many、Many-to-Many、Many-to-One
- 5.使用draw.io绘制E-R图；实体集的主码、弱实体集
- 6.去除冗余属性、E-R图转化为关系模式、模式的合并

## 收获：
- 1.使用 [draw.io](https://app.diagrams.net/) 绘制 university 数据库的 E-R 图，并与datagrip中的E-R图进行比对
- 2.知道不同映射的区别，以及如何用箭头表示
- 3.如何将E-R图转化为关系模式。去除冗余属性并合并模式

## 拓展
完成作业时，发现将一个关系转化为E-R图还是有所困难，参考[A Guide to the Entity Relationship Diagram (ERD)](https://www.databasestar.com/entity-relationship-diagram/)完成了E-R图的绘制[作业8](8_er.md)，有很多不同的notation，尽量和课上讲到的保持一致。

# week 11-norm

## 学习内容：
- 1.1NF、3NF 和 BCNF 的定义及无损分解的重要性
- 2.函数依赖（如 ID→name）和闭包推导（如 A→B，B→C 推 A→C）

## 收获：
- 1.学会验证是否满足BCNF
- 2.理解BCNF和3NF之间需要权衡，3NF更常用于保持依赖的场景

## 拓展：
- 进一步结合示例了解范式 [A Comprehensive Guide to Database Normalization with Examples](https://guides.visual-paradigm.com/a-comprehensive-guide-to-database-normalization-with-examples/)

# week 12-theory
理论学习，数据库如何存储以及索引机制

## 学习内容：
- 1.主流数据库存储基于磁盘，计算时从磁盘读取数据到内存
- 2.文件存储：DBMS将文件组织成pages，内容包括header和data
- 3.组织方式：堆文件、树文件、顺序文件、哈希文件
- 4.存储模型：行存储（row storage）、列存储（column storage）
- 5.索引：有序索引、聚集索引、非聚集索引、稠密索引、稀疏索引、B+树索引

## 收获：
- 1.理解DBMS 如何将数据组织为 pages
- 2.行存储和列存储在不同查询场景下的效率差异

## 拓展：
- Slidev
- DuckDB
- [vector databases](https://www.dailydoseofds.com/a-beginner-friendly-and-comprehensive-deep-dive-on-vector-databases/#approximate-nearest-neighbors-ann)
- 也可查看此网站其它data science相关文章
