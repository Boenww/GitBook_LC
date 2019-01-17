# subarray sum/closest

## I

Given an integer array, find a subarray where the sum of numbers is **zero**. Your code should return the index of the first number and the index of the last number.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public List<Integer> subarraySum(int[] nums) {
        List<Integer> res = new ArrayList<>();
        Map<Integer, Integer> prefixSum = new HashMap<>();
        prefixSum.put(0, -1);
        
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (prefixSum.containsKey(sum)) {
                res.add(prefixSum.get(sum) + 1);
                res.add(i);
                break;
            }
            
            prefixSum.put(sum, i);
        }
        
        return res;
    }
}

// 1 0 -1
// 1 1 0

//prefixSum[-1] = 0
//prefixSum[i] = A[0] + ... + A[i]

//sum[i, j] = prefixSum[j] - prefixSum[i - 1] = A[i] + ... + A[j]

```
{% endtab %}
{% endtabs %}

## II

Given an integer array, find a subarray with sum closest to zero. Return the indexes of the first number and last number.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java

```
{% endtab %}
{% endtabs %}

