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


