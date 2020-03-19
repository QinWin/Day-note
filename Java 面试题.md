1:
  Integer i = 42;
  Long l = 42l;
  Double d = 42.0;
  下面为true的是

  A.(i == l)
  B.(i == d)
  C.(l == d)
  D.i.equals(d)
  E.d.equals(l)
  F.i.equals(l)
  G.l.equals(42L)

 正确答案: G
 解析：同类型的进行比较，如Integer 与int，Long与long进行==比较时，会自动拆箱；不同类型之间进行比较，
   如果有一方为非包装类，则会自动拆箱。如果两方都为包装类，则不会拆箱，且不能比较，编译会报错
2:
What will happen when you attempt to compile and run the following code?
public class Test{
static{
   int x=5;
}
static int x,y;
public static void main(String args[]){
   x--;
   myMethod( );
   System.out.println(x+y+ ++x);
}
public static void myMethod( ){
  y=x++ + ++x;
 }
}

A.compiletime error
B.prints:1
C.prints:2
D.prints:3
E.prints:7
F.prints:8

正确答案: D
解析：1.静态语句块中x为局部变量，不影响静态变量x的值
      2.x和y为静态变量，默认初始值为0，属于当前类，其值得改变会影响整个类运行。
   3.java中自增操作非原子性的
   main方法中：
   执行x--后 x=-1
   调用myMethod方法，x执行x++结果为-1(后++)，但x=0，++x结果1，x=1 ，则y=0
   x+y+ ++x,先执行x+y，结果为1，执行++x结果为2，得到最终结果为3

4：
以下哪些类是线程安全的（）

A.Vector
B.HashMap
C.ArrayList
D.StringBuffer
E.Properties

正确答案: A D E
解析：A，Vector相当于一个线程安全的List
   B，HashMap是非线程安全的，其对应的线程安全类是HashTable
   C，ArrayList是非线程安全的，其对应的线程安全类是Vector
   D，StringBuffer是线程安全的，相当于一个线程安全的StringBuilder
   E，Properties实现了Map接口，是线程安全的
   
5:
Java中的集合类包括ArrayList、LinkedList、HashMap等，下列关于集合类描述错误的是？
A.ArrayList和LinkedList均实现了List接口
B.ArrayList的访问速度比LinkedList快
C.随机添加和删除元素时，ArrayList的表现更佳
D.HashMap实现Map接口，它允许任何类型的键和值对象 

正确答案: C
解析：ArrayList 查询快，增删慢  LinkedListed 相反
关于D选项“HashMap实现Map接口，它允许任何类型的键对象” 这句话是有前提条件的。 这需要
查看HashMap底层源码，在计算hashcode的过程中会用到equals（）和hashCode（）这两个函数；所以键的对象
类型必须遵守这两个函数的规则，保证键的不变性
同时HashMap 存放键值对时，首先会检查是否存在键值，若存在则覆盖，不存在就创建

6：
在Java中，对于不再使用的内存资源，如调用完成的方法，“垃圾回收器”会自动将其释放。（  ）

A.正确
B.错误

正确答案: B 
解析：JVM 内存可简单分为三个区：
   
   1、堆区（heap）：用于存放所有对象，是线程共享的（注：数组也属于对象）
   
   2、栈区（stack）：用于存放基本数据类型的数据和对象的引用，是线程私有的（分为：虚拟机栈和本地方法栈）
   
   3、方法区（method）：用于存放类信息、常量、静态变量、编译后的字节码等，是线程共享的（也被称为非堆，即 None-Heap）
   
   Java 的垃圾回收器（GC）主要针对堆区
  
7:
 
 
8:
下列程序的输出结果是什么？
public class Test1{
    public static void main(String args[]){
            String a="1234";
            String b="1234";
            String c = new String("1234");
            System.out.println(a==b);
            System.out.println(a==c);
            System.out.println(a.equals(c));
    }
} 

