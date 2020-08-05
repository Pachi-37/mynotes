# 数据库的基本操作

### 仓库

##### 查看

- `show databases;`

##### 创建

-  正常写法

  `create database [name] ;`

-  防报错写法

  `create database if not exists [name];`

-  创建数据仓库时规定时不能使用关键词，但是也可以创建如果使用 ` `` ` 将仓库名括起来

- 指定字符编码
  ` charset=gbk    `   

  -   window上使用`gbk`（`cmd`为`gbk`），实际开发工程中使用`UTF-8`

##### 删除

- 删除数据仓库

`drop database [name];`

`drop database if exists [name];`

##### 查看仓库信息

- 查看创建仓库时使用的SQL语句

`show create database [name];`

##### 修改字符编码

`alter database [database_name] charset=`

##### 使用

`use [database_name]`

