1.创建数据库
    create database 库名
2.创建并设置数据库编码
    create database 库名 character set 编码
3.查看数据库
    show create database 库名
4.删除一个数据库
    drop database 库名
5.使用或切换当前数据库
    use 库名
6.查看正再使用的数据库
    select database<>


1.创建表
    create table 表名(
        字段名 类型(长度) [约束],
        字段名 类型(长度) [约束],
        字段名 类型(长度) [约束]
    );
2.查看数据库有哪些表
    show tables
3.查看表的列信息
    desc 表名
4.删除一张表
    drop table 表名
5.添加、修改、删除列、或列信息
    alter table 表名 add 字段名 类型(长度) [约束]
    alter table 表名 modify 要修改的字段名 类型(长度) [约束]
    alter table 表名 change 旧列名 新列名 类型(长度) [约束]
    alter table 表名 drop 列名
6.修改表名
    rename table 表名 to 新表名
7.修改表的字符集
    alter table 表名 character set 编码
8.查看表的编码等信息
    show create table 表名
    
    
1.对表的增删改查
    insert into 表名(列名1,列名2,列名3...) values(值1,值2,值3...)
    insert into 表名 values(值1,值2,值3……)
    update 表名 set 字段名=值, 字段名=值, 字段名=值……
    update 表名 set字段名=值, 字段名=值, 字段名=值…… where 条件
    delete from 表名 where 条件
    select [distinct] *| 列名1，列名2 from 表名 [where条件]
        eg: select * from product as[可以省略] p(使用别名)
            select pname as[可以省略] p from product(使用别名)
            select distinct(price) from product(去掉重复值)
            select pname,price+10 from product;(所有的商品的价格+10进行显示)
            select pname from product where pname>xxx or pname<xxx;
            select pname from product where pname like %哈%; _ *  .  
            select pname from product where pname in (a, 6, 9)  
2.delete与truncate的区别
    delete删除的时候是一条一条的删除记录，它配合事务，可以将删除的数据找回。
    truncate删除，它是将整个表摧毁，然后再创建一张一模一样的表。它删除的数据无法找回。
3.排序
    select pname from product order by pname asc
    select pname from product order by pname desc
4.聚合函数
    select sum(price) from product
    select avg(price) from product
    select count(*) from product
5.查询总结
    select  一般在的后面的内容都是要查询的字段
    from  要查询到表
    where
    group by 
    having  分组后带有条件只能使用having
    order by 它必须放到最后面