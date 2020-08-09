# Column properties

### 主键（`primary key`）

- 绝对唯一
- 确定数据存在性
- 加快查询数据的速度
- 表关联的依据

注：

- 主键不可以为空（设置自动增长除外）
- 一般主键设置为改动少的



##### 添加主键

```mysql
alter table [table_name] add primary key [field];
```

##### 删除主键

```mysql
alter table [table_name] drop primary key [field];
```

##### 设置组合主键

```mysql
alter table [table_name] add primary key [fields];
#  作用不大，一般使用
#  案例：文章区分
```



### 唯一键

- 可以为空
- 可以有多个
- 保障数据不会重复

##### 添加唯一键

```mysql
alter table [table_name] add unique [field];
```

##### 添加组合唯一键

##### 删除唯一键

```mysql
alter table [table_name] drop index [field];
```



### 注释

- 代码注释
- SQL内注释

##### 单行注释

- `#`
- `--`

##### 多行注释

- `/* */`

##### 其他方式

- `comment '---'`

##### 查看注释

```mysql
show create table [table_name];
```



##### 数据完整性

- 保证一张表里面有一个主键（唯一的约束）
- 数据类型合理性
- 空和非空
- `Default`
- 是否需要被外部引用



### 外键 

##### 创建表示添加外键

```mysql
foreign key [field] references [table_name]([field]);
#  并发项目中一般禁止使用外键 
```

##### 添加外键

```mysql
alter table [table_name] add foreign key [field] references [table_name] ([field]);
```

注：一般不使用更新表的手段，表的大体结构在创建是基本确定

##### 删除外键

```mysql
show create table [table_name];
#  找到该字段的别名
alter table [table_name] drop foreign key [alias];
```

##### 操作

- 置空表
  - 不删除，改为空
- 级联
  - 全部改变，主要用于外界更新

```mysql
alter table [table_name] add foreign key [field] references [table_name] ([field]) on delete set null on update cascade;
#  删除时置空，更新时级联
```