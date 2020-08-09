# Other

### 视图

- 数据库管理部分，隐藏敏感数据
- 隐藏表的结构，在某种程度上简化数据表

##### 创建

```mysql
create view [view_name] as select [fields] from [table_name];
```

##### 查看 

```mysql
select * from [view_name];	
```

##### 显示

```mysql
show tables;
#  其中会展示试图，在终端下为了区分一般视图创建时添加前缀

show table status where comment='view' \G
```



##### 修改视图

```mysql
alter view [view_name] as select [fields] from [table_name];
#  直接将`create`改为`alter`可以更新视图
```

##### 删除

```mysql
drop view [view_name];
```

##### 视图算法

- 合并
- 临时表

```mysql
algorithm=
#  三种定义算法：undefined、merge、temptable（子查询调整算法保障结果）
```





### 事务（transaction）

更钱等较严格的操作（确定操作）

##### 开启事务

```mysql
start transaction;
```



##### 回滚

```mysql
rollback;

#   设置回滚点
savepoint [point_name];
rollback to [point_name];
```



##### 提交事务

```mysql
commit;
```



##### ACID

- atomicity
  - 原子性
- consistency
  - 一致性
- isolation
  - 隔离性
- durability
  - 持久性



### 索引（index）

- 方便查询 
- 改动效率低
- 占空间

##### 主键索引

##### 唯一键索引

##### 普通索引

##### 全局索引（不一定支持中文——sphinx）



##### 创建索引

```mysql
create index [index_name] on [table_name]([field]);

#  设置唯一/主键索引
create (unique / primary key) index [index_name] on [table_name]([field]);
```

##### 更改（alter）

```mysql
alter table [table_name] add [index_name] ([field]); 
```



##### 删除（drop）

```mysql
drop index [index_name] on [table_name];
```



### 存储过程（函数）

模块化设计

```mysql
delimiter //
#  改变sql语句结尾字符

#  创建存储过程
create procedure proc()
begin
[sql]
end //

#  调用存储过程
call pro();

#  查看存储过程
show create procedure proc;
```



### 函数

##### 随机数

```mysql
select rand();

select * from student order by rand() limit 3;

#  向上取整
select ceil();

select round();

select  floor();


select ucase();

select lcase();

select left / right (String, wideth);

select substring (-,-,-);

select concat();

select now();

select unix_timestamp();

select sha();
```

