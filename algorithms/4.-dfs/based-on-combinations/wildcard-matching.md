# wildcard matching

Given an input string \(`s`\) and a pattern \(`p`\), implement wildcard pattern matching with support for `'?'` and `'*'`.

```text
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
```

The matching should cover the **entire** input string \(not partial\).

* `s` could be empty and contains only lowercase letters `a-z`.
* `p` could be empty and contains only lowercase letters `a-z`, and characters like `?` or `*`.

```text
Example
Input:
s = "adceb"
p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```

{% tabs %}
{% tab title="Notes" %}
* dfs with memorization 
* multiple index method O\(mn\)
* dp
{% endtab %}

{% tab title="Solution" %}
```text

```
{% endtab %}
{% endtabs %}

