---
description: >-
  Given a sorted array nums, remove the duplicates in-place such that each
  element appear only once and return the new length. O(1) extra memory.
---

# remove duplicates from sorted array

{% tabs %}
{% tab title="Notes" %}
Follow up: such that duplicates appear at most _twice_
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

//follow up
public int removeDuplicates(int[] nums) {
    if (nums == null || nums.length == 0) {
        return 0;
    }

    int i = 0, count = 1;
    for (int j = 1; j < nums.length; j++) {
        if (nums[i] != nums[j]) {
            nums[++i] = nums[j];
            count = 1;
        } else if (count < 2) {
            count++;
            nums[++i] = nums[j];
        }
    }

    return i + 1;
}

```
{% endtab %}
{% endtabs %}
