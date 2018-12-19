# letter combinations of a phone number

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public final String[] KEYBOARD = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    
    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return res;
        }
        
        dfs(digits, new StringBuilder(), res);
        return res;
    }
    
    public void dfs(String digits, StringBuilder sb, List<String> res) {
        if (sb.length() == digits.length()) {
            res.add(sb.toString());
            return;
        }
        
        String digit = KEYBOARD[digits.charAt(sb.length()) - '0'];
        for (int i = 0; i < digit.length(); i++) {
            sb.append(digit.charAt(i));
            dfs(digits, sb, res);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```
{% endtab %}
{% endtabs %}

