1.创建数据库<br>
    create database 库名
    
2.创建并设置数据库编码<br>
    create database 库名 character set 编码
    
3.查看数据库<br>
    show create database 库名
    
4.删除一个数据库<br>
    drop database 库名
    
5.使用或切换当前数据库<br>
    use 库名
    
6.查看正再使用的数据库<br>
    select database<>

1.创建表<br>
    create table 表名(
        字段名 类型(长度) [约束],
        字段名 类型(长度) [约束],
        字段名 类型(长度) [约束]
    );
    
2.查看数据库有哪些表<br>
    show tables
    
3.查看表的列信息<br>
    desc 表名
    
4.删除一张表<br>
    drop table 表名
    
5.添加、修改、删除列、或列信息<br>
    alter table 表名 add 字段名 类型(长度) [约束]
    alter table 表名 modify 要修改的字段名 类型(长度) [约束]
    alter table 表名 change 旧列名 新列名 类型(长度) [约束]
    alter table 表名 drop 列名
    
6.修改表名<br>
    rename table 表名 to 新表名
    
7.修改表的字符集<br>
    alter table 表名 character set 编码<br>
    alter database 表名 character set 编码
    
8.查看表的编码等信息<br>
    show create table 表名
    
    
1.对表的增删改查<br>
    insert into 表名(列名1,列名2,列名3...) values(值1,值2,值3...)<br>
    insert into 表名 values(值1,值2,值3……)<br>
    update 表名 set 字段名=值, 字段名=值, 字段名=值……<br>
    update 表名 set字段名=值, 字段名=值, 字段名=值…… where 条件<br>
    delete from 表名 where 条件<br>
    select [distinct] *| 列名1，列名2 from 表名 [where条件]<br>
        eg: select * from product as[可以省略] p(使用别名)<br>
            select pname as[可以省略] p from product(使用别名)<br>
            select distinct(price) from product(去掉重复值)<br>
            select pname,price+10 from product;(所有的商品的价格+10进行显示)<br>
            select pname from product where pname>xxx or pname<xxx;<br>
            select pname from product where pname like %哈%; _ *  .  <br>
            select pname from product where pname in (a, 6, 9);
            
2.delete与truncate的区别
    delete删除的时候是一条一条的删除记录，它配合事务，可以将删除的数据找回。<br>
    truncate删除，它是将整个表摧毁，然后再创建一张一模一样的表。它删除的数据无法找回。
    
3.排序
    select pname from product order by pname asc<br>
    select pname from product order by pname desc
    
4.聚合函数
    select sum(price) from product<br>
    select avg(price) from product<br>
    select count(*) from product
    MAX/MIX
    
5.查询总结
    select  一般在的后面的内容都是要查询的字段<br>
    from  要查询到表<br>
    where<br>-------常用between...and  in(xx,xxx,xx) like '%_*'  is null----and or not
    group by <br>
    having  分组后带有条件只能使用having<br>
    order by 它必须放到最后面
    
    
1.多表设计
   一对一   主键任意存
   一对多   多的一方存
   多对多   新建一张关联表保存各自的主键
2.数据类型
   varchar 可变长度字符串（根据存的东西的长短，只占用实际的）---节省空间
   char    固定长度的字符串（无论存的东西是否占满，都是占用那么多空间）----更省时间
   blob    大二进制数据（视频，图片等，最大4G）
   text    大文本数据（最大4G）
   tinyint 1
   smallint 2
   int 4
   bigint 8
   float
   double
   bit   一位0101010（布尔）
   data 日期
   time  时间
   datetime 日期时间
   timestamp  当某一列市timestamp的时候，这行记录新增或修改时，自动更新最近修改时间
   
3.约束
    主键 primary key
    主键自动增长 auto_increment
    唯一约束 unique
    非空 not null
    外键约束
    
4.mysql的字符跟日期类型的数据必须用单引号包起来

5.注意区分mysqlserver的编码，与自己库表编码的区别的编码

6.例子
    ~统计一个班级语文、英语、数学的成绩总和
        select sum(ifnull(chinese,0)+ifnull(english,0)+ifnull(math,0)) from exam;
    在执行计算时,只要有null参与计算,整个计算的结构都是null
    此时可以用ifnull函数进行处理
    ~统计一个班级语文成绩平均分
        select sum(chinese)/count(*) 语文平均分 from exam;
        
7.group by 列名
    写了groupby哪一列，那么那一列值相同就会合在一起，（立体重叠）其他列的值显示的就是第一条数据
    ~对订单表中商品归类后，显示每一类商品的总价
    	select product,sum(price) from orders group by product;--product的price就是就是重叠的综合价格显示
    ~询购买了几类商品，并且每类总价大于100的商品
  		select product 商品名,sum(price)商品总价 from orders group by product having sum(price)>100;	
    where子句和having子句的区别:
        where子句在分组之前进行过滤having子句在分组之后进行过滤
        having子句中可以使用聚合函数,where子句中不能使用
        很多情况下使用where子句的地方可以使用having子句进行替代
        
8.多表查询
    笛卡尔积查询:
        将两张表的记录进行一个相乘的操作查询出来的结果就是笛卡尔积查询,如果左表有n条记录,右表有m条记录,笛卡尔积查询出有n*m条记录,其中往往包含了很多错误的数据,所以这种查询方式并不常用
        select * from dept,emp;
        
    内连接查询:查询的是左边表和右边表都能找到对应记录的记录
        select * from dept,emp where dept.id = emp.dept_id;
        select * from dept inner join emp on dept.id=emp.dept_id;
    
    外连接查询:
        左外连接查询:在内连接的基础上增加左边表有而右边表没有的记录
            select * from dept left join emp on dept.id=emp.dept_id;
        
        右外连接查询:在内连接的基础上增加右边表有而左边表没有的记录
            select * from dept right join emp on dept.id=emp.dept_id;
        全外连接查询:在内连接的基础上增加左边表有而右边表没有的记录和右边表有而左表表没有的记录
            select * from dept full join emp on dept.id=emp.dept_id; -- mysql不支持全外连接
            可以使用union关键字模拟全外连接:
            select * from dept left join emp on dept.id = emp.dept_id
            union
            select * from dept right join emp on dept.id = emp.dept_id;
            
一、事务
    事务的概念:事务是指逻辑上的一组操作,这组操作要么同时完成要么同时不完成.
      
   事务的管理:默认情况下,数据库会自动管理事务,管理的方式是一条语句就独占一个事务.
                如果需要自己控制事务也可以通过如下命令开启/提交/回滚事务
                start transaction;
                commit;
                rollback;
                
               JDBC中管理事务:
                    conn.setAutoCommit(false);
                    conn.commit();
                    conn.rollback();
                    SavePoint sp = conn.setSavePoint();
                    conn.rollback(sp);
               
   事务的四大特性:一个事务具有的最基本的特性,一个设计良好的数据库可以帮我们保证事务具有这四大特性(ACID)
        原子性:原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。 
        一致性:如果事务执行之前数据库是一个完整性的状态,那么事务结束后,无论事务是否执行成功,数据库仍然是一个完整性状态.
            数据库的完整性状态:当一个数据库中的所有的数据都符合数据库中所定义的所有的约束,此时可以称数据库是一个完整性状态.
        隔离性:事务的隔离性是指多个用户并发访问数据库时，一个用户的事务不能被其它用户的事务所干扰，多个并发事务之间数据要相互隔离。
        持久性:持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来即使数据库发生故障也不应该对其有任何影响。
    
   隔离性:
        将数据库设计成单线程的数据库,可以防止所有的线程安全问题,自然就保证了隔离性.但是如果数据库设计成这样,那么效率就会极其低下.
        
        数据库中的锁机制:
            共享锁:在非Serializable隔离级别做查询不加任何锁,而在Serializable隔离级别下做的查询加共享锁,                              
                    共享锁的特点:共享锁和共享锁可以共存,但是共享锁和排他锁不能共存
            排他锁:在所有隔离级别下进行增删改的操作都会加排他锁,
                    排他锁的特点:和任意其他锁都不能共存
        
        如果是两个线程并发修改,一定会互相捣乱,这时必须利用锁机制防止多个线程的并发修改
        如果两个线程并发查询,没有线程安全问题
       
        如果两个线程一个修改,一个查询......
            四大隔离级别:
                Read uncommitted -- 不防止任何隔离性问题,具有脏读/不可重复度/虚读(幻读)问题
                Read committed -- 可以防止脏读问题,但是不能防止不可重复度/虚读(幻读)问题
                Repeatable read -- 可以防止脏读/不可重复读问题,但是不能防止虚读(幻读)问题
                Serializable -- 数据库被设计为单线程数据库,可以防止上述所有问题
        
                从安全性上考虑: Serializable>Repeatable read>read committed>read uncommitted
                从效率上考虑: read uncommitted>read committed>Repeatable read>Serializable
                
                真正使用数据的时候,根据自己使用数据库的需求,综合分析对安全性和对效率的要求,选择一个隔离级别使数据库运行在这个隔离级别上.
                mysql 默认下就是Repeatable read隔离级别
                oracle 默认下就是read committed个隔离级别
                
                查询当前数据库的隔离级别:select @@tx_isolation;
                设置隔离级别:set [global/session] transaction isolation level xxxx;其中如果不写默认是session指的是修改当前客户端和数据库交互时的隔离级别,而如果使用golbal,则修改的是数据库的默认隔离级别
                
        
      脏读:一个事务读取到另一个事务未提交的数据
            a 1000
            b 1000
            
            ----------
            a:
                start transaction;
                update account set money=money-100 where name=a;
                update account set money=money+100 where name=b;
            ----------
            b:
                start transaction;
                select * from account;
                    
                    a : 900
                    b : 1100
            ----------
            a:
                rollback;
            ----------
            b:
                start transaction;
                select* from account;
                    a: 1000
                    b: 1000
        
     不可重复读:在一个事务内读取表中的某一行数据，多次读取结果不同 --- 行级别的问题
               活期存款 定期存款  固定资产
            a:  1000       1000      1000
            b: 银行职员
            
            ---------
            b:start transaction;
            select 活期存款 from account where name='a'; ---- 活期存款:1000
            select 定期存款 from account where name='a'; ---- 定期存款:1000
            select 固定资产 from account where name='a'; ---- 固定资产:1000       
                -------
                a:(此时并发)
                    start transaction;
                    update accounset set 活期存款=活期存款-1000 where name='a';
                    commit;
                -------
            select 活期+定期+固定 from account where name='a';  --- 总资产:2000（对a来说理应三千）
            commit;
            ----------
        
     虚读(幻读):是指在一个事务内读取到了别的事务插入的数据，导致前后读取不一致 --- 表级别的问题
            a: 1000
            b: 1000
            d: 银行业务人员
            
            -----------
            d:
                start transaction;
                select sum(money) from account; --- 2000 元
                select count(name) from account; --- 2 个
                
                ------
                c:
                    start transaction;
                        insert into account values(c,4000);
                     commit;
                ------
               
                select sum(money)/count(name) from account; --- 平均:2000元/个
                commit;
            ------------
        
        更新丢失问题:
            两个线程基于同一个查询结果进行修改,后修改的人会将先修改人的修改覆盖掉.
            
            悲观锁:悲观锁悲观的认为每一次操作都会造成更新丢失问题,在每次查询时就加上排他锁select xx from oder where id=1 for update
                  
            乐观锁:乐观锁会乐观的认为每次查询都不会造成更新丢失.利用一个版本字段进行控制
             
                  查询非常多,修改非常少,使用乐观锁
                  修改非常多,查询非常少,使用悲观锁