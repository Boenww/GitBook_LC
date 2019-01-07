# palindrome partitioning

Given a string _s_, partition _s_ such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of _s_.  


{% tabs %}
{% tab title="Notes" %}
* Combination based\(decide whether cut or not at each index\)
* more general
* optimize: get palindrome information ahead
{% endtab %}

{% tab title="Solution" %}
```java
//combination based
public class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        
        partitionHelper(s, 0, 1, new ArrayList<>(), res);
        return res;
    }
    
    public void partitionHelper(String s, int lastIndex, int curIndex, List<String> sub, List<List<String>> res) {
        if (curIndex == s.length()) {
            if (isPalindrome(s.substring(lastIndex, curIndex))) {
                sub.add(s.substring(lastIndex, curIndex));
                res.add(new ArrayList<>(sub));
                sub.remove(sub.size() - 1);
            }
            return;
        }
        
        if (isPalindrome(s.substring(lastIndex, curIndex))) {
            sub.add(s.substring(lastIndex, curIndex));    
            partitionHelper(s, curIndex, curIndex + 1, sub, res);
            sub.remove(sub.size() - 1);
            
        } 
        partitionHelper(s, lastIndex, curIndex + 1, sub, res);
    }
    
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
    }
}

//more general 
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        
        helper(s, 0, new ArrayList<>(), res);
        return res;
    }
    
    public void helper(String s, int startIndex, List<String> sub, List<List<String>> res) {
        if (startIndex == s.length()) {
            res.add(new ArrayList<>(sub));
            return;
        }
        
        for (int i = startIndex; i < s.length(); i++) {
            if (isPalindrome(s.substring(startIndex, i + 1))) {
                sub.add(s.substring(startIndex, i + 1));
                helper(s, i + 1, sub, res);
                sub.remove(sub.size() - 1);
            }
        }
    }
    
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        
        return true;
    }
}

//optimize 
class Solution {
    public boolean[][] isPalindrome;
    
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        isPalindrome = getIsPalindrome(s);
        
        helper(s, 0, new ArrayList<>(), res);
        return res;
    }
    
    public void helper(String s, int startIndex, List<String> sub, List<List<String>> res) {
        if (startIndex == s.length()) {
            res.add(new ArrayList<>(sub));
            return;
        }
        
        for (int i = startIndex; i < s.length(); i++) {
            if (isPalindrome[startIndex][i]) {
                sub.add(s.substring(startIndex, i + 1));
                helper(s, i + 1, sub, res);
                sub.remove(sub.size() - 1);
            }
        }
    }
    
    public boolean[][] getIsPalindrome(String s) {
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= i; j++) {
                dp[j][i] = s.charAt(i) == s.charAt(j) && (i - j <= 2 || dp[j + 1][i - 1]);
            }
        }
        return dp;
    }
}
```
{% endtab %}
{% endtabs %}

