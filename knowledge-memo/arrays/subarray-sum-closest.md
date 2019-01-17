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
public class Solution {
    public int[] subarraySumClosest(int[] nums) {
        if (nums.length == 1) {
            return new int[]{0, 0};
        }
        
        int[] res = new int[2];
        Map<Integer, Integer> prefixSumToIndex = new HashMap<>();
        prefixSumToIndex.put(0, -1);//sum[i, j] = prefixSum[j] - prefixSum[i - 1]
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (prefixSumToIndex.containsKey(sum)) {
                res[0] = prefixSumToIndex.get(sum) + 1;
                res[1] = i;
                return res;
            }
            
            prefixSumToIndex.put(sum, i);
        }
        
        List<Integer> prefixSum = new ArrayList<>(prefixSumToIndex.keySet());
        Collections.sort(prefixSum);
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < prefixSum.size() - 1; i++) {
            if (prefixSum.get(i + 1) - prefixSum.get(i) < min) {
                min = prefixSum.get(i + 1) - prefixSum.get(i);
                res[0] = prefixSumToIndex.get(prefixSum.get(i + 1));
                res[1] = prefixSumToIndex.get(prefixSum.get(i));
                
            }
        }
        
        Arrays.sort(res);
        res[0]++;
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

