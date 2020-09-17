# String &  StringBuilder

### String 存在的问题
* String一旦创建对象之后就不能改变字符串的值
     * String 遗留的问题
        * 一旦创建无法被修改
        * 进行追加修改的操作，将会重新创建对象（内存）
> 字符串1 = 字符串1 + 字符串2 前后两个字符串不是一个字符串
* StringBuilder
    *  字符串进行频繁的修改

* StringBuffer
    * 涉及到线程安全时使用，大部分情况下因为其速度比不上 `StringBuilder`

### 链式调用
* 对象方法，对象方法连续调用的写法