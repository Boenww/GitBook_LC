---
description: >-
  Given two strings, write a method to decide if one is a permutation of the
  other.
---

# permutations

{% tabs %}
{% tab title="Solution" %}
```java
public boolean Permutation(String A, String B) {
    if (A == null || B == null || A.length() != B.length()) {
        return false;
    }
    
    int res = 0;
    for (int i = 0; i < A.length(); i++) {
        res ^= A.charAt(i) ^ B.charAt(i);
    }
    
    return res == 0;
}
```
{% endtab %}
{% endtabs %}

