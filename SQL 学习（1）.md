### SQL  Structured Query Language

####  常识

不使用任何业务相关的字段作为主键。主键也不应该允许NULL。

把数据与另一张表关联起来，这种列称为外键   

索引是关系数据库中对某一列或多个列的值进行预排序的数据结构。通过使用索引，可以让数据库系统不必扫描整
个表，而是直接定位到符合条件的记录，这样就大大加快了查询速度。

索引的优点是提高了查询效率，缺点是在插入、更新和删除记录时，需要同时修改索引，因此，索引越多，插入、更新和删除记录的速度就越慢。

-- 以双减号开头的是注释

不带FROM子句的SELECT语句有一个有用的用途，就是用来判断当前到数据库的连接是否有效。

这种把多条语句作为一个整体进行操作的功能，被称为数据库事务。数据库事务可以确保该事务范围内的所有操作都可以全部成功或者全部失败。如果事务失败，那么效果就和没有执行这些SQL一样，不会对数据库数据有任何改动。

####  语句
CRUD：Create、Retrieve、Update、Delete。

SELECT <column> FROM <tablename>   (*表示“所有列”) 
SELECT <column> FROM <table1> <table2> 

SELECT <column> FROM <tablename>   WHEAE <condition>  (AND OR NOT条件表达式运算)
其他条件表达式  =(等于) >(大于) >=(大等于) <(小于) <=(小等于) <>(不等于) LIKE(相似 %表示任意字符)

SELECT <column> FROM <tablename> ORDER BY <column> (默认的排序规则是ASC：“升序”，即从小到大。)
SELECT <column> FROM <tablename> ORDER BY <column> DESC (DESC表示“倒序”)
如果有WHERE子句，那么ORDER BY子句要放到WHERE子句后面。

SELECT <column> FROM <tablename> LIMIT <m> OFFSET <n> （分页 m pagesize分页大小  n页码）
OFFSET超过了查询的最大数量并不会报错，而是得到一个空的结果集。

SELECT COUNT<column> FROM <tablename> 查询表记录条数
COUNT(*)表示查询所有列的行数，要注意聚合的计算结果虽然是一个数字，但查询的结果仍然是一个二维表，只是这个二维表只有一行一列，并且列名是COUNT(*)。
其他聚合函数  SUM(求和) AVG(平均) MAX(最大) MIN(最小)
如果聚合查询的WHERE条件没有匹配到任何行，COUNT()会返回0，而SUM()、AVG()、MAX()和MIN()会返回NULL

SELECT <column> FROM <tablename> GROUP BY <column> 

INSERT INTO <tablename> <column> VALUES <value>

UPDATE <tablename> SET <column> WHEAE <condition>

DELETE FROM <tablename> WHEAE <condition>