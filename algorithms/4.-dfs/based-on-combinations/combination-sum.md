---
description: >-
  Given a set of candidate numbers (candidates) and a target number (target),
  find all unique combinations in candidates where the candidate numbers sums to
  target.
---

# combination sum

{% tabs %}
{% tab title="Notes" %}
1. The same repeated number may be chosen from candidates unlimited number of times.
2. Each number in candidates may only be used once in the combination.

* Possible duplicates in the candidate numbers?
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //Time Tree Structure O((target/min)^n) exponential
    //Space O(target/min)
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        if (candidates == null || candidates.length == 0) {
            return res;
        }
        
        Arrays.sort(candidates);
        backtrack(candidates, 0, res, new ArrayList<>(), target);
        
        return res;
    }
    
    public void backtrack(int[] candidates, int index, List<List<Integer>> res, List<Integer> comb, int target) {
        if (target == 0) {
            res.add(new ArrayList<>(comb));
            return;
        } else if (target > 0) {
            for (int i = index; i < candidates.length; i++) {
                //skip possible duplicates in the sorted input
                if (i != index && candidates[i] == candidates[i - 1]) {
                    continue;
                }
                
                if (target >= candidates[i]) {
                    comb.add(candidates[i]);
                    backtrack(candidates, i, res, comb, target - candidates[i]);//1. i; 2. i + 1
                    comb.remove(comb.size() - 1);
                }
            }
        }   
    }
}
```
{% endtab %}
{% endtabs %}

