# Child-tableQuery

### 子查询

```mysql
select * from [table_name] where [field]=(select [field] from [table_name] where [field]);
#  `=` 子查询返回一个数据，如果返回多个数据使用`in`,`not in`

select * from [table_name] where exists (select [field] from [table_name] where [field]);
#  存在显示全部
```

