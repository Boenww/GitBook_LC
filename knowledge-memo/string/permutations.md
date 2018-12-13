---
description: >-
  Given two strings, write a method to decide if one is a permutation of the
  other.
---

# permutations

{% tabs %}
{% tab title="Notes" %}
* Avoid XOR bit operation, "aa" and "bb"
{% endtab %}

{% tab title="Solution" %}
```java
public boolean Permutation(String s, String t) {
    int[] count = new int[256]; //extended ASCII
    for (int i = 0; i < s.length(); i++) {
        count[s.charAt(i)]++;
    }

    for (int j = 0; j < t.length(); j++) {
        count[t.charAt(j)]--;
    }

    for (int k: count) {
        if (k != 0) {
            return false;
        }
    }

    return true;
}
```
{% endtab %}
{% endtabs %}