正确答案：true \n false \n true
解析：第一次String a="1234"时，会在常量池中创建一个常量1234,String b=1234时，常量池中已经有了该常量，
所以直接取，a和b的地址一样，所以地址值相等；String c = newString("1234")重新new了对象，在堆内存中开辟
了新的空间，所以地址值不相等，而String的equals方法重写了比较的是值是否相等。

9：
Java 程序中使用赋值运算符进行对象赋值时，可以得到两个完全相同的对象。
  
A.正确
B.错误

正确答案: B   
解析：是两个不同的引用指向同一个对象          


10：
定义有StringBuffer s1=new StringBuffer(10);s1.append(“1234”)则s1.length()和s1.capacity()分别是多少?

A.4   10
B.4   4
C.10  10
D.10  4

正确答案: A 
解析：length 返回当前长度。如果字符串长度没有初始化长度大，capacity返回初始化的长度。如果append后的字
符串长度超过初始化长度，capacity返回增长后的长度。

11:
下面那些情况可以终止当前线程的运行？

A.当一个优先级高的线程进入就绪状态时
B.抛出一个异常时
C.当该线程调用sleep()方法时
D.当创建一个新线程时

正确答案: B  
解析：B：p thread_clean_pop抛出一个例外，线程终止！也可以通过其他线程调用p thread_cancel（）函数来终止
另一个线程
 A：并不是终止，而是抢占，进程是资源分配的最基本单位，同一个进程创建的不同线程共享这些资源。所以这些
 线程能使用的资源是有限的。当某一个线程优先级比较高时，它就会抢占其他线程的资源，导致其他线程没有资源
 可用，会造成阻塞，直到那个优先级高地线程使用完。 
 
 12:
 ArrayList list = new ArrayList(20);中的list扩充几次
    
  A.  0
  B.  1
  C.  2
  D.  3
    
 正确答案: A   
 解析：ArrayList的构造函数总共有三个：
    （1）ArrayList()构造一个初始容量为 10 的空列表。
    （2）ArrayList(Collection<? extends E> c)构造一个包含指定 collection 的元素的列表，这些元素是按照
    该 collection 的迭代器返回它们的顺序排列的。
    （3）ArrayList(int initialCapacity)构造一个具有指定初始容量的空列表。
 
13:
在开发中使用泛型取代非泛型的数据类型（比如用ArrayList<String>取代ArrayList），程序的运行时性能会变得更好。（） 

A.正确
B.错误    

正确答案: B   
解析：1，类型安全。 泛型的主要目标是提高 Java 程序的类型安全。通过知道使用泛型定义的变量的类型限制，
编译器可以在一个高得多的程度上验证类型假设。没有泛型，这些假设就只存在于程序员的头脑中（或者如果幸运的话，
还存在于代码注释中）。
   2，消除强制类型转换。 泛型的一个附带好处是，消除源代码中的许多强制类型转换。这使得代码更加可读，
   并且减少了出错机会。
   3，潜在的性能收益。 泛型为较大的优化带来可能。在泛型的初始实现中，编译器将强制类型转换（没有泛型的话，
   程序员会指定这些强制类型转换）插入生成的字节码中。但是更多类型信息可用于编译器这一事实，为未来版本的 
   JVM 的优化带来可能。由于泛型的实现方式，支持泛型（几乎）不需要 JVM 或类文件更改。所有工作都在编译器中完成，
   编译器生成类似于没有泛型（和强制类型转换）时所写的代码，只是更能确保类型安全而已。
   所以泛型只是提高了数据传输安全性，并没有改变程序运行的性能
   
14：
下面的方法，当输入为2的时候返回值是多少?
public static int getValue(int i) {
        int result = 0;
        switch (i) {
        case 1:
            result = result + i;
        case 2:
            result = result + i * 2;
        case 3:
            result = result + i * 3;
        }
        return result;
}
 
A.0
B.2
C.4
D.10   

正确答案: D 
解析：switch结构中case若没有break,则从匹配上的case执行到第一个break或者结尾。