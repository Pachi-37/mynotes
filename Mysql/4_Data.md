# Data

### 插入数据

```mysql
insert into [table_name] ([fields]) values ([]);
#  要求数据顺序与前面字段排序相对应
#  字段排序可以省略，但是插入值时要与仓库字段对应
#  相关只可以为空，如果不填按default否则为null
#  插入多行数据，直接使用`,``分隔
```

### 查询数据

```mysql
select * from [table_name];
select [fields] from [table_name];
```

### 删除数据

```mysql
delete from [table_name] where [field [operation] value];
#  opereation: `=` `>`  `<`
#  尽量使用唯一的标识来删除数据
```

### 清空表数据

```mysql
#  一般删除数据不建议使用删除操作，删除操作要先遍历速度较慢，并且无法覆盖主键信息，一般直接重置数据表
truncate table [table_name];
```

### 更新数据表

```mysql
update [table_name] set [field=[value]] where [field=value];
#  可以同时更改多个字段的值
#  如果后面没有加上`where`数据库数据全部被更改
#  `where`可以使用 `or` `and` 来调整范围
```





### 基础部分知识小结：

##### `DDL`

- `date definition language`
  - `create`
  - `alter`
  - `drop`
  - `show`

##### `DML`

- `data manipulation language`
  - `insert`
  - `update`
  - `delete`
  - `select`

##### 字符集编码

```mysql
show variables like 'character_set_%';
#  保证`character_set_client` `character_set_results`字符编码一致（Win）
#  实际开发全部为`utf-8`
```

