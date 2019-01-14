# regular expression match

Given an input string \(`s`\) and a pattern \(`p`\), implement regular expression matching with support for `'.'` and `'*'`.

```text
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the **entire** input string \(not partial\).

* `s` could be empty and contains only lowercase letters `a-z`.
* `p` could be empty and contains only lowercase letters `a-z`, and characters like `.` or `*`.

```text
Example
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".

Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

{% tabs %}
{% tab title="Notes" %}
* Same kind with the wildcard matching problem 
* dfs with memo 
* dp
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public boolean[][] visited, memo;
    
    public boolean isMatch(String s, String p) {
        visited = new boolean[s.length()][p.length()];
        memo = new boolean[s.length()][p.length()];
        
        return helper(s, p, 0, 0);
    }
    
    private boolean helper(String s, String p, int sIndex, int pIndex) {
        if (pIndex == p.length()) {
            return sIndex == s.length();
        }
        
        if (sIndex == s.length()) {
            return isEmpty(p, pIndex);
        }
        
        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }
        
        char curS = s.charAt(sIndex), curP = p.charAt(pIndex);
        boolean match = false;
        
        if (curP == '*') {
            match = helper(s, p, sIndex, pIndex + 1) ||
                (pIndex > 0 && matchChar(curS, p.charAt(pIndex - 1)) && helper(s, p, sIndex + 1, pIndex));
        } else {
            match = (matchChar(curS, curP) && helper(s, p, sIndex + 1, pIndex + 1)) ||
                (pIndex < p.length() - 1 && p.charAt(pIndex + 1) == '*' && helper(s, p, sIndex, pIndex + 2)); 
        }
        
        visited[sIndex][pIndex] = true;
        memo[sIndex][pIndex] = match;
        
        return match;
    }
    
    private boolean matchChar(char s, char p) {
        return s == p || p == '.';
    }
    
    private boolean matchEmpty(String p, int pIndex) {
        for (int i = pIndex; i < p.length() - 1; i++) {
            if (p.charAt(i) != '*' && p.charAt(i + 1) != '*') {
                return false;
            }
        }
        
        return p.charAt(p.length() - 1) == '*';
    }
}
```
{% endtab %}
{% endtabs %}

