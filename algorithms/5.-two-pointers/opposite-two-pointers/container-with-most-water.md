# container with most water

Find two lines, which together with x-axis forms a container, such that the container contains the most water.

![](../../../.gitbook/assets/image.png)

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public int maxArea(int[] height) {
    if (height == null) {
        return 0;
    }

    int max = 0, left = 0, right = height.length - 1;
    while (left < right) {
        max = Math.max(max, (right - left) * Math.min(height[left], height[right]));
        if (height[left] < height[right]) {
            left++;
        } else { // height[left] == height[right] doesn't matter, caz if right doesn't change, the area will be smaller regardless of height[left++]
            right--;
        }
    }

    return max;
}
```
{% endtab %}
{% endtabs %}
