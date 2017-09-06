# mysql-basic-command
A Readme introduct mysql basic command

## 这篇文档主要是介绍mysql的基本命令

**每条sql语句后需要加分号**
1.显示所有数据库名
```sql
SHOW DATABASE
```

2.显示当前数据库所有表名
```sql
SHOW TABLES
```

3.显示cus表所有列
```sql
SHOW COLUMNS FROM cus
```

4.显示pro表中所有prod_name字段内容(单字段检索)
```sql
SELECT prod_name FROM pro
```

5.显示pro表中所有prod_name,prod_price字段内容(多字段检索)
```sql
SELECT prod_name,prod_price FROM pro
```

6.显示pro表所有数据
```sql
SELECT * FROM products
```

7.对prod_name结果去重
```sql
SELECT DISTINCT prod_name FROM products
```

8.只返回结果前5行
```sql
SELECT name from products LIMIT 5
```

9.从第5行开始返回6行数据
```sql
SELECT name from products LIMIT 5,6
```

10.对结果以pro列按字符*升序*排列
```sql
SELECT name FROM products ORDER BY pro
```

11.对结果以pro列按字符*降序*排列
```sql
SELECT name FROM products ORDER BY pro DESC
```

12.对结果以pro，name列按字符*升序*排列
```sql
SELECT name FROM products ORDER BY pro, name
```

13.对结果以pro列降序排列的基础上按name列*升序*排列
```sql
SELECT name FROM products ORDER BY pro DESC, name
```


14.找出num列为111的name
```sql
SELECT name FROM products WHERE num=111
```

15.找出num列中为NULL的name
```sql
SELECT name FROM products WHERE num IS NULL
```

16.找出num列大于100且kk列大于20的name
```sql
SELECT name FROM products WHERE num=111 and kk>20
```

17.找出num列中含有je字符的name
```sql
SELECT name FROM products WHERE num like "%je%"
```

18.找出num列中以je开头的name
```sql
SELECT name FROM products WHERE num like "je%"
```

19.找出num列中以je开头且je后面只有一个字符串的name
```sql
SELECT name FROM products WHERE num like "je_"
```

20.将name字段和age字段中间用age字符拼接起来，可凭借多个字符或字符串
```sql
SELECT Concat(name, 'age',age )FROM products
```

21.将结果列用别名显示
```sql
SELECT name AS rename FROM products
```

22.聚集函数
 - AVG():返回某列的平均值
 - COUNT():返回某列的行数
 - MAX():返回某列的最大值
 - MIN():返回某列的最小值
 - SUM():返回某列值之和
 - SELECT AVG(pro_price) FROM pro;

23.将num_prod列的统计按照vend_id列的不同数据分组，即最后结果有两栏，一栏是vend._id，另一栏是num_prods，
   num_prods结果是当前vend_id对应的num_prods数量
```sql
SELECT vend._id, COUNT(*) AS num_prods FROM pro GROUP BY vend._id
```

24.过滤分组
```sql
SELECT vend._id, COUNT(*) AS num_prods FROM pro where pro_price >= 10 GROUP BY vend._id HAVING count(*) >= 2;
```

 - where在数据分组前进行过滤，having在分组后进行过滤

25.sql语句顺序
```sql
select from where group by having order by limit
```

26.联结表(等值联结)
**联结多个表进行查询，返回一组结果**
```sql
SELECT vend_name, prod_name, prod_price 
FROM vendors, products
WHERE vendors.vend_id = products.vend_id
ORDER BY vend_name, prod_name;
```

27.联结表(内部联结)
**JOIN ON语法，ON相当于WHERE**
```sql
SELECT vend_name, prod_name, prod_price 
FROM vendors INNER JOIN products
ON vendors.vend_id = products.vend_id
ORDER BY vend_name, prod_name;
```

28.组合查询
** sql UNION sql**

**显示结果，交集**
```sql
SELECT vend_id, prod_id, prod_price 
FROM products
WHERE prod_price <= 5
UNION
SELECT vend_id, prod_id, prod_price 
FROM products
WHERE vend_id IN (1001,1002);
```

**显示所有结果，并集**
```sql
SELECT vend_id, prod_id, prod_price 
FROM products
WHERE prod_price <= 5
UNION ALL
SELECT vend_id, prod_id, prod_price 
FROM products
WHERE vend_id IN (1001,1002);
```

UNION使用规则
 - UNION必须由两条或两条以上的SELECT语句组成，语句之间用UNION分割，多条语句使用多个UNION
 - UNION中的每个查询必须使用相同的列、表达式或聚集函数
 - 列数据类型必须兼容，类型不必完全相同

29.插入数据
```sql
INSERT INTO cus(cum1, 
cum2) 
VALUES('100',
'200');
```

30.插入多条数据
```sql
INSERT INTO cus(cum1, 
cum2) 
VALUES(
    '100',
    '200'
),
(
    '100',
    '200'
);
```

31.更新数据
```sql
UPDATE cus
SET cus_name='new name',
    cus_email='new email'
where cus_id=100;
```

32.删除数据
```sql
DELETE FROM cus
where cus_id=100;
```

33.创建用户
```sql
CREATE USER clx IDENTIFIED BY 'password';
```

33.删除用户
```sql
DROP USER clx;
```

34.查看用户权限
```sql
SHOW GRANT FOR clx;
```

34.用户授权
```sql
GRANT SELECT ON database_name.table_name TO clx;#授予clx对database_name数据库的table_name有select权限
GRANT ALL ON *.* TO clx;#授予clx对所有数据库的所有表有所有权限
```
常用权限
 - ALL
 - ALTER
 - REPLICATION SLAVE

35.修改密码
```sql
set password for clx = password('new_password');
```

36.创建表
```sql
CREATE TABLE test(
    cus_id int not null,
    PRIMARY KEY (cus_id)
)engine=InnoDB;
```

37.给表新增字段
```sql
ALTER TABLE test
ADD vend_phone char(20);
```

37.给表删除字段
```sql
ALTER TABLE test
DROP COLUMN vend_phone;
```

38.修改字段名

**alter table 表名称 change 字段名称 字段名称 字段类型**
```sql
ALTER TABLE clx
CHANGE venc_phone
vend_cell char(30);
```

39.显示所有字段名
```sql
 DESC table_name;
```

40.重命名表

```sql
RENAME TABLE clx TO clx1;
```

41.mysql使用帮助
*在命令前面加？，可以差看该命令的帮助*
```sql
？ SHOW
? ALTER
? DATA DEFINITION
...
```
