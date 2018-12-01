# single number

## I

{% tabs %}
{% tab title="Notes" %}
Given a **non-empty** array of integers, every element appears _twice_ except for one. Find that single one.
{% endtab %}

{% tab title="Solution" %}
```java
public int singleNumber(int[] A) {
    int res = A[0];
    for (int i = 1; i < A.length; i++) {
        res ^= A[i];
    }

    return res;
}
```
{% endtab %}
{% endtabs %}

## II

{% tabs %}
{% tab title="Notes" %}
Given a **non-empty** array of integers, every element appears _three_ times except for one, which appears exactly once. Find that single one.

* p \* n + 1 elements
{% endtab %}

{% tab title="Solution" %}
```java
//extract every bit of the single number by modulo
public int singleNumber(int[] nums) {
    int ans = 0;
    
    //ith bit
    for(int i = 0; i < 32; i++) {
        int sum = 0;
        for(int j = 0; j < nums.length; j++) {
            if(((nums[j] >> i) & 1) == 1) { //() !!!
                sum++;
            }
        }
        sum %= 3; // % p
        if(sum == 1) {
            ans |= sum << i;
        }
    }
    return ans;
}
```
{% endtab %}
{% endtabs %}

## III

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}

{% endtab %}
{% endtabs %}

## IV

{% tabs %}
{% tab title="Notes" %}
Give an array, all the numbers appear twice except one number which appears once and _all the numbers which appear twice are next to each other_. Find the number which appears once.

* O\(n\) method is the same, but can achieve O\(logn\) by binary search.
{% endtab %}

{% tab title="Solution" %}
```java
public int getSingleNumber(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == nums[mid + 1]) {
            if ((right - mid + 1) % 2 == 1) {
                left = mid + 2;
            } else {
                right = mid - 1;
            }
        } else if (nums[mid] == nums[mid - 1]) {
            if ((mid - left + 1) % 2 == 1) {
                right = mid - 2;
            } else {
                left = mid + 1;
            }
        } else {
            return nums[mid];
        }
    }

    return nums[left];
}
```
{% endtab %}
{% endtabs %}

