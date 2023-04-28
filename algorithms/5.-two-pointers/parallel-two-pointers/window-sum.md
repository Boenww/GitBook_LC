---
description: lintcode
---

# 604. window sum

Given an array of n integers, and a moving window(size k), move the window at each iteration from the start of the array, find the sum of the element inside the window at each moving.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public int[] winSum(int[] nums, int k) {
        if (nums == null || k <= 0 || k > nums.length) { // clarify what to return when k > nums.length
            return new int[0];
        }
        
        int[] res = new int[nums.length - k + 1];
        int start = 0, cur = 0, sum = 0, index = 0;
        while (cur - start < k) {
            sum += nums[cur++];
        }
        res[index++] = sum;
        
        while (index < res.length) {
            sum = sum + nums[cur++] - nums[start++];
            res[index++] = sum;
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}
