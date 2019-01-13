# kth smallest/largest element in an array

{% tabs %}
{% tab title="Notes" %}
* Kth largest: the index will be \(nums.length - k\) in the asc sorted array; kth smallest: the index will be k - 1
* how to partition properly
* O\(n\) average O\(n^2\) worst
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public int kthSmallest(int k, int[] nums) {
        if (nums == null || nums.length == 0 || k < 1 || k > nums.length) {
            return -1;
        }
        
        return partition(k - 1, nums, 0, nums.length - 1); // k - 1 !!!
        //nums.length - k for the kth largest problem 
    }
    
    public int partition(int k, int[] nums, int left, int right) {
        if (left >= right) {
            return nums[k];
        }
        
        int pivot = nums[left + (right - left) / 2];
        int i = left, j = right;
        while (i <= j) {
            while (i <= j && nums[i] < pivot) {
                i++;
            }
            
            while (i <= j && nums[j] > pivot) {
                j--;
            }
            
            if (i <= j) {
                swap(nums, i++, j--);
            }
            
        }
        
        if (k <= j) {
            return partition(k, nums, left, j);
        }
            
        return partition(k, nums, i, right);
    }
    
    public void swap(int[] nums, int left, int right) {
        int tmp = nums[left];
        nums[left] = nums[right];
        nums[right] = tmp;
    }
}

//space: O(1)
public int kthLargest(int[] nums, int k) {
    //corner case
    if (nums == null) {
        return -1;
    }
    
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int index = left;
        for (int i = left; i < right; i++) { //pivot = nums[right]
            if (nums[i] > nums[right]) {
                swap(nums, i, index++);
            }
        }
        
        swap(nums, index, right); //the element with index is the (index + 1)th largest element
        if (index + 1 == k) {
            return nums[index];
        } else if (index + 1 < k) { //kth would be in the range index + 1...right
            left = index + 1;
        } else {
            right = index - 1;
        }
    }
    
    return -1;
}
```
{% endtab %}
{% endtabs %}

