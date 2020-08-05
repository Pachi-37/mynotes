# Data Type

### 整数类型

- `UNSIGNED`

- `TINYINT`
- `SMALLINT`
- `MEDIUMINT`
- `INT`  `INTERGER`

### 浮点型

- `FLOAT`

- `DOUBLE`

  ```mysql
  [field] double(3,1);
  #  整数位数必须大于小数位数
  ```

> 浮点数会导致精度丢失

##### `DECIMAL`

防止丢失精度



### 字符串

- `CHAR`
  - 定长字符串
- `VARCHAR`
  - 变长字符串，可以自动回收未使用的字节，效率比`CHAR`低

### 文本（略）

### 布尔类型

### 枚举类型

```mysql
[field] enum([value]);
#  插入数据时只可以填写列出的选项
#  每个选项对应一个数字，数字从`1`开始
```

### Set类型

与枚举类型相似，但是可以存取多个

```mysql
[field] set(value);
select into [table_name] value();
#  注：此处存储的为一个字段数据`''`,`'',''`两个字段
#  分配数字从左向右按`2^n`
```



### 时间日期

- `DATE`

- `TIME`
- `YEAR`
- `DATETIME`
  - 一般情况使用

```mysql
[field] datetime;
insert into [table_name] values('2020-04-05');
#  注：插入时系统自动补充当前时间
```



- `TIMESTAMP`