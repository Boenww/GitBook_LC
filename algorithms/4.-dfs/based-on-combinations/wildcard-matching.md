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
* dfs with memorization //时间复杂度是 O\(mn\)，m和n是两个字符串的长度。因为对于我们要记忆的东西（也就是搜索函数里的参数组合）一共就 O\(nm\) 种可能性。每种参数组合的可能性往下递归的时候，是 O\(1\) 的处理时间。
* multiple index method O\(mn\)
* dp
{% endtab %}

{% tab title="Solution" %}
```java
//dfs with memorization 
public class Solution {     
    public boolean[][] visited;
    public boolean[][] memo;
    
    public boolean isMatch(String s, String p) {
        visited = new boolean[s.length()][p.length()];
        memo = new boolean[s.length()][p.length()];
        
        return helper(s, p, 0, 0);
    }
    
    public boolean helper(String s, String p, int sIndex, int pIndex) {
        if (sIndex == s.length()) {
            return allStars(p, pIndex);
        }
        
        if (pIndex == p.length()) {
            return sIndex == s.length();
        }
        
        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }
        
        char curS = s.charAt(sIndex), curP = p.charAt(pIndex);
        boolean match = false;
        
        if (curP == '*') {
            match = helper(s, p, sIndex, pIndex + 1) || helper(s, p, sIndex + 1, pIndex);
        } else {
            match = (curS == curP || curP == '?') && helper(s, p, sIndex + 1, pIndex + 1);
        }
        
        visited[sIndex][pIndex] = true;
        memo[sIndex][pIndex] = match;
        
        return match;
    }
    
    public boolean allStars(String p, int pIndex) {
        for (int i = pIndex; i < p.length(); i++) {
            if (p.charAt(i) != '*') {
                return false;
            }
        }
        
        return true;
    }
}

//multiple index method
class Solution {
    public boolean isMatch(String s, String p) {
        int sIndex = 0, pIndex = 0, starIndex = -1, match = 0; 
        while (sIndex < s.length()) {
            if (pIndex < p.length() && (s.charAt(sIndex) == p.charAt(pIndex) || p.charAt(pIndex) == '?')) {
                pIndex++;
                sIndex++;
            } else if (pIndex < p.length() && p.charAt(pIndex) == '*') {
                starIndex = pIndex;
                match = sIndex;
                pIndex++;
            } else if (starIndex != -1) {
                pIndex = starIndex + 1; //backtrack 
                sIndex = ++match;
            } else {
                return false;
            }
        }
    
        for (int i = pIndex; i < p.length(); i++) {
            if (p.charAt(i) != '*') {
                return false;
            }
        }
        
        return true;
    }
}

//dp
```
{% endtab %}
{% endtabs %}

