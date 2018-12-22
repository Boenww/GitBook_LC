---
description: 'Given an array of strings, group anagrams together.'
---

# group anagrams

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();
    for (String s: strs) {
        char[] chars = s.toCharArray();
        Arrays.sort(chars);
        String key = String.valueOf(chars);
        map.putIfAbsent(key, new ArrayList<>());
        map.get(key).add(s);
    }

    return new ArrayList<>(map.values());
}
```
{% endtab %}
{% endtabs %}

