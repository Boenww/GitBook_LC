---
description: used for solving greatest common divisor
---

# Euclidean algorithm

{% tabs %}
{% tab title="Notes" %}
The time complexity can be obtained by making an analogy to Fibonacci and mathematical induction. 
{% endtab %}

{% tab title="Solution" %}
```java
//O(log(min(a, b)))
public static int gcd(int a, int b) {
    if (b != 0) {
        return gcd(b, a % b);
    }
    
    return a;
}
```
{% endtab %}
{% endtabs %}



