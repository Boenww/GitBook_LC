# remove duplicate numbers in array

Given an array of integers, remove the duplicate numbers in it.

You should:

1. Do it in place in the array.
2. Move the unique numbers to the front of the array.
3. Return the total number of the unique numbers.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public int deduplication(int[] nums) {
    if (nums == null || nums.length <= 1) {
        return 0;
    }
    Arrays.sort(nums);
    int i = 0, j = 1;
        
    while (i < j && j < nums.length) {
        while (j < nums.length && nums[i] == nums[j]) {
            j++;
        }
            
        if (j < nums.length) {
            swap(nums, ++i, j++);
        }
    }
        
    return i + 1;
}
    
public void swap(int[] nums, int left, int right) {
    int tmp = nums[left];
    nums[left] = nums[right];
    nums[right] = tmp;
}
```
{% endtab %}
{% endtabs %}

