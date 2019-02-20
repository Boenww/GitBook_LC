# 75. sort colors

Given an array with _n_ objects colored _red_, _white_ or _blue_, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue. Only one pass using constant space.

Here, we will use the integers `0`, `1`, and `2` to represent the color red, white, and blue respectively.

{% tabs %}
{% tab title="Notes" %}
* Use three pointers
* Take care when to move the "cur" pointer
* nums\[cur\] == 0 -&gt; the number from left cannot be 2 -&gt; cur++
* nums\[cur\] == 2 -&gt; the number from right can be any number -&gt; not change cur
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public void sortColors(int[] nums) {
        if (nums == null) {
            return;
        }
        
        int left = 0, cur = 0, right = nums.length - 1;
        while (cur <= right) {
            if (nums[cur] == 0) {
                swap(nums, left++, cur++);
            } else if (nums[cur] == 1) {
                cur++;
            } else if (nums[cur] == 2) {
                swap(nums, right--, cur);
            }
        }
    }
    
    public void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```
{% endtab %}
{% endtabs %}

