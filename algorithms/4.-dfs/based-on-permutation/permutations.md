---
description: 'Given a collection of distinct integers, return all possible permutations.'
---

# permutations

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive O(n!)
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        
        dfs(res, new ArrayList<>(), new boolean[nums.length], nums);
        return res;
    }
    
    public void dfs(List<List<Integer>> res, List<Integer> permutation, boolean[] visited, int[] nums) { 
        if (permutation.size() == nums.length) {
            res.add(new ArrayList<>(permutation));//!!! important (ref)
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            
            visited[i] = true;
            permutation.add(nums[i]);
            dfs(res, permutation, visited, nums);
            visited[i] = false;
            permutation.remove(permutation.size() - 1);
        }
    }
    
    //non-recursive
    //use next permutation
}
```
{% endtab %}
{% endtabs %}

