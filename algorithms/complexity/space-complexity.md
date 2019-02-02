# space complexity

空间复杂度就是衡量算法运行时所占用的临时存储空间的度量。

算法所占用的空间主要有三个方面：算法代码本身占用的空间、输入输出数据占用的空间、算法运行时临时占用的空间。其中，代码本身和输入输出数据占用的空间不是算法空间复杂度考虑的范围内，空间复杂度**只考虑运行时临时占用的空间**，又称为算法的额外空间（Extra space）。

临时占用的空间包括为参数列表中形参变量分配的空间和为函数体中局部变量分配的空间

### 运行时堆栈

递归函数需要保存当前的环境，以便在递归返回的时候能够还原之前的现场。因此递归的深度越深，所要占用的栈空间越大。当空间超出一定范围的时候就会出现程序**爆栈**（Stack Overflow）的情况。堆栈空间应该是与递归的深度成正比（此处只讨论单线程）。

### 大部分计算方法

累加下面两个部分：

1. 你的代码里开辟了多少新的空间（new 了多少新的内容出来）
2. 你的递归深度 \* 递归函数内部的参数和局部变量所占用的空间

### Examples

{% tabs %}
{% tab title="Code" %}
```java
int Fibo(int n) {
    if(n == 0 || n == 1) return 1;
    return Fibo(n-1) + Fibo(n-2);
}
```
{% endtab %}

{% tab title="Ans" %}
O\(n\), 最多调用n次
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Code" %}
```java
int Fibo(int n) {
    int x1 = 1, x2 = 1, ret = 1;
    for(int i = 2; i <= n; i++){
        ret = x1 + x2;
        x1 = x2;
        x2 = ret;
    }
    return ret;
}
```
{% endtab %}

{% tab title="Ans" %}
O\(1\)
{% endtab %}
{% endtabs %}

