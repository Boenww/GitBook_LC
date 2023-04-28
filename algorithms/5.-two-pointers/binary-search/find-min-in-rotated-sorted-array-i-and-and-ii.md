# find min in rotated sorted array I && II

## I

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element. You may assume no duplicate exists in the array.

{% tabs %}
{% tab title="Notes" %}
O(n): traverse when nums\[i] < nums\[i - 1]

O(logn): bs
{% endtab %}

{% tab title="Solution" %}
```java
//O(logn)
public int findMin(int[] nums) {
    int left = 0, right = nums.length - 1;
    int target = nums[right];
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) { // nums[right] is ok, too
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return nums[left];
}
```
{% endtab %}
{% endtabs %}

## II

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element. The array may contain duplicates.

{% tabs %}
{% tab title="Notes" %}
* worst case: O(n), e.g. 1 0 1 1 1 1 ... 1
{% endtab %}

{% tab title="Solution" %}
```java
public int findMin(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == nums[right]) { //no idea, e.g. [3, 1, 3] but we can eliminate nums[right]
            right--;
        } else if (nums[mid] < nums[right]) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return nums[left];
}
```
{% endtab %}
{% endtabs %}
