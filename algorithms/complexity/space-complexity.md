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

### Heap and Stack Space

当一个程序在执行的时候，操作系统为了让进程可以使用一些固定的不被其他进程侵占的空间用于进行函数调用，递归等操作，会开辟一个固定大小的空间（比如 8M）给一个进程使用。这个空间不会太大，否则内存的利用率就很低。这个空间就是栈空间，Stack space。栈溢出（Stack Overflow）是指在函数调用，或者递归调用的时候，开辟了过多的内存，超过了操作系统余留的那个很小的固定空间导致的。

栈空间主要包含如下几个部分：

1. 函数的参数与返回值
2. 函数的局部变量

#### Example

{% tabs %}
{% tab title="Code" %}
```java
public int f(int n) {
    int[] nums = new int[n];
    int sum = 0;
    for (int i = 0; i < n; i++) {
        nums[i] = i;
        sum += i;
    }
    return sum;
}
```
{% endtab %}

{% tab title="Notes" %}
根据我们的定义，参数 n，最后的函数返回值f，局部变量 sum 都是放在栈空间里的。那么主要的难点在 nums。这里 nums 可以理解为两个部分：

1. 一个名字叫做 nums 的局部变量，他存储了指向内存空间的一个地址（Reference），这个地址也就是 4 个字节（32位地址总线的计算机，地址大小为 4 字节）。
2. new 出来的，一共有 n 个位置的整数数组，int\[n\]。一共有 4 \* n 个字节。

这里 nums 这个变量本身，是存储在栈空间的，因为它是一个局部变量。但是 nums 里存储的 n 个整数，是存储在堆空间里的。它并不占用栈空间，并不会导致栈溢出。

在大多数的编程语言中，特别是 Java, Python 这样的语言中，万物皆对象，基本上每个变量都包含了变量自己和变量所指向的内存空间两个部分的逻辑含义。
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Code" %}
```java
public int[] copy(int[] nums) {
    int[] arr = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        arr[i] = nums[i]
    }
    return arr;
}

public void main() {
    int[] nums = new int[10];
    nums[0] = 1;
    int[] new_nums = copy(nums);
}
```
{% endtab %}

{% tab title="Notes" %}
在 copy 这个函数中，arr 是一个局部变量，他在 copy 函数执行结束之后就会被销毁。但是里面 new 出来的新数组并不会被销毁。这样在 main 函数里，new\_nums 里才会有被复制后的数组。所以可以发现一个特点：栈空间里存储的内容，会在函数执行结束的时候被撤回。简而言之可以这么区别栈空间和堆空间：

new 出来的就放在堆空间，其他都是栈空间。
{% endtab %}
{% endtabs %}

#### Stack Overflow

递归深度就是递归函数在内存中同时存在的最大次数。

```java
int factorial(int n) {
    if (n == 1) {
        return 1;
    }
    return factorial(n - 1) * n;
}
```

首先，函数本身也是在内存中占空间的，主要用于存储传递的参数，以及调用代码的返回地址。  
函数的调用，会在内存的栈空间中开辟新空间，来存放子函数。递归函数更是会不断占用栈空间，例如该阶乘函数，展开到最后n=1时，内存中会存在factorial\(100\), factorial\(99\), factorial\(98\) ... factorial\(1\)这些函数，它们从栈底向栈顶方向不断扩展。当递归过深时，栈空间会被耗尽，这时就无法开辟新的函数，会报出stack overflow这样的错误。所以，在考虑空间复杂度时，**递归函数的深度也是要考虑进去的**。

#### [尾递归](https://stackoverflow.com/questions/33923/what-is-tail-recursion)

若递归函数中，递归调用是整个函数体中最后的语句，且它的返回值不属于表达式的一部分时，这个递归调用就是尾递归。（上例factorial函数满足前者，但不满足后者，故不是尾递归函数）  
尾递归函数的特点是：在递归展开后该函数不再做任何操作，这意味着该函数可以不等子函数执行完，自己直接销毁，这样就不再占用内存。一个递归深度O\(n\)的尾递归函数，可以做到只占用O\(1\)的空间，这极大的优化了栈空间的利用。  
但要注意，这种内存优化是由编译器决定是否要采取的，不过大多数现代的编译器会利用这种特点自动生成优化的代码。在实际工作当中，尽量写尾递归函数，是很好的习惯。  
而在算法题当中，计算空间复杂度时，建议还是老老实实地算空间复杂度了，尾递归这种优化提一下也是可以，但别太在意。

```java
int factTailRecursion(int n, int a)
{   
    if (n < 0) {
        return 0;
    } else if (n == 0) {
        return 1;
    } else if (n == 1) {
        return a;
    } else {
        return facttail(n - 1, n * a);
    }
}
```

