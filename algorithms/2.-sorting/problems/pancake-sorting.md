---
description: 'Use flip(arr, i) function to sort the array.'
---

# pancake sorting

{% tabs %}
{% tab title="Notes" %}
1. do a linear scan of the array from right to left and maintain the current end index
2. for each end index, find the index of the maximum element from array\[0\] to array\[end\]
3. flip\(array, index\)
4. flip\(array, end--\)
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param array: an integer array
     * @return: nothing
     */
    public void pancakeSort(int[] array) {
        if (array == null) {
            return;
        }
        
        int end = array.length - 1;
        while (end > 0) {
            int max = Integer.MIN_VALUE, index = 0;
            for (int i = 0; i <= end; i++) {
                if (array[i] > max) {
                    max = array[i];
                    index = i;
                }
            }
            flip(array, index);
            flip(array, end--);
        }
    }
}
```
{% endtab %}
{% endtabs %}

