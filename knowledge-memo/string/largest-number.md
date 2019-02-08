# 179. largest number

Given a list of non negative integers, arrange them such that they form the largest number.

```text
Input: [3,30,34,5,9]
Output: "9534330"
```

{% tabs %}
{% tab title="Notes" %}
```java
new Comparator<>() {
    @Override
    public int compare(lhs, rhs) {
         //return 1 if rhs should be before lhs
         //return -1 if lhs should be before rhs
         //return 0 otherwise
    }
}
```
{% endtab %}

{% tab title="Solution" %}
```java
//O(knlogn), k average length of the strings
class Solution {
    public String largestNumber(int[] nums) {
       if (nums == null || nums.length == 0) {
           return "";
       }
        
        String[] strNums = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            strNums[i] = String.valueOf(nums[i]);
        }
        
        Arrays.sort(strNums, new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return (s2 + s1).compareTo(s1 + s2);
            }
        });
        
        //edge case
        if (strNums[0].equals("0")) {
            return "0";
        }
        
        String res = "";
        for (String s: strNums) {
            res += s;
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

