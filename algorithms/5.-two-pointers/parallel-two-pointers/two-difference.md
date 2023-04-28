---
description: lintcode
---

# 610. two sum - difference equals to target

Given an array of integers, find two numbers that their `difference` equals to a target value.\
where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are NOT zero-based. It's guaranteed there is only one available solution.

{% tabs %}
{% tab title="Notes" %}
* sorted or unsorted&#x20;
* return index or the array value
* only one available solution, i.e. two different values&#x20;
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
            while (j < nums.length && numsCopy[j] - numsCopy[i] < target) {
                j++;
            }
            
            if (numsCopy[j] - numsCopy[i] == target) {
                break;
            }
            i++; // i == j??? e.g. [0,1,2,2] 0
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
    
    // old: above and return index
    // new: return values
    public int[] twoSum7(int[] nums, int target) {
    		int[] res = new int[]{-1, -1};
    
    		if (nums == null || nums.length < 2) {
    			return res;
    		}
    
    		int i = 0, j = 1, difference = 0;
    		while (i < nums.length && j < nums.length) {
    			difference = nums[j] - nums[i];
    			if (difference == target && i != j) {
    				res[0] = nums[i];
    				res[1] = nums[j];
            break;
    			} else if (difference < target) {
    				j++;
    			} else {
    				i++;
    			}
    		}
    
        Arrays.sort(res);
    		return res;
	}
}
```
{% endtab %}
{% endtabs %}
