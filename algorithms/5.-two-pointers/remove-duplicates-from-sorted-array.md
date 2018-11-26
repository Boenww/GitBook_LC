---
description: >-
  Given a sorted array nums, remove the duplicates in-place such that each
  element appear only once and return the new length. O(1) extra memory.
---

# remove duplicates from sorted array

{% tabs %}
{% tab title="Notes" %}
Follow up:
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /*
     * @param nums: An ineger array
     * @return: An integer
     */
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 1) {
            return nums.length;
        }
        
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[i] != nums[j]) {
                nums[++i] = nums[j];
            }
        }
        
        return i + 1;
    }
}


```
{% endtab %}
{% endtabs %}

