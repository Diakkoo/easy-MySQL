

## 基础MySQL语句

用“ { } ”代表MySQL语句中可省略的内容，
用“ / ”枚举出多个可选关键字。

#### 1. 登录MySQL

`
mysql -h localhost -P port -u username -p password
`

#### 2. 数据库定义语言（DDL）

`
CREATE/ALTER/DROP DATABASE/TABLE/VIEW/INDEX/FUNCTION/TRIGGER/USER
`

#### 3. 数据库操作语言（DML）
`
SELECT/UPDATE/DELETE
`

#### 4. 数据库控制语言（DCL）
`
GRANT/REVOKE/COMMIT/ROLLBACK/SAVEPOINT
`

#### 5.数据库（DATABASE）相关MySQL语句
* ##### 创建数据库

`
CREATE DATABASE 库名 CHARACTER SET 字符集 COLLATE 排序规则;
`

* ##### 查看数据库

`
SHOW DATABASE;
`

`
SHOW CREATE DATABASE;
`

* ##### 修改数据库

`
ALTER DATABASE 库名 CHARACTER SET 新字符集;
`

* ##### 删除数据库

`
DROP DATABASE {IF EXISTS} 库名;
`

#### 6. 数据表（TABLE）相关MySQL语句
* ##### 创建数据表

```
CREATE TABLE 表名 (
    字段名1 数据类型 是否空，约束类型 备注,
    字段名2 数据类型 是否空，约束类型 备注,
    字段名3 数据类型 是否空，约束类型 备注
);
```

* ##### 查看数据表基本结构

`
DESC 表名;
`

* ##### 查看数据表详细结构

`
SHOW CREATE TABLE 表名;
`

* ##### 重命名数据表

`
ALTER TABLE 表名 RENAME 新表名;
`

* ##### 添加新字段

`
ALTER TABLE 表名 ADD 字段名 数据类型 是否空 约束类型 备注 {FIRST/AFTER 字段名};
`

* ##### 修改字段

`
ALTER TABLE 表名 MODIFY 字段名 数据类型 是否空 约束类型 备注;
`

* ##### 重命名字段

`
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 新数据类型;
`

* ##### 添加约束

1. 添加主键约束

`
ALTER TABLE 表名 ADD CONSTRAINT 约束名 PRIMARY KEY {字段名,...};
`

2. 添加外键约束

`
ALTER TABLE 表名 ADD CONSTRAINT 约束名 FOREIGN KEY {字段名,...} REFERENCES 主表名 主键1{,主键2,主键3,....};
`

3. 添加唯一约束

`
ALTER TABLE 表名 ADD CONSTRAINT 约束名 UNIQUE(字段名);
`

4. 添加默认值约束

`
ALTER TABLE 表名 ALTER 约束名 SET DEFAULT 默认值;
`

* ##### 删除字段

`
ALTER TABLE 表名 DROP 字段名;
`

* ##### 删除表

`
DROP TABLE {IF EXISTS} 表名;
`

#### 7. 数据查询相关MySQL语句

```
SELECT */字段名1,字段名2,.../函数
FROM 表名/数据名
WHERE 查询条件语句
GROUP BY 被SELECT字段名
ORDER BY 被SELECT字段名
HAVING 次要查询语句
LIMIT 限制输出行数;
```

连接查询

`
SELECT .... FROM 表名1 JOIN 表名2 ON 连接条件;
`

子查询

`
SELECT ....FROM 表名1 WHERE 条件 IN (SELECT ....FROM 表名2 WHERE ...);
`

#### 8. 视图（VIEW）相关MySQL语句

* ##### 创建视图

`
CREATE VIEW 视图名 AS SELECT语句;
`

* ##### 查看视图基本结构

`
DESC 视图名;
`

`
SHOW TABLE STATUS LIKE '视图名';
`

* ##### 查看视图详细结构

`
SHOW CREATE VIEW 视图名;
`

* ##### 修改视图

`
CREATE OR REPLACE VIEW 视图名 AS SELECT语句;
`

`
ALTER VIEW 视图名 AS SELECT语句;
`

* ##### 更新视图

`
UPDATE 视图名 SET 字段名1 = 值1, 字段名2 = 值2 {WHERE 条件语句};
`

* ##### 删除视图

`
DROP VIEW {IF EXISTS} 视图名;
`

#### 9. 索引（INDEX）相关MySQL语句

* ##### 创建索引

`
CREATE {UNIQUE/FULLTEXT/SPATIAL} INDEX 索引名;
`

* ##### 查看索引

`
SHOW INDEX FROM 表名;
`

* ##### 删除索引

`
DROP INDEX 索引名 ON 表名;
`

#### 10. 数据增、删、改相关MySQL语句

* ##### 插入数据
`
INSERT {INTO} 表名 (字段名1, 字段名2, ...) VALUES(值1, 值2, ...);
`

`
INSERT INTO 表名 SET 字段名1 = 值1, 字段名2 = 值2, ...;
`

