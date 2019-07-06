# Java基础
**1.什么是字节码？它对Java的Internet程序设计为何十分重要？**

字节码是一种高度优化的指令集，由Java虚拟机执行，可以帮助Java获得可移植性和安全性。

**2.面向对象程序设计的三个主要原则是什么？**

封装、多态性和继承。

**3.Java程序从何处开始执行？**

main()

**4.什么是变量？**

变量是一种命名的内存地址，变量的内容可以在程序运行时修改。

**5.下面哪几个变量是无效的？**

  **A.count**
  **B.$count**
  **C.count27**
  **D.67count**

D

**6.如何创建单行注释与多行注释？**

**7.写出if语句和for循环的基本形式。**

if(condition) statement;

for(initialization; condition; iteration) statement;

**8.如何创建代码块？**

{}

**9.月球重力为地球重力的17%。编写一个程序来计算你在月球上的实际体重。**

```java
class Moon {

     public static void main(String[] args) {

         double earthweight; // weight on earth

         double moonweight; // weight on moon
         
         earthweight = 165;

         moonweight = earthweight * 0.17;

         System.out.println("The weight on moon is " + moonweight);
     }
}
```

**10.如果在输入程序时犯了输入错误，这会导致什么类型的错误？**

语法错误。

**11.语句在一行中的放置位置有限制吗？**

没有限制。


 
