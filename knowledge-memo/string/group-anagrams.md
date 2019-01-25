# 49. group anagrams

Given an array of strings, group anagrams together.

```text
Example:
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

* All inputs will be in lowercase.
* The order of the output does not matter.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //O(nk)
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> freqToAnagrams = new HashMap<>();
        
        for (String str: strs) {
            String key = getFreq(str);
            freqToAnagrams.putIfAbsent(key, new ArrayList<>());
            freqToAnagrams.get(key).add(str);
        }
        
        return new ArrayList<>(freqToAnagrams.values());
    }
    
    private String getFreq(String str) {
        int[] count = new int[26];
        
        for (int i = 0; i < str.length(); i++) {
            count[str.charAt(i) - 'a']++;
        }
        
        String freq = "";
        for (int i = 0; i < count.length; i++) {
            freq += String.valueOf(count[i]);
        }
        
        return freq;
    }
    
    //O(nklogk)
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        for (String str: strs) {
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String key = String.valueOf(chars);
            map.putIfAbsent(key, new ArrayList<>());
            map.get(key).add(s);
        }

        return new ArrayList<>(map.values());
    }
}
```
{% endtab %}
{% endtabs %}

