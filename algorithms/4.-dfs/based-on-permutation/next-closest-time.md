# next closest time

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

