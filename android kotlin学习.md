
====================================================================
1, var val
lateinit
  必须是可读且可写的变量，即用var声明的变量
  不能声明于可空变量。
  不能声明于基本数据类型变量。例：Int、Float、Double等，注意：String类型是可以的。
  声明后，在使用该变量前必须赋值，不然会抛出UninitializedPropertyAccessException异常。

lazy
   使用lazy{}高阶函数，不能用于类型推断。且该函数在变量的数据类型后面，用by链接。
   必须是只读变量，即用val声明的变量。

const 常量

2，Byte 1 Short 2 Int 4 Long 8  Float 4 Double 8
   0x十六进制  0b二进制
   大于127其内存地址不同，反之则相同。这是`kotlin`的缓存策略导致的，而缓存的范围是` -128 ~ 127 `。

   Boolean
   Char

   String
   包含转义字符的字符串 转义包括（\t、\n等）,不包含转义字符串的也同属此类型
   包含任意字符的字符串 由三重引号（""" …. """）表示
   使用字符串模板的符号为（$）。在$符号后面加上变量名或大括号中的表达式

   Array  arrayOf()  arrayOfNulls()  工厂函数（Array()）


3, if  在Kotlin中其实是不存在三元运算符(condition ? then : else)  这种操作可用if替代
   for  until[n,m)  downTo[n,m] ..[n,m]  step
   while  do..while
   when   is(!is)   in (!in)

   return break continue

4, class fun

   init

   open abstract  data  sealed   inner

   object  companion object   Any

   this super  override

   enum interface
