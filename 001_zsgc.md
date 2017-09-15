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