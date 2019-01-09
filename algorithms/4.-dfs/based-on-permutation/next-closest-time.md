# next closest time

Given a time represented in the format "HH:MM", form the next closest time by reusing the current digits. There is no limit on how many times a digit can be reused.

You may assume the given input string is always valid. For example, "01:34", "12:09" are all valid. "1:34", "12:9" are all invalid.

```text
Input: "19:34"
Output: "19:39"
Explanation: The next closest time choosing from digits 1, 9, 3, 4, is 19:39, which occurs 5 minutes later.  It is not 19:33, because this occurs 23 hours and 59 minutes later.

Input: "23:59"
Output: "22:22"
Explanation: The next closest time choosing from digits 2, 3, 5, 9, is 22:22. It may be assumed that the returned time is next day's time since it is smaller than the input time numerically.
```

{% tabs %}
{% tab title="Notes" %}
1. sort the digits of the input time
2. get all valid time as a list in order by dfs with sorted digits
3. find the position of the input time in the obtained list
4. the time at the next position is the ans
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public String nextClosestTime(String time) {
        int[] digits = new int[4];
        digits[0] = time.charAt(0) - '0';
        digits[1] = time.charAt(1) - '0';
        digits[2] = time.charAt(3) - '0';
        digits[3] = time.charAt(4) - '0';
        
        Arrays.sort(digits);
        
        //all valid time in order
        List<String> allTime = new ArrayList<>();
        
        dfs(digits, "", allTime);
        
        int index = 0;
        for (int i = 0; i < allTime.size(); i++) {
            if (allTime.get(i).equals(time)) {
                index = i;
            }
        }
        
        //next in circular order
        index = (index == allTime.size() - 1) ? 0 : index + 1;
        return allTime.get(index);
    }
    
    private void dfs(int[] digits, String s, List<String> list) {
        if (s.length() == 5) {
            list.add(s);
            return;
        }
        
        if (s.length() == 2) {
            s += ":";
        }
        
        //eliminate invalid time
        for (int i = 0; i < 4; i++) {
            if (s.length() == 0 && digits[i] > 2) {
                return;
            }
            
            if (s.length() == 1 && s.charAt(0) == '2' && digits[i] > 3) {
               return;
            }
            
            if (s.length() == 3 && digits[i] > 5) {
                return;
            }

            dfs(digits, s + digits[i], list);
        }
    }
}
```
{% endtab %}
{% endtabs %}

