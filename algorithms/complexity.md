# \* Complexity

## Time Complexity

时间复杂度定性地描述了一个算法的运行时间，与问题规模n正相关，使用O\(poly\(n\)\)表示。

* **只包含多项式的最高次项。** 这是因为在复杂度计算中，最高次项对运行时间有决定性的作用，次高次项可以忽略不计。例如f\(n\) = n^2 + n， 此时n这一项对于多项式的值的影响相对于n^2可以忽略不计。
* **不包含多项式最高次项的系数。** 对于最高次项，我们忽略它的系数，在算法中，我们称之为常数。

| 复杂度 | 可能对应的算法 | 备注 |
| :--- | :--- | :--- |
| O\(1\) | 位运算 | 常数级复杂度，一般面试中不会有 |
| O\(logn\) | 二分法，倍增法，快速幂算法，辗转相除法 |  |
| O\(n\) | 枚举法，双指针算法，单调栈算法，KMP算法，Rabin Karp，Manacher's Algorithm | 线性时间复杂度 |
| O\(nlogn\) | 快速排序，归并排序，堆排序 |  |
| O\(n^2\) | 枚举法，动态规划，Dijkstra |  |
| O\(n^3\) | 枚举法，动态规划，Floyd |  |
| O\(2^n\) | 与组合有关的搜索问题 |  |
| O\(n!\) | 与排列有关的搜索问题 |  |

### Examples

{% tabs %}
{% tab title="Code" %}
```java
int Fibo(int n) {
    if (n == 0 || n == 1) return 1;
    return Fibo(n - 1) + Fibo(n - 2);
}
```
{% endtab %}

{% tab title="Ans" %}
时间复杂度为 O\(2^\(n/2\)\) ~ O\(2^n\)

时间复杂度上界：Fibo\(n\) = Fibo\(n-1\) + Fibo\(n-2\) &lt; 2 \* Fibo\(n-1\)  
递归版 Fibonacci 的时间复杂度 &lt; T\(n\) = 2 \* T\(n-1\) + O\(1\) = O\(2^n\)

时间复杂度下界：Fibo\(n\) = Fibo\(n-1\) + Fibo\(n-2\) &gt; 2 \* Fibo\(n-2\)  
递归版 Fibonacci 的时间复杂度 &gt; T\(n\) = 2 \* T\(n-2\) + O\(1\) = O\(2^\(n/2\)\)
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Code" %}
```java
int[] F = new int[50];
F[0] = F[1] = 1;
int Fibo(int n) {
    if (F[n] != 0) {
        return F[n];
    }
    F[n] = Fibo(n-1) + Fibo(n-2);
    
    return F[n];
}
```
{% endtab %}

{% tab title="Ans" %}
O\(n\)
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Code" %}
```java
int j = 0;
for (int i = 0; i < n; i++) {
    while (j < n && nums[j] - nums[i] < window) {
        j++;
    }
}
```
{% endtab %}

{% tab title="Ans" %}
O\(n\)  
这个程序是典型的双指针算法，\[i, j\) 是一个滑动窗口的两端，滑动窗口之内的数，两两之差 &lt; window。  
  
数循环次数是一个偷懒的时间复杂度计算方法，却不是最准确的时间复杂度计算方法。时间复杂度的定义，是程序总共执行的语句数目的数量级。在这个代码中，执行次数最多的是 j++ 这个循环主体。而这个循环体不会被执行 O\(n^2\)次，因为 j 在每次 i 循环的时候，不会被重置到 i 或者 0 的位置开始重新计算。j一直是自顾自的单向递增，那么一旦某一次 while 循环使得 j++ 执行了 n 次以后，while 循环就再也进不去了。因此总共的执行次数是 O\(n + n\) = O\(n\)而不是 O\(n \* n\)。
{% endtab %}
{% endtabs %}

## Space Complexity

