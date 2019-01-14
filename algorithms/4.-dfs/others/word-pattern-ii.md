# word pattern II

Given a `pattern` and a string `str`, find if `str` follows the same pattern.

Here **follow** means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** substring in `str`.

```text
Input: pattern = "abab", str = "redblueredblue"
Output: true

Input: pattern = "aabb", str = "xyzabcxzyabc"
Output: false
```

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public boolean wordPatternMatch(String pattern, String str) {
        return dfs(pattern, str, new HashMap<>(), new HashSet<>());
    }
    
    public boolean dfs(String pattern, String str, Map<Character, String> map, Set<String> set) {
        if (pattern.length() == 0 && str.length() == 0) {
            return true;
        } else if (pattern.length() == 0 || str.length() == 0) {
            return false;
        }
        
        char curP = pattern.charAt(0);
        if (map.containsKey(curP)) {
            String prefix = map.get(curP);
            if (!str.startsWith(prefix)) {
                return false;
            }
            
            return dfs(pattern.substring(1), str.substring(prefix.length()), map, set);
        }
        
        for (int i = 1; i <= str.length(); i++) {
            String prefix = str.substring(0, i);
            if (set.contains(prefix)) {
                continue;
            }
            
            set.add(prefix);
            map.put(curP, prefix);
            if (dfs(pattern.substring(1), str.substring(prefix.length()), map, set)) {
                return true;
            }
            
            map.remove(curP);
            set.remove(prefix);
        }
        
        return false;
    }
}
```
{% endtab %}
{% endtabs %}

