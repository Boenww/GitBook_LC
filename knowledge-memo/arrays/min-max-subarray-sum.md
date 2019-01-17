# min/max subarray sum

Given an array of integers, find a contiguous subarray which has the smallest/largest sum.

{% tabs %}
{% tab title="Notes" %}
* prefixSum
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public int minSubArray(List<Integer> nums) {
        int sum = 0, min = Integer.MAX_VALUE, maxSum = 0;
        for (Integer num: nums) {
            sum += num;
            min = Math.min(min, sum - maxSum);
            maxSum = Math.max(maxSum, sum);
        }
        
        return min;
    }
    
    public int maxSubArray(int[] nums) {
        int minSum = 0, sum = 0, max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(minSum, sum);
        }
        
        return max;
    }
}
```
{% endtab %}
{% endtabs %}

