# split string

Give a string, you can choose to split the string after one character or two adjacent characters, and make the string to be composed of only one character or two characters. Output all possible results.

#### Example

Given the string `"123"`  
return `[["1","2","3"],["12","3"],["1","23"]]`

{% tabs %}
{% tab title="Notes" %}
* combination based
* more general 
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public List<List<String>> splitString(String s) {
        List<List<String>> res = new ArrayList<>();
        
        helper(s, 0, new ArrayList<>(), res);
        return res;
    }
    
    public void helper(String s, int startIndex, List<String> sub, List<List<String>> res) {
        if (startIndex == s.length()) {
            res.add(new ArrayList<>(sub));
            return;
        }
        
        //combination based
        sub.add(s.substring(startIndex, startIndex + 1));
        helper(s, startIndex + 1, sub, res);
        sub.remove(sub.size() - 1);
        if (startIndex + 2 <= s.length()) {
            sub.add(s.substring(startIndex, startIndex + 2));
            helper(s, startIndex + 2, sub, res);
            sub.remove(sub.size() - 1);    
        }
        
        //more general
        for (int i = startIndex; i < s.length(); i++) {
            if (i > startIndex + 1) {
                break;
            }
            
            sub.add(s.substring(startIndex, i + 1));
            helper(s, i + 1, sub, res);
            sub.remove(sub.size() - 1);
        }
    }
}
```
{% endtab %}
{% endtabs %}

