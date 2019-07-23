1、查询emp表中的所有信息

```SQL
select * from emp;
```

2、显示emp表的员工姓名和工资。

```SQL
select ename, sal from emp;
```

3、查询emp表中部门编号为20的并且sal（工资）大于3000的所有员工信息

```SQL
select * from emp where deptno = 20 and sal > 3000;
```

4、查询emp表中部门编号为20的或者sal（工资）大于3000的所有员工信息

```SQL
select * from emp where deptno = 20 or sal > 3000;
```

5、使用between and 查询工资在2000和4000之间的员工（用and 重新实现）

```SQL
select * from emp where sal between 2000 and 4000;
select * from emp where sal >= 2000 and sal <= 4000;
```

6、使用in 查询 部门编号10，20的所有员工

```SQL
select * from emp where deptno in (10, 20);
```

7、使用like查询所有名字中包括 W的员工信息

```SQL
select * from emp where ename like '%W%';
```

8、使用like查询所有员工名字中第二子字母为W的员工信息

```SQL
select * from emp where ename like '_W%';
```

9、查询所有员工信息并按照部门编号和工资进行排序

```SQL
select * from emp order by deptno, sal;
```

10、显示员工工资上浮20%的结果。

```SQL
select empno, ename, job, mgr, hiredate, sal*1.2, comm, deptno from emp;
```

11、显示EMP表的员工姓名以及工资和奖金的和。

```SQL
select ename, sal+nvl(comm, 0) from emp;
```

12、显示DEPT表的内容，使用别名将表头转换成中文显示。     

```SQL
select deptno 部门编号, dname 部门名称, loc 地点 from dept;
```

13、查询员工姓名和工资，并按工资从小到大排序。

```SQL
select ename, sal from emp order by sal;
```

14、查询员工姓名和雇佣日期，并按雇佣日期排序，后雇佣的先显示。

```SQL
select ename, hiredate from emp order by hiredate desc;
```

15、查询员工信息，先按部门编号从小到大排序，再按雇佣时间的先后排序。

```SQL
select * from emp order by deptno, hiredate;
```

16、按工资和入职月份的乘积排序（倒序）。

```SQL
select * from emp order by sal * extract (month from hiredate) desc;
```

17、显示职务为“SALESMAN”的员工的姓名、职务和工资。

```SQL
select ename, job, sal from emp where job = 'SALESMAN';
```

18、显示工资大于等于3000的员工姓名、职务和工资。

```SQL
select ename, job, sal from emp where sal > 3000;
```

19、显示1982年以后雇佣的员工姓名和雇佣时间。

```SQL
select ename, hiredate from emp where extract(year from hiredate) > 1982;
```

20、显示部门编号为10的员工姓名和雇佣时间

```SQL
select ename, hiredate from emp where deptno = 10;
```

21、显示工资在1000～2000之间(不包括1000和2000)的员工信息。

```SQL
select * from emp where sal>1000 and sal<2000;
```

22、显示部门10中工资大于1500的员工。

```SQL
select * from emp where sal>1500 and deptno=10;
```

23、显示职务为CLERK或MANAGER的员工信息。

```SQL
select * from emp where job in('CLERK', 'MANAGER');
```

24、显示部门10以外的其他部门的员工。

```SQL
select * from emp where deptno!=10;
```

25、显示部门10和部门20中工资小于1500的员工。

```SQL
select * from emp where deptno in(10, 20) and sal<1500;
```

26、查询姓名首字母为“A”或第二个字符为“A”的所有员工信息

```SQL
select * from emp where ename like 'A%' or ename like '_A%';
```

27、查询部门20和30中的、岗位不是“CLERK”或“SALESMAN”的所有员工信息。

```SQL
select * from emp where deptno in (20, 30) and job != 'CLERK' and job != 'SALESMAN';
```

28、查询出工资在2500-3500之间，1981年入职的，没有奖金的所有员工信息。

```SQL
select * from emp where sal between 2500 and 3500 and hiredate between to_date('1981/1/1', 'yyyy-MM-dd') and to_date('1981/12/31', 'yyyy-MM-dd') and comm is null;
```

29、查询比平均员工工资高的员工信息。

```SQL
select * from emp where sal > (select avg(sal) from emp);
```

30、查询平均工资高于2000的部门信息。

```SQL
select *
  from dept
 where deptno in
       (select deptno
          from (select deptno, avg(sal) avg_sal from emp group by deptno)
         where avg_sal > 2000);
```

31、查询出WARD的工作所在地。

```SQL
select loc
  from dept
 where deptno = (select deptno from emp where ename = 'WARD');
```

32、查询出工资比ADAMS高的所有人姓名、部门、所在地。

```SQL
select ename, dname, loc
  from emp e
 inner join dept d on e.deptno = d.deptno
 where sal > (select sal from emp where ename = 'ADAMS');
```

33、查询工资排名第7的员工信息。

```SQL
select *
  from (select *
          from (select *
                  from (select * from emp order by sal desc)
                 where ROWNUM <= 7)
         order by sal)
 where rownum <= 1;
```

34、假定当前的系统日期是2013年11月13日，显示部门10员工的雇佣天数。

```SQL
select to_date('2013-11-13', 'yyyy-mm-dd')-hiredate 雇佣天数 from emp where deptno=10;
```

35、显示员工姓名和雇佣的星期数

```SQL
select ename, ceil((to_date('2013-11-13', 'yyyy-mm-dd')-hiredate)/7) 雇佣的星期数 from emp;
```

36、显示从本年1月1日开始到现在经过的天数。

```SQL
select sysdate-to_date('2019-1-1 00:00:00', 'yyyy-mm-dd HH24-MI-SS') from dual;
```

37、查询所有员工的奖金，如果奖金没有，用0来替代

```SQL
select nvl(comm, 0) from emp;
```



