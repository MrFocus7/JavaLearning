###  **Oracle基础术语**   


1. **数据字典**：是数据库中所有对象及其关系的信息集合。   
2. **数据文件**：数据文件包含实际数据，例如销售订单和客户。逻辑数据库结构(如表和索引)的数据物理存储在数据文件中。    
3. **控制文件**：每个Oracle数据库都有一个包含元数据的控制文件。元数据描述数据库的物理结构，包括数据库名称和数据文件的位置。   
4. **日志文件**：每个Oracle数据库都有一个联机重做日志，其中包含两个或多个联机重做日志文件。联机重做日志由重做条目组成，用于记录对数据所做的所有更改。  
5. **表空间**：数据库是由称为表空间的逻辑存储单元构成的。表空间是段的逻辑容器。每个表空间至少包含一个数据文件。  
6. **段**：段是分配用于存储用户对象的一组范围，例如表或索引。  
7. **区**：区是用于存储特定类型信息的特点数量的逻辑连续数据块。  
8. **数据块**：数据库对应于磁盘上的字节数。Oracle将数据存储在数据块中。数据块也称为逻辑块，Oracle块或页面。  
   
     
**DML**: Data Manipulation Language  
**DQL**: Data Query Language  
**DCL**: Data Control Language  
**DDL**: Data Definition Language

---
### **Oracle基本命令**

  
创建表空间：
```sql
create tablespace XXX datafile 'u01/app/test.dbf' size 500m [next 50m maxsize 1g] autoextend on;
```
查询数据库中的所有用户：
```SQL
select * from dba_users;
```
创建用户：
```SQL
create user test identified by 123456; -- 创建用户 
grant connect, resource to test [with admin option]; -- 赋予权限
drop user test cascade; -- 删除
```
赋予权限：
```SQL
grant connect to 用户名; -- 授予用户允许登录的权限
grant create tablespace to 用户名; -- 授予创建表空间的权限
grant select on 授权的表名 to 用户名; -- 授予该用户可以查询某个表的权限
grant update on 授予的表名 to 用户名; -- 授予该用户可以更新某个表的权限
grant insert on 授予的表名 to 用户名; -- 授予该用户可以插入某个表的权限
grant execute on 存储过程 to 用户名; -- 授予该用户具有存储过程权限
grant update on 授权的表名 to 用户名 with grant option; -- (连续授权)授权更新权限转移给下一个用户,可以继续授权
```
收回权限：
```SQL
revoke select on 授权的表名 from 用户名;
revoke insert on 授权的表名 from 用户名;
revoke connect to 用户名; -- 收回该用户的登录权限
revoke all on 授权的表名 from 用户名; -- 收回该用户所有权限
```
权限查询：
```SQL
select * from dba_tab_privs where grantee='用户名'; -- 查询一个用户拥有的对象权限
select * from dba_sys_privs where grantee='用户名'; -- 查询一个用户拥有的系统权限
select * from session_privs; -- 当前会话有效的系统权限
```
锁：
```SQL
alter user scott account lock;
alter user scott account unlock;
```
角色：
```SQL
create role 角色名称; -- 建立'角色名称'角色
grant 角色名称 to 用户名 ; -- 将角色的权限授权给该用户;
alter user 角色名称 default 用户名1,用户名2; -- 修改用户默认角色
DROP ROLE 角色名称; -- 删除角色；
select * from role_sys_privs where role=角色名称; -- 查看某个角色下有什么系统权限；
select * from role_role_privs where role=角色名称; -- 查看某个角色下面有什么角色权限
select * from role_tab_privs where role='角色名称'; -- 查看某个角色下面有什么表权限
select * from dba_role_privs where grantee='用户名'; -- 查看用户下面有多少个角色；
```
---
### **Oracle权限概述**
1. 系统权限：指在系统级控制数据库的存取和使用的机制   
2. 对象权限：指在对象级控制数据库的存取和使用的机制
---    
### **Oracle数据类型**
每种数据类型都有一个由Oracle内部管理的代码。要查找列中值的数据类型代码，请使用该DUMP()函数。  

类型 | 含义
---|---
CHAR | 固定长度字符串
VARCHAR2 | 可变长度的字符串
NCHAR | 根据字符集而定的固定长度字符串
NVARCHAR2 | 根据字符集而定的可变长度字符串
DATE | 日期(日-月-年)
TIMESTAMP | 日期(日-月-年)
LONG | 超长字符串
RAW | 固定长度的二进制数据
LONG RAW | 可变长度的二进制数据
BLOG | 二进制数据
CLOG | 字符数据
NCLOG | 根据字符集而定的字符数据
BFILE | 存放在数据库外的二进制数据
ROWID | 数据表中记录的唯一行号
NROWID | 二进制数据表中记录的唯一行号
NUMBER(P,S) | 数字类型
---   
### **查询数据**
```SQL
SELECT [ALL|DISTINCT]
{*|table.*|[table.]field1[AS alias1][,[table.]field2[AS alias2][,···]]}
FROM tableexpression[,···][IN externaldatabase]
[WHERE···]
[GROUP BY···]
[HAVING···]
[ORDER BY···]
[WITH OWNERACCESS OPTION]
```
---
### **运算符**   

运算符 | 含义
---|---
= | 等于 
<>, != | 不等于
< | 小于
<= | 小于等于
BETWEEN···AND | 在两值之间
IN | 在一组值的范围内
LIKE | 与字符串匹配
IS NULL | 为空值

---
### **练习**
```SQL
--1.查询姓名首字母为"A"或第二个字符为"A"的的所有员工的信息。
select * from emp where ename like 'A%' or ename like '_A%';
--2.查询部门20和30中的、岗位不是"CLERK"或"SALESMAN"的所有员工信。
select * from emp where deptno in (20, 30) and job != 'CLERK' and job != 'SALESMAN';
--3.查询出工资在2500-3500之间，1981年入职的，没有奖金的所有员工信息。
select * from emp where sal between 2500 and 3500 and hiredate between to_date('1981/1/1', 'yyyy-MM-dd') and to_date('1981/12/31', 'yyyy-MM-dd') and comm is null;
--4.查询比平均员工工资高的员工信息。
select * from emp where sal > (select avg(sal) from emp);
```
