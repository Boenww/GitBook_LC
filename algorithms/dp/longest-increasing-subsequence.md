# longest increasing subsequence

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```text
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

{% tabs %}
{% tab title="Notes" %}
* O\(n^2\): 

1. dp\[i\]: the longest length of the LIS by including the ith element
2. dp\[i\] = max\(dp\[j\]\) + 1, 0 &lt; j &lt; i 

* O\(nlogn\): maintain the LIS while scanning the array
{% endtab %}

{% tab title="Solution" %}
```java
class Solution { 
    //O(n^2)
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int[] dp = new int[nums.length];
        dp[0] = 1;
        int length = 1;
        for (int i = 1; i < nums.length; i++) {
            int max = 0;
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) { //condition to include the ith element 
                    max = Math.max(max, dp[j]);
                }
            }
            dp[i] = max + 1;
            length = Math.max(length, dp[i]);
        }
        
        return length;
    }
    
    //O(nlogn)
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int[] LIS = new int[nums.length];
        int length = 0;
        for (int num: nums) {
            int index = binarySearch(LIS, num, 0, length);
            
            LIS[index] = num;
            if (index == length) {
                length++;
            }
        }
        
        return length;
    }
    
    public int binarySearch(int[] LIS, int num, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (LIS[mid] >= num) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (LIS[start] >= num) {
            return start;
        } else {
            return end;
        }
    }
}
```
{% endtab %}
{% endtabs %}

