### 显示所有的表

`show tables;`



### 创建表

```mysql
create table [name](
   id int,
   name varchar()
);

create table if not exists [name](
id int primary key auto_increment comment 'comment',
   name  varchar() not null comment '',
   address varchar() default '' comment '',
)engine=innodb;
```

### 查看表信息

```mysql
show create table [name];        # SQL语句
desc [name];                     # 结构展示
```



### 删除表

```mysql
drop table if not exists [table_name];
```



### 修改表

```mysql
#  添加字段
alter table [table_name] add [field] ([address]);
after before first

#  删除字段
alter table [table_name] drop [field];

#  修改字段
alter table [table_name] change [old_field] [field][type];

#  修改字段类型
alter table [table_name] modify [field] [type];

#  表改名
alter table [table_name] rename to [table_name];	
```

