# 125/680. valid palindrome I && II

## I

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

```text
Example 1:
Input: "A man, a plan, a canal: Panama"
Output: true

Example 2:
Input: "race a car"
Output: false
```

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }
        
        int left = 0, right = s.length() - 1;
        while (left < right) {
            while (left < right && !isAlphanumeric(s.charAt(left))) {
                left++;
            }
            
            while (left < right && !isAlphanumeric(s.charAt(right))) {
                right--;
            }
            
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            } 
            
            left++;
            right--;
        }
        
        return true;
    }
    
    public boolean isAlphanumeric(char c) {
        return Character.isLetter(c) || Character.isDigit(c);
    }
}
```
{% endtab %}
{% endtabs %}

## II

Given a non-empty string `s`, you may delete at most one character. Judge whether you can make it a palindrome.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param s: a string
     * @return: nothing
     */
    public boolean validPalindrome(String s) {
        int start = 0, end = s.length() - 1;
        while (start < end) {
            if (s.charAt(start) == s.charAt(end)) {
                start++;
                end--;
            } else {
                return isPalindrome(s, start + 1, end) || isPalindrome(s, start, end - 1);
            }
        }
        
        return true;
    }
    
    public boolean isPalindrome(String s, int left, int right) {
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
```
{% endtab %}
{% endtabs %}

