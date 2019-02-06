# 31. next permutation

Rearrange numbers into the lexicographically next greater permutation of numbers.If such arrangement is not possible, it be the lowest possible order\(ie, sorted in ascending order\).

{% tabs %}
{% tab title="Notes" %}
1. 从右往左遍历数组nums，直到找到一个位置i，满足nums\[i\] &gt; nums\[i - 1\]或者i为0。
2.  i不为0时，用j再次从右到左遍历nums，寻找第一个nums\[j\] &gt; nums\[i - 1\]。而后交换nums\[j\]和nums\[i - 1\]。**满足要求的j一定存在！且交换后nums\[i\]及右侧数组仍为降序数组**。
3. 将nums\[i\]及右侧的数组翻转，使其升序。
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers
     */
    public int[] nextPermutation(int[] nums) {
        if (nums == null || nums.length <= 1) {
            return nums;
        }
        
        int index = 0;
        for (int i = nums.length - 1; i > 0; i--) {
            if (nums[i] > nums[i - 1]) {
                index = i;
                for (int j = nums.length - 1; j >= index; j--) {
                    if (nums[j] > nums[i - 1]) {
                        swap(nums, j, i - 1);
                        break;
                    }
                }
                break;
            }
        }
        
        reverse(nums, index, nums.length - 1);
        return nums;
    }
    
    public void swap(int[] nums, int left, int right) {
        int tmp = nums[left];
        nums[left] = nums[right];
        nums[right] = tmp;
    }
    
    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            swap(nums, start++, end--);
        }
    }
}
```
{% endtab %}
{% endtabs %}

