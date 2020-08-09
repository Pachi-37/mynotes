# Single table query	

### `select`

```mysql
select 'name';
#  |name|
#  |name|
select 2*7
#  |2*7|
#  |14 |

#  将查询部分作为字段名，查的内容可能是源内容，有可能是经处理之后的结果
```

​	

### 别名使用

```mysql
select a as b;
#  |b|
#  |a|

# as可以省略 
```



### `from`

```mysql
select * from [table_name],[table_name];
#  主要返回笛卡尔积,没什么用
```



### `dual`

```mysql
select 2*7 as rel from dual;
#  dual默认的伪表
```



### `where`

##### 条件筛选

- `=`
- `!=`
- `>`
- `<`
- `and`
- `or`
- `not`

```mysql
# in & not in
select 	* from [table_name] where [field] in ();
select 	* from [table_name] where [field] or [field];
```

##### `between and` `not between and`

##### `not null`

```mysql
# 查询字段为空不能直接使用`=`，使用关键字查询
select * from [table_name] where [field] is null;
```





### 聚合函数

统计时使用

```mysql
select sum(field) from [table_name];
avg,max,min,count
 
# count(*)与count(1)问题
```



### 模糊查询

```mysql
select * from [table_name] where [field] like value;
#  % 代表多个字符
#  _ 代表一个字符
```



##### 排序

```mysql
select * from [table_name] order by [field] asc;
#  asc 升序，默认
#  desc 降序
```



##### 分组统计

```mysql
select avg([field]) as 'score', [field] as '性别' from [table_name] group by [field];
#  使用该函数要保证查询的字段为分组字段和聚合函数

select group_concat([field]),[field] from [table_name] group by [field];
#  聚合显示所有查询
```



##### `having`

- `where`查询是从表里面开始一条一条进行筛选找出符合条件的，无法查询虚拟表
- `having`可以在之前结果上查询显示，用法和`where`基本一致，但是需要注意别名

##### `limit`

取数从哪里开始到哪里结束

```mysql
select * from [table_name]  limit 0,2;
#  第一条开始查询两个
#  1，3从第二条数据开始向后查询三个
#  起始位置，跨度
```



##### `distinct`

- 去重
- 默认情况下有`all`(省略)