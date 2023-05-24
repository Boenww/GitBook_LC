# sort colors I && II

### I

Given an array with 0, 1, 2 and sort. Input: \[1, 0, 1, 2]. Expected output: \[0, 1, 1, 2]. Iterate only once.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public void sortColors(int[] nums) {
    if (nums == null) {
        return;
    }

    int i = 0, left = 0, right = nums.length - 1;
    while (i <= right) {
        if (nums[i] == 0) {
            swap(nums, left++, i++);
        } else if (nums[i] == 2) {
            swap(nums, right--, i);
        } else {
            i++;
        }
    }
}
```
{% endtab %}
{% endtabs %}

### II

Given an array of _n_ objects with _k_ different colors (numbered from 1 to k), sort them so that objects of the same color are adjacent, with the colors in the order 1, 2, ... k. A rather straight forward solution is a two-pass algorithm using counting sort. That will cost O(k) extra memory. Can you do it without using extra memory?

{% tabs %}
{% tab title="Notes" %}
* Given k, O(nlogk) can be achieved with partitioning.
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        if (colors == null) {
            return;
        }
        
        sortHelper(colors, 0, colors.length - 1, 1, k);
    }
    
    public void sortHelper(int[] colors, int start, int end, int from, int to) {
        if (start >= end || from >= to) {
            return;
        }
        
        int pivot = from + (to - from) / 2, i = start;
        for (int j = start; j <= end; j++) {
            if (colors[j] <= pivot) {
                swap(colors, i++, j);
            }
        }
        
        sortHelper(colors, start, i - 1, from, pivot);
        sortHelper(colors, i, end, pivot + 1, to);
    }
    
    public void swap(int[] colors, int i, int j) {
        int tmp = colors[i];
        colors[i] = colors[j];
        colors[j] = tmp;
    }
}
```
{% endtab %}
{% endtabs %}
