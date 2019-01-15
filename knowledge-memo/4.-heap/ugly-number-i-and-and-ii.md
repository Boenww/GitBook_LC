# ugly number I && II

## I

Write a program to check whether a given number is an ugly number.

Ugly numbers are **positive numbers** whose prime factors only include `2, 3, 5`.`1` is typically treated as an ugly number.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public boolean isUgly(int num) {
        if (num <= 0) {
            return false;
        }
        
        while (num != 1) {
            if (num % 2 == 0) {
                num /= 2;
            } else if (num % 3 == 0) {
                num /= 3;
            } else if (num % 5 == 0) {
                num /= 5;
            } else {
                return false;
            }
        }
        
        return true;
    }
}
```
{% endtab %}
{% endtabs %}

## II

Write a program to find the `n`-th ugly number.

Ugly numbers are **positive numbers** whose prime factors only include `2, 3, 5`. 

{% tabs %}
{% tab title="Notes" %}
* priority queue\(+ hashset to avoid duplicates\): O\(nlogn\)
* dp: O\(n\)
{% endtab %}

{% tab title="Solution" %}
```java
//pq
public int nthUglyNumber(int n) {      
    Queue<Integer> pq = new PriorityQueue<>();
    pq.add(1);
    for (int i = 1; i < n; i++) {
        int tmp = pq.poll();

        while (!pq.isEmpty() && tmp == pq.peek()) {
            pq.poll();
        }
        pq.add(tmp * 2);
        pq.add(tmp * 3);
        pq.add(tmp * 5);
    }

    return pq.poll();
}

//dp
public int nthUglyNumber(int n) { 
        int[] ugly = new int[n];
        ugly[0] = 1;
        int index2 = 0, index3 = 0, index5 = 0;
        for (int i = 1; i < n; i++) {
            ugly[i] = Math.min(Math.min(ugly[index2] * 2, ugly[index3] * 3), ugly[index5] * 5);
            
            if (ugly[i] == ugly[index2] * 2) {
                index2++;
            }
            
            if (ugly[i] == ugly[index3] * 3) {
                index3++;
            }
            
            if (ugly[i] == ugly[index5] * 5) {
                index5++;
            }
        }
    
        return ugly[n - 1];
}
```
{% endtab %}
{% endtabs %}



