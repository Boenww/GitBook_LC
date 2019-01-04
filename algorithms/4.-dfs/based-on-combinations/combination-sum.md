# combination sum I && II

## I

Given a **set** of candidate numbers \(`candidates`\) **\(without duplicates\)** and a target number \(`target`\), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

The **same** repeated number may be chosen from `candidates` unlimited number of times.

**Note:**

* All numbers \(including `target`\) will be positive integers.
* The solution set must not contain duplicate combinations.

{% tabs %}
{% tab title="Notes" %}
* recursion with the same index\(chosen unlimited number of times\)
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //Time Tree Structure O((target/min)^n) exponential
    //Space O(target/min)
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        if (candidates == null) {
            return res;
        }
        
        backtrack(candidates, 0, res, new ArrayList<>(), target);
        
        return res;
    }
    
    public void backtrack(int[] candidates, int index, List<List<Integer>> res, List<Integer> comb, int target) {
        if (target == 0) {
            res.add(new ArrayList<>(comb));
            return;
        } else if (target > 0) {
            for (int i = index; i < candidates.length; i++) {
                if (target >= candidates[i]) {
                    comb.add(candidates[i]);
                    backtrack(candidates, i, res, comb, target - candidates[i]);
                    comb.remove(comb.size() - 1);
                }
            }
        }   
    }
}
```
{% endtab %}
{% endtabs %}

## II

Given a collection of candidate numbers \(`candidates`\) and a target number \(`target`\), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:**

* All numbers \(including `target`\) will be positive integers.
* The solution set must not contain duplicate combinations.

{% tabs %}
{% tab title="Notes" %}
* consider how to remove duplicate
* recursion with the next index\(chosen only once\)
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        
        if (candidates == null) {
            return res;
        }
        
        Arrays.sort(candidates);
        dfs(candidates, 0, target, new ArrayList<Integer>(), res);
        
        return res;
    }
    
    public void dfs(int[] candidates, int index, int target, List<Integer> comb, List<List<Integer>> res) {
        if (target == 0) {
            res.add(new ArrayList<>(comb));
            return;
        }
        
        if (target < 0 || index == candidates.length) {
            return;
        }
        
        for (int i = index; i < candidates.length; i++) {
            if (i > index && candidates[i] == candidates[i - 1]) {
                continue;
            }
            
            comb.add(candidates[i]);
            dfs(candidates, i + 1, target - candidates[i], comb, res);
            comb.remove(comb.size() - 1);
        }
    }
}
```
{% endtab %}
{% endtabs %}

