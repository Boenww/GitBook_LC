# longest substring without repeating characters

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public int lengthOfLongestSubstring(String s) {
    if (s == null || s.length() == 0) {
        return 0;
    }

    int longest = 0, start = 0, cur = 0;

    //charToLastIndex mapping
    Map<Character, Integer> map = new HashMap<>();
    while (cur < s.length()) {
        char key = s.charAt(cur);
        if (map.containsKey(key) && map.get(key) >= start) {
            start = map.get(key) + 1;
        }

        map.put(s.charAt(cur), cur);
        longest = Math.max(longest, cur - start + 1);
        cur++;
    }

    return longest;
}
```
{% endtab %}
{% endtabs %}

