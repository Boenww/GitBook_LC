# 5. longest palindromic substring

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

```text
Example 1:
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Example 2:
Input: "cbbd"
Output: "bb"
```

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
     //dp: Time/Space O(n^2)
     //dp[i][j]: if the substring from i to j is palindrome
     public String longestPalindrome(String s) {
         if (s == null || s.length() == 0) {
             return "";
         }
         
         int n = s.length(), len = 1, start = 0;
         boolean[][] dp = new boolean[n][n];
         for (int i = 0; i < n - 1; i++) {
             dp[i][i] = true;
         }
         
         for (int i = 0; i < n - 1; i++) {
             dp[i][i + 1] = s.charAt(i) == s.charAt(i + 1);
             if (dp[i][i + 1]) {
                 len = 2;
                 start = i;
             }
         }
         
         for (int i = n - 1; i >= 0; i--) {
             for (int j = i + 2; j < n; j++) {
                dp[i][j] = dp[i + 1][j - 1] && s.charAt(i) == s.charAt(j);
                if (dp[i][j] == true && j - i + 1 > len) {
                    start = i;
                    len = j - i + 1;
                }
             }
         }
         
         return s.substring(start, start + len);
     }
     
     //expand around center(2n - 1): O(n^2), Space O(1)
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) {
            return s;
        }
        
        int start = 0, len = 0, longest = 0;
        for (int i = 0; i < s.length(); i++) {
            // i
            //aba
            len = findLongestPalindrome(s, i, i);
            if (len > longest) {
                longest = len;
                start = i - len / 2;
            }
            // i
            //abba
            len = findLongestPalindrome(s, i, i + 1);
            if (len > longest) {
                longest = len;
                start = i - len / 2 + 1;
            }        
        }
        
        return s.substring(start, start + longest);
    }
    
    public int findLongestPalindrome(String s, int left, int right) {
        int len = 0;
        while (left >= 0 && right < s.length()) {
            if (s.charAt(left) != s.charAt(right)) {
                break;
            }
            len += left == right ? 1 : 2;
            left--;
            right++;
        }
        
        return len;
    }
}
```
{% endtab %}
{% endtabs %}

