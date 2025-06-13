# Pattern Matching Notes
参考：[PostgreSQL 字符串匹配函数文档](https://www.postgresql.org/docs/17/functions-matching.html)
```txt
PostgreSQL提供了3种不同的Pattern Matching方法:
1.the traditional SQL LIKE operator
2.the more recent SIMILAR TO operator
3.POSIX-style regular expressions. 
Aside from the basic “does this string match this pattern?” operators, functions are available to extract or replace matching substrings and to split a string at matching locations.
```
## LIKE operator：
```txt
 %：(matches) any sequence of zero or more characters
 _：(matches) any single character
匹配"%"或"_"：在"%"或"_"前面加上escape character（转义字符）
默认的转义字符是\(backslash)，即使用"\%"或"\_"匹配
ILIKE can be used instead of LIKE to make the match case-insensitive according to the active locale. (PostgreSQL)
~~: 和LIKE一样
~~*: 和ILIKE一样
!~~: NOT LIKE
!~~*: NOT ILIKE (PostgreSQL)
```
```sql
'abc' LIKE 'abc'    true
'abc' LIKE 'a%'     true
'abc' LIKE '_b_'    true
'abc' LIKE 'c'      false
```

## SIMILAR TO operator:
```txt
和LIKE类似，
区别：it interprets the pattern using the SQL standard's definition of a regular expression.
POSIX正则表达式(regular expressions):
|：选择（两个选项中的任意一个）。
*：前一项重复零次或多次。
+：前一项重复一次或多次。
?：前一项重复零次或一次。
{m}：前一项精确重复 m 次。
{m,}：前一项至少重复 m 次。
{m,n}：前一项至少重复 m 次，至多重复 n 次。
() 可用于将多个项分组，使其作为一个整体处理。
[...] 指定一个字符类
```
```sql
'abc' SIMILAR TO 'abc'          true
'abc' SIMILAR TO 'a'            false
'abc' SIMILAR TO '%(b|d)%'      true
'abc' SIMILAR TO '(b|c)%'       false
'-abc-' SIMILAR TO '%\mabc\M%'  true
'xabcy' SIMILAR TO '%\mabc\M%'  false
```
```txt
注：
在 SIMILAR TO 表达式中，\m 和 \M 分别表示 单词的开始 和 单词的结束，类似于 POSIX 正则表达式中的 \b（单词边界）。
1️⃣ '-abc-' SIMILAR TO '%\mabc\M%' → true
\mabc\M 表示匹配一个独立的单词 abc，即：
\m 需要 abc 前面是非字母数字字符或字符串开头。
\M 需要 abc 后面是非字母数字字符或字符串结尾。
'-abc-' 这个字符串包含 abc，且：
- 在 abc 前面（非字母数字字符，符合 \m）。
- 在 abc 后面（非字母数字字符，符合 \M）。
结果：匹配成功，返回 true。
2️⃣ 'xabcy' SIMILAR TO '%\mabc\M%' → false
xabcy 也包含 abc，但：
abc 的前面是 x（字母），不符合 \m。
abc 的后面是 y（字母），不符合 \M。
结果：不匹配，返回 false。
```
