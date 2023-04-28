# 438. find all anagrams in a string

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

```
Example 1:
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

{% tabs %}
{% tab title="Notes" %}
* Sliding window O(n)
* hash: count array&#x20;
* brute force O(nk), k is the length of p
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
