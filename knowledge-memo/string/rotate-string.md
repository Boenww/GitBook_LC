# 8. rotate string

Given a string and an offset, rotate string by offset. \(rotate from left to right\)

{% tabs %}
{% tab title="Notes" %}
* reverse three times with constant extra space
* same method to solve "39. recover rotated sorted array"
{% endtab %}

{% tab title="Solution" %}
```java
public void rotateString(char[] str, int offset) {
    if (str == null || str.length <= 1 || offset == 0) {
        return;
    }
    
    int newOffset = offset % str.length;
    reverse(str, 0, str.length - 1 - newOffset);
    reverse(str, str.length - newOffset, str.length - 1);
    reverse(str, 0, str.length - 1);
}

public void reverse(char[] chars, int left, int right) {
    while (left < right) {
        char tmp = chars[left];
        chars[left] = chars[right];
        chars[right] = tmp;
        left++;
        right--;
    }
}
```
{% endtab %}
{% endtabs %}



