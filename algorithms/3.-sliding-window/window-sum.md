---
description: >-
  Given an array of n integers, and a moving window(size k), move the window at
  each iteration from the start of the array, find the sum of the element inside
  the window at each moving.
---

# window sum

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public int[] winSum(int[] nums, int k) {
    if (k <= 0 || nums == null || nums.length == 0) {
        return new int[0];
    }
        
    int[] res = new int[nums.length - k + 1];
    int start = 0, cur = 0, sum = 0, index = 0;
    while (cur - start < k) {
        sum += nums[cur++];
    }
    res[index++] = sum;
        
    while (cur < nums.length) {
        sum -= nums[start++];
        sum += nums[cur++];
        res[index++] = sum;
    }
        
    return res;
}
```
{% endtab %}
{% endtabs %}