`
INSERT {INTO} 表名 {(字段名1, 字段名2, ...)} SELECT语句;
`

* ##### 更新数据

`
UPDATE 表名 SET 字段名1 = 值1 {WHERE 条件语句}；
`

* ##### 删除数据

`
DELETE FROM 表名 {WHERE 条件语句};
`

`
TRUNCATE {TABLE} 表名;
`

#### 11. 存储过程（PROCEDURE）相关MySQL语句

* ##### 创建存储过程

```
CREATE PROCEDURE 存储名({IN/OUT/INOUT 参数名 数据类型})
BEGIN
   SELECT语句
END;
```

* ##### 修改存储过程

`
ALTER PROCEDURE 存储名;
`

* ##### 调用存储过程

`
CALL 存储名({参数});
`

* ##### 查看存储过程

`
SHOW PROCEDURE STATUS {LIKE '存储名'};
`

`
SHOW CREATE PROCEDURE 存储名;
`

* ##### 删除存储过程

`
DROP PROCEDURE 存储名;
`

#### 12. 游标相关MySQL语句

* ##### 声明游标

`
DECLARE 游标名 CURSOR FOR SELECT语句;
`

* ##### 打开游标

`
OPEN 游标名;
`

* ##### 使用游标

`
FETCH 游标名 INTO 参数;
`

* ##### 关闭游标

`
CLOSE 游标名;
`

#### 13. 存储函数（FUNCTION）相关MySQL语句

* ##### 创建存储函数

```
CREATE FUNCTION 函数名 (参数)
RETURNS 数据类型
BEGIN
   DECLARE 变量名 数据类型
   SELECT ... INTO 变量名 FROM ...
   {WHERE 条件语句}
   RETURN 变量名
END;
```

* ##### 调用存储函数

`
SELECT 函数名(参数);
`

* ##### 查看存储函数基本结构

`
SHOW FUNCTION STATUS {LIKE '函数名'};
`

* ##### 查看存储函数详细结构

`
SHOW CREATE FUNCTION 函数名;
`

* ##### 修改存储函数

`
ALTER FUNCTION 函数名;
`

* ##### 删除存储函数

`
DROP FUNCTION {IF EXISTS} 函数名;
`

#### 14. 触发器（TRIGGER）相关MySQL语句

* ##### 创建触发器

```
CREATE TRIGGER 触发器名
BEFORE/AFTER INSERT/UPDATE/DELETE ON 表名
FOR EACH ROW
BEGIN
  SELECT语句块
END;
```

* ##### 查看触发器

`
SHOW TRIGGERS;
`

`
SHOW CREATE TRIGGER 触发器名;
`

`
SELECT * FROM information_schema.TRIGGERS;
`

* ##### 删除触发器

`
DROP TRIGGER {IF EXISTS} 触发器名;
`

#### 15. 数据库安全相关MySQL语句

* ##### 创建用户

`
CREATE USER 用户名@主机名 IDENTIFIED BY '密码';
`

* ##### 修改用户

`
UPDATE mysql.user SET USER = '新用户名' WHERE USER = '旧用户名';
`

* ##### 查看用户

`
SELECT user FROM mysql.user;
`

* ##### 删除用户

`
DROP USER 用户名;
`

* ##### 授予权限

`
GRANT 权限1, 权限2, ... ON 库名{.表名} TO 用户名; 
`

* ##### 查看权限

`
SHOW GRANTS {FOR 用户名};
`

`
SHOW GRANTS FOR CUNRRENT_USER;
`

* ##### 回收权限

`
REVOKE 权限1, 权限2, ... ON 库名{.表名} FROM 用户名;
`

* ##### 激活角色

```
SET DEFAULT ROLE ALL TO 用户名@主机名;
SET GLOBAL activate_all_role_on_login = ON;
```

* ##### 回收用户的角色

`
REVOKE 角色名 FROM 用户名;
`

* ##### 删除角色

`
DROP ROLE 角色名;
`

#### 16. 数据库备份与恢复相关MySQL语句

* ##### 备份数据库

`
mysqldump -u 用户名 -p 密码 库名{.表名} > 路径/文件名.sql
`

* ##### 数据恢复

`
mysql -u 用户名 -p 密码 库名{.表名} < 路径/文件名.sql
`

`
SOURCE 路径/文件名.sql;
`

* ##### 导出文本文件

`
mysql -u 用户名 -p 密码 -e "SELECT语句" 库名 > 路径/文件名.txt
`

`
mysqldump -u 用户名 -p 密码 -T 路径/文件名.txt 库名{.表名}
`

* ##### 导出XML文件

`
mysql -u 用户名 -p 密码 -X -e "SELECT语句" 库名 > 路径/文件名.xml
`

* ##### 数据库数据迁移

`
mysqldump -h 主机名1 -u 用户名 -p 密码 --all 库名 | mysql -h 主机名2 -u 用户名 -p 密码
`
