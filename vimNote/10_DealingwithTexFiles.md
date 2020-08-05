# 处理文本文件

### 自动换行

`:set textwidth=30 `

- 根据文本宽度换行

`:set wrapmargin=margin`

- 中断此行，防止有来自屏幕右侧的空白字符



### 格式化

`gq`

##### 居中

`:range center width`

`:range left margin`

##### 外部引用

`:source $VIMRUNTIME/macros/justify.vim`

##### 行间合并

`J`

- 合并两行内容，中间使用空格分割

##### `formatoptions`

控制vim如何执行自动包装

- 控制文本和注释的包装方式

`:set formatoptions=characters`

- `t`
  - 自动换行
- `c`
  - 自动包装，自动插入注释
- `r`
  - 换行后，加入注释`#`
- `o`
  - 使用插入命令`o` `O`加入注释
- `q`
  - 允许使用`gq`
- `2`
  - 缩进格式参考第二行
- `v`
  - `vi`,只在空格上操作
- `b`
  - 只在空格上换行，该命令在`textwidth`之前才生效
- `1`
  - 在插入模式下不自动换行，`gq`可以

###### 返回到原始段落

`:set formatoptions += 2`



### 使用外部格式化程序

`:set formatprg=fmt`

##### 运行一个段落

`!}fmt`



##### 文件格式

`:set fileformats=unix,dos`

`:set fileformat?`



##### 改变最后一行的结束方式

更改文件是否以`<EOL>`结尾

`:set endofline`

`:set noendofline`