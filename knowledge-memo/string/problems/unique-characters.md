---
description: Implement an algorithm to determine if a string has all unique characters.
---

# unique characters

{% tabs %}
{% tab title="Solution" %}
```java
public class Solution {
    /*
     * @param str: A string
     * @return: a boolean
     */
     //O(nlogn)
    public boolean isUnique(String str) {
        char[] array = str.toCharArray();
        Arrays.sort(array);
        
        for (int i = 0; i < array.length - 1; i++) {
            if (array[i] == array[i + 1]) {
                return false;
            }
        }
        
        return true;
    }
    
    //O(n)
    public boolean isUnique(String str) {
        boolean[] hasChar = new boolean[256];
        for (char c: str.toCharArray()) {
            if (hasChar[c]) {
                return false;
            }
            hasChar[c] = true;
        }
        
        return true;
    }
    
    //str: a-z
    //O(n)
    //without additional datastructures
    public boolean isUnique(String str) {
        int checker = 0;
        
        for (int i = 0; i < str.length(); i++) {
            int val = str.charAt(i) - 'a';
            //bit has been set
            if ((checker & (1 << val)) > 0) {
                return false;
            }
            
            //set bit
            checker |= 1 << val;
        }
        
        return true;   
    }
}
```
{% endtab %}
{% endtabs %}

