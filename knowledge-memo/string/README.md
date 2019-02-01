# \* String

### **为什么Java中不能直接用 == 判等？**

Java中**String**类型具有一个**equals**的方法可以用于判断两种字符串是否相等，但是这种相等与运算符“==”所判断的“相等”有所不同。

* 使用==判断的相等时指相同的内存地址，也就是同一个对象实例。
* 使用equals方法判断的相等在不同的对象中实现不同，意义也不同。

Java中所有的对象都继承自**Object** 类，在**Object**类中实现的**equals\(\)** 方法如下：

```text
public boolean equals(Object obj) {  
    return (this == obj);  
}  
```

也就是等同于“==”, 只有在内存一样的时候才返回true。

* String类重写了这个方法，重写后的方法首先判断内存地址是否一致，如果一致返回true，否则比较字符串的内容是否一致，如果内容一致也返回true。因此，**使用String类的equals方法是比较内容是否一致，而使用“==”是比较实例是否是同一个实例**。
* StringBuilder类并没有重写equals方法，因此使用equals比较时，需要是同一个实例才会返回true，否则返回false。

### **Java创建字符串的过程**

在我们使用“=”赋值时，如果内存中已经有这个字符串，就会直接将其地址给这个变量，不会产生新的字符串。

当我们使用“+”或者“concat”方法拼接字符串的时候，会创建一个新的字符串，占用新的内存空间，因此使用“==”判断时返回false。

### **Java 中String的引用方式**

```java
public class Hello {
    public static void main(String argv[]) {
        String sa = "abc";
        String sb = "abc";
        if (sa == sb) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}
```

上面这段代码的结果是Yes。程序运行的过程是这样，先在内存中创建字符串“abc”, 然后将地址的引用给了变量sa， 随后又把这个地址的引用给了sb。因此sa和sb引用的是同一段内存。  
由于String类是一个不可更改的类。字符串不可被更改，所以这样的方式并不会产生问题。

### null 和 ““

```java
String s = null; //空对象
```

说明我们只是定义了s这个变量，只是在栈内存中标记了这个变量的存在，但是并没有实际分配任何堆内存给这个变量，变量没有指向的地址，是个空对象。

```java
String s = ""; //空串
```

这个声明中，s不是空对象，是指向实实在在的堆内存的。只是这段内存中没有数据而已，s此时是个空串。

### 常用操作

* substring, 取子字符串
* startsWith, 判断一个字符串是否以某个字符串开头
* endsWith, 判断一个字符串是否以某个字符串结尾
* compareTo, 比较两个字符串的大小，一般用于按照字典序排序字符串
* indexOf，查询一个字符串里另外一个字符串第一次出现的位置
* lastIndexOf, 查询一个字符串里另外一个字符串出现的最后一个位置
* format, 格式化字符串

