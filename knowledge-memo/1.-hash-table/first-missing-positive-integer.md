# first missing positive integer

Given an unsorted integer array `nums`, return the smallest missing positive integer.

You must implement an algorithm that runs in `O(n)` time. Challenge: use constant extra space.

<pre><code><strong>Example
</strong><strong>Input: nums = [3,4,-1,1]
</strong><strong>Output: 2
</strong><strong>Explanation: 1 is in the array but 2 is missing.
</strong></code></pre>

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
// use HashSet, not constant extra space
public int firstMissingPositive(int[] a) {
    // write your code here
    int res = 1;
    if (a == null) {
        return res;
    }

    Set<Integer> set = new HashSet<>();
    for (int i = 0; i < a.length; i++) {
        set.add(a[i]);
        while (set.contains(res)) {
            res++;
        }
    }

    return res;
}

// constant extra space
public int firstMissingPositive(int[] a) {
    // write your code here
    // target condition for the array
    // a[i] == i + 1
    // then we can find the first number that does not meet this condition
    int n = a.length;
    for (int i = 0; i < n; i++) {
        while (a[i] > 0 && a[i] <= n && a[i] != a[a[i] - 1]) {
            swap(a, i);
        }
    }

    for (int i = 0; i < n; i++) {
        if (a[i] != i + 1) {
            return i + 1;
        }
    }

    return n + 1;
}

public void swap(int[] a, int i) {
    int tmp = a[i];
    a[i] = a[tmp - 1];
    a[tmp - 1] = tmp;
}
```
{% endtab %}
{% endtabs %}

