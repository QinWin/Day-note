Java
====================================================================================================
### java 温故知新

一个Java源码只能定义一个public类型的class，并且class名称和文件名要完全一致；
一个.java文件只能包含一个public类，但可以包含多个非public类。如果有public类，文件名必须和public类的名字相同。

类名规范  英文字母（best 首字母大写），数字，下划线
方法名规范  英文字母（best 首字母小写），数字，下划线

java中用补码表示二进制数，补码的最高位是符号位，最高位为“0”表示正数，最高位为“1”表示负数。
<原码>就是二进制定点表示法，即最高位为符号位，“0”表示正，“1”表示负，其余位表示数值的大小。
     原码就是符号位加上真值的绝对值, 即用第一位表示符号, 其余位表示值.
<反码>表示法规定：正数的反码与其原码相同；负数的反码是对其原码逐位取反，但符号位除外。
<补码>表示法规定：正数的补码与其原码相同；负数的补码是在其反码的末位加1。

变量  常量（常量在定义时进行初始化后就不可再次赋值，再次赋值会导致编译错误。）
基本类型  引用类型

& | ！ ^ 异或运算的规则是，如果两个数不同，结果为1，否则为0


可变参数(String...parameter)可以保证无法传入null，因为传入0个参数时，接收到的实际值是一个空数组而不是null。

基本类型参数的传递，是调用方值的复制。双方各自的后续修改，互不影响。
引用类型参数的传递，调用方的变量，和接收方的参数变量，指向的是同一个对象。双方任意一方对这个对象的修改，都会影响对方（因为指向同一个对象嘛）

如果我们自定义了一个构造方法，那么，编译器就不再自动创建默认构造方法
在Java中，任何class的构造方法，第一行语句必须是调用父类的构造方法。如果没有明确地调用父类的构造方法，编译器会帮我们自动加一句super();
如果父类没有默认的构造方法，子类就必须显式调用super()并给出参数以便让编译器定位到父类的一个合适的构造方法。
即子类不会继承任何父类的构造方法。子类默认的构造方法是编译器自动生成的，不是继承的。

方法名相同，但各自的参数不同，称为方法重载（Overload）。
在继承关系中，子类如果定义了一个与父类方法签名完全相同的方法，被称为覆写（Override）。
注意：方法重载的返回值类型通常都是相同的。
注意：方法名相同，方法参数相同，但方法返回值不同，也是不同的方法。在Java程序中，出现这种情况，编译器会报错。
多态(Polymorphic)——》多态的特性就是，运行期才能动态决定调用的子类方法。
如果一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为final。
用final修饰的方法不能被Override, 用final修饰的类不能被继承, 用abstract修饰的类方法只能被继承
因为静态方法属于class而不属于实例，因此，静态方法内部，无法访问this变量，也无法访问实例字段，它只能访问静态字段。
interface是可以有静态字段的，并且静态字段必须为final类型

这种把一个子类类型安全地变为父类类型的赋值，被称为向上转型（upcasting）。
向上转型相反，如果把一个父类类型强制转型为子类类型，就是向下转型（downcasting）。（ClassCastException instanceof)

object几个重要的方法  toString() equals() hashCode()

Java的接口特指interface的定义，表示一个接口类型和一组方法签名，而编程接口泛指接口规范，如方法签名，数据格式，网络协议等。
一般来说，公共逻辑适合放在abstract class中，具体逻辑放到各个子类，而接口层次代表抽象程度。

修饰字段 final(常量，定义时初始化，构造时初始化) static(共享空间，关联类持有一份) 


在Java虚拟机执行的时候，JVM只看完整类名，因此，只要包名不同，类就不同。
包没有父子关系。java.util和java.util.zip是不同的包，两者没有任何继承关系。

Java编译器在编译期，会自动把所有相同的字符串当作一个对象放入常量池
从String的不变性设计可以看出，如果传入的对象有可能改变，我们需要复制而不是直接引用。
Java的String和char在内存中总是以Unicode编码表示。
字符串操作不改变原字符串内容，而是返回新字符串；
char  String  StringBuilder(高效拼接字符串) StringBuffer(线程安全版本) StringJoiner


对于较小的数，始终返回相同的实例(-128 -0- 127)

枚举类的字段也可以是非final类型，即可以在运行期修改，但是不推荐这样做！
enum的构造方法要声明为private，字段强烈建议声明为final；

比较BigDecimal的值是否相等，必须使用compareTo()而不能使用equals()

Math.random() 0 <= x < 1
SecureRandom就是用来创建安全的随机数的


反射是为了解决在运行期，对某个实例一无所知的情况下，如何调用其方法
反射获取权限setAccessible(true)可能会失败。如果JVM运行期存在SecurityManager，那么它会根据规则进行检查，有可能阻止setAccessible(true)。
如果获取到的Method表示一个静态方法，调用静态方法时，由于无需指定实例对象，所以invoke方法传入的第一个参数永远为null。
使用反射调用方法时，仍然遵循多态原则：即总是调用实际类型的覆写方法（如果存在）
getInterfaces()只返回当前类直接实现的接口类型，并不包括其父类实现的接口类型
如果是两个Class实例，要判断一个向上转型是否成立，可以调用isAssignableFrom()

@interface
Java的注解本身对代码逻辑没有任何影响。
注释会被编译器直接忽略，注解则可以被编译器打包进入class文件，因此，注解是一种用作标注的“元数据”。
有一些注解可以修饰其他注解，这些注解就称为元注解（meta annotation）@Target  @Retention @Repeatable @Inherited(继承父类定义的Annotation)

