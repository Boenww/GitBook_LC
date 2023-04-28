---
description: >-
  Given an array nums, write a function to move all 0's to the end of it while
  maintaining the relative order of the non-zero elements.
---

# move zeroes

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //insert index
    public void moveZeroes(int[] nums) {
        int index = 0;
        for (int num: nums) {
            if (num != 0) {
                nums[index++] = num;
            }
        }
        
        while (index < nums.length) {
            nums[index++] = 0;
        }
    }
    
    //two pointers: j points to the first zero and i moves forward to detect non zero
    public void moveZeroes(int[] nums) {
        int j = 0;
        for (int i = 0; i < nums.length; i++) { // i should start from 0 also to maintain the relative order!
            if (nums[i] != 0) {
                int tmp = nums[i];
                nums[i] = nums[j];
                nums[j] = tmp;
                j++;
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}
