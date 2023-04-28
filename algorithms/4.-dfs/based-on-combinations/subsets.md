# 78/90. subsets I && II

## I

Given a set of **distinct** integers, _nums_, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

{% tabs %}
{% tab title="Notes" %}
* recursive
* 组合类搜索（一层一层地决策每个数要不要）
* more general
* iterative
* bit manipulation&#x20;
* bfs
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //组合类
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        
        helper(nums, 0, res, new ArrayList<>());
        return res;
    }
    
    public void helper(int[] nums, int index, List<List<Integer>> res, List<Integer> subset) {
        if (index == nums.length) {
            res.add(new ArrayList<>(subset));
            return;
        }
        
        subset.add(nums[index]);
        helper(nums, index + 1, res, subset);
        subset.remove(subset.size() - 1);
        helper(nums, index + 1, res, subset);
    }
    
    //more general version
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        
        dfs(nums, 0, res, new ArrayList<>());
        return res;
    }
    
    public void dfs(int[] nums, int startIndex, List<List<Integer>> res, List<Integer> subset) {
        res.add(new ArrayList<>(subset));
        
        for (int i = startIndex; i < nums.length; i++) {
            subset.add(nums[i]);
            dfs(nums, i + 1, res, subset);
            subset.remove(subset.size() - 1);
        }
    }
    
    //bit manipulation
     public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        
        //[1,2,3]
        //[000] -> []
        //[001] -> [3]
        //...
        for (int i = 0; i < (1 << nums.length); i++) {
            List<Integer> subset = new ArrayList<>();
            for (int j = 0; j < nums.length; j++) {
                if ((i & (1 << j)) != 0) {
                    subset.add(nums[j]);
                }
            }
            res.add(subset);
        }
        
        return res;
    }
    
    //iterative
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        
        Arrays.sort(nums);
        Queue<List<Integer>> queue = new LinkedList<>();
        queue.offer(new ArrayList<>());
        while (!queue.isEmpty()) {
            List<Integer> subset = queue.poll();
            res.add(subset);
            
            for (int i = 0; i < nums.length; i++) {
                if (subset.size() == 0 || subset.get(subset.size() - 1) < nums[i]) {
                    List<Integer> newSubset = new ArrayList<>(subset);
                    newSubset.add(nums[i]);
                    queue.offer(newSubset);
                }
            }
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

## II

Given a collection of integers that might contain duplicates, _**nums**_, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.\


{% tabs %}
{% tab title="Notes" %}
* If nums\[i - 1] is not added to the subset and nums\[i] == nums\[i - 1]\(next recursion), nums\[i] should also not be added into the subset.
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        
        Arrays.sort(nums);
        dfs(nums, 0, new ArrayList<Integer>(), res);
        return res;
    }
    
    public void dfs(int[] nums, int startIndex, List<Integer> subset, List<List<Integer>> res) {
        res.add(new ArrayList<>(subset));
        
        for (int i = startIndex; i < nums.length; i++) {
            if (i > startIndex && nums[i] == nums[i - 1]) {
                continue;
            }
            subset.add(nums[i]);
            dfs(nums, i + 1, subset, res); //i - 1 + 1 == i == startIndex if i - 1 is added
            subset.remove(subset.size() - 1);
        }
    }
}
```
{% endtab %}
{% endtabs %}
