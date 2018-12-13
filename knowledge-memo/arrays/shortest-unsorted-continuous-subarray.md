---
description: >-
  Given an integer array, you need to find one continuous subarray that if you
  only sort this subarray in ascending order, then the whole array will be
  sorted in ascending order, too.
---

# shortest unsorted continuous subarray

{% tabs %}
{% tab title="Notes" %}
* intuitive: sort and compare
* two for loops to optimize to O\(n\)
{% endtab %}

{% tab title="Solution" %}
```java
//sort and compare
public int findUnsortedSubarray(int[] nums) {
    if (nums == null || nums.length <= 1) {
        return 0;
    }

    int[] copy = nums.clone();
    Arrays.sort(copy);
    int start = nums.length - 1, end = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != copy[i]) {
            start = Math.min(start, i);
            end = Math.max(end, i);
        }
    }

    return start > end ? 0 : end - start + 1;
}

//two for loops O(n)
public int findUnsortedSubarray(int[] nums) {
    if (nums == null || nums.length <= 1) {
        return 0;
    }
    
    //find the most right element that is smaller than the max from its left
    int right = -1, max = nums[0];
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] < max) {
            right = i;
        }
        max = Math.max(max, nums[i]);
    }
    
    //alread sorted in asc
    if (right == -1) {
        return 0;
    }
    
    //find the most left element that is larger than the min from its right 
    int left = -1, min = nums[nums.length - 1];
    for (int j = nums.length - 2; j >= 0; j--) {
        if (nums[j] > min) {
            left = j;
        }
        min = Math.min(min, nums[j]);
    }
    
    return right - left + 1;
}
```
{% endtab %}
{% endtabs %}

