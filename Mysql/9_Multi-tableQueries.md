# Multi-table queries

### `union`

合并两条`sql`的结果集，会 删去重复的数据

```mysql
select [fields] from [table_name] union (all / distinct)
select [fields] from [table_name];
#  要求两个结果集的列数相同
```



### `inner join`(常用写全)

##### 内连接

```mysql
select [fields] from  [table_name] inner join [table_name] [table.field]=[table.field];
#  显示两个表里面都有的数据
#  [table.field]=[table.field]建立公共字段
```

注：

- 建立公共字段写法无法省略
- `inner join`可以联合更多的表



### `left join`

##### 左连接，以左表为基准，基本用法类似`inner join`

### `right join`



### `cross join`

##### 交叉

```mysql
select * from [table_name] cross join [table_name];
#  返回笛卡尔积
select * from [table_name] cross join [table_name] where [table.field]=[table.field];
#  该用法相当于内连接
```



### `natural join`

##### 自然连接

```mysql
select * from [table_name] natural (right / left) join [table_name];
#  根据同名字段创建公共字段
#  如果不含同名字段返回笛卡尔积
```



### `using`

指定连接的字段

```mysql
select * from [table_name]  inner join [table_name] using(field);
#  以某一字段为准不重复
#  存在多个相同字段，指定连接字段
```

