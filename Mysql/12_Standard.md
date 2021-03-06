# Standard

### 字段规范

##### 判断是否

- 字段名必须以`is_`前缀开头（Java里面不一样）
- 字段类型必须保障为`unsigned tinyint`
- 长度为`1`

##### 表名字段名强制全部小写字母，不能数字开头，分割单词使用下划线（Linux下区分大小写）

##### 表

- 表名不可以出现复数

- 关键字不可用作表名
- 每张表里面强制包含三个字段
  - `id`必须为主键，类型为`unsigned bigint`，单表必须自增（除非分布式）
  - `create_time`必须为`datatime`类型
  - `update_time`必须为`datatime`类型

##### 索引名

- 主键索引名一般以`pk_`开头

- 唯一键索引`uk_`
- `idx_`

##### 小数

- 禁止使用浮点，全部使用`decimal`

##### 字符串

- 定义的字符串长度较小的时候使用`char`
- 大数据使用`text`



#### 其他

表名与业务名最好相关

仓库名一般与应用名保持一致

频繁查询字段允许适当的冗余

单表行数超过500万行或5G分库分表



### 索引

在业务或流程上有唯一特性的字段，应该设置唯一索引

- 提高查找速度
- 校验性提高，预防脏数据 

- 在 `varchar`建立索引，指定长度（文本区分度）
- 多表关联查询

`join`最多只允许两个表关联查询，数据类型必须一致

关联查询时保证关联查询的字段也有索引



### SQL

`count`

```mysql
count(*) >> count([fields]);
#  count(*)可以统计null
```

不允许使用`=`来判断`null`

```mysql
where name=null;
# 使用ISNULL(expr)函数
select * from [table_name] where [field] is null;
```

不能使用外键和级联（并发不允许，应用层解决）

不允许使用存储过程

更改数据前先查询

子查询里面`in`避免使用

`utf-8`