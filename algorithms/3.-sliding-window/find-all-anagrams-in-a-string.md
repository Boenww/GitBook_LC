# find all anagrams in a string

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> res = new ArrayList<>();
    int[] count = new int[26];
    for (int i = 0; i < p.length(); i++) {
        count[p.charAt(i) - 'a']++;
    }

    int left = 0, right = 0, diff = p.length();
    while (right < s.length()) {
        if (count[s.charAt(right) - 'a'] > 0) {
            diff--;
        }
        count[s.charAt(right) - 'a']--;
        right++;

        if (diff == 0) {
            res.add(left);
        }

        if (right - left == p.length()) {
            if (count[s.charAt(left) - 'a'] >= 0) { //appears in p, o.w. negative due to line 13
                diff++;
            }
            count[s.charAt(left) - 'a']++;
            left++;
        }
    }

    return res;
}
```
{% endtab %}
{% endtabs %}

