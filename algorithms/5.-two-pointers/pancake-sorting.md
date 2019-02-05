# 969. pancake sorting

Use flip\(arr, i\) function to sort the array.

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
        for (int i = array.length - 1; i >= 0; i--) {
            int max = Integer.MIN_VALUE, index = 0;
            for (int j = 0; i <= i; j++) {
                if (array[j] > max) {
                    max = array[j];
                    index = j;
                }
            }
            flip(array, index);
            flip(array, i);
        }
    }
}
```
{% endtab %}
{% endtabs %}

