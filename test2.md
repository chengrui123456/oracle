#实验2:用户管理 - 掌握管理角色、权根、用户的能力，并在用户之间共享对象。

- 第1步：以system登录到pdborcl，创建角色cr_se和用户cr，并授权和分配空间：

```sql
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE cr_se;
Role created.
SQL> GRANT connect,resource,CREATE VIEW TO cr_se;
Grant succeeded.
SQL> CREATE USER cr IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
User created.
SQL> ALTER USER cr QUOTA 50M ON users;
User altered.
SQL> GRANT cr_se TO cr;
Grant succeeded.
SQL> exit
```
- 第2步：新用户cr连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户。

```sql
$ sqlplus cr/123@pdborcl
SQL> show user;
USER is "CR"
SQL> CREATE TABLE mytable (id number,name varchar(50));
Table created.
SQL> INSERT INTO mytable(id,name)VALUES(1,'zhang');
1 row created.
SQL> INSERT INTO mytable(id,name)VALUES (2,'wang');
1 row created.
SQL> CREATE VIEW myview AS SELECT name FROM mytable;
View created.
SQL> SELECT * FROM myview;
NAME
--------------------------------------------------
zhang
wang
SQL> GRANT SELECT ON myview TO hr;
Grant succeeded.
SQL>exit
```

- 第3步：用户hr连接到pdborcl，查询cr授予它的视图myview

```sql
$ sqlplus hr/123@pdborcl
SQL> SELECT * FROM cr.myview;
NAME
--------------------------------------------------
zhang
wang
SQL> exit
```
