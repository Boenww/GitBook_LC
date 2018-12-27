# two difference

Given an array of integers, find two numbers that their `difference` equals to a target value.  
where index1 must be less than index2. Please note that your returned answers \(both index1 and index2\) are NOT zero-based. It's guaranteed there is only one available solution.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param nums: an array of Integer
     * @param target: an integer
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
     
    //O(nlogn), O(n) without hashmap
    public int[] twoSum7(int[] nums, int target) {
        int[] numsCopy = Arrays.copyOf(nums, nums.length);
        Arrays.sort(numsCopy);
        target = Math.abs(target);
        int i = 0, j = 1;
        while (i < j && j < nums.length) {
            while (i == j || (j < nums.length && numsCopy[j] - numsCopy[i] < target)) {
                j++;
            }
            
            if (numsCopy[j] - numsCopy[i] == target) {
                break;
            }
            i++;
        }
        
        int[] res = new int[]{-1, -1};
        boolean iFound = false, jFound = false;
        for (int x = 0; x < nums.length; x++) {
            if (nums[x] == numsCopy[i] && !iFound) {
                res[0] = x + 1;
                iFound = true;
                continue;
            }
            
            if (nums[x] == numsCopy[j] && !jFound) {
                res[1] = x + 1;
                jFound = true;
            }
        }
        
        Arrays.sort(res);
        return res;
    }
    
    //O(n), O(n) with hashmap
    public int[] twoSum7(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i] + target)) {
                return new int[]{map.get(nums[i] + target), i + 1};
            }
            
            if (map.containsKey(nums[i] - target)) {
                return new int[]{map.get(nums[i] - target), i + 1};
            } 
            
            map.put(nums[i], i + 1);
        }
        
        return new int[]{-1, -1};
    }
}
```
{% endtab %}
{% endtabs %}

