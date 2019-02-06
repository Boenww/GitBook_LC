# 46/47. permutations I && II

## I

Given a collection of distinct integers, return all possible permutations.

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

## II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

{% tabs %}
{% tab title="Notes" %}
* sort to make duplicates close to each other and add another condition to skip invalid permutation\(e.g. 2'', 2'\)
* non-recursion by using next permutation.
{% endtab %}

{% tab title="Solution" %}
```java
//based on I
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        
        Arrays.sort(nums); //!!!
        dfs(nums, new boolean[nums.length], new ArrayList<>(), res);
        
        return res;
    }
    
    public void dfs(int[] nums, boolean[] visited, List<Integer> permutation, List<List<Integer>> res) {
        if (permutation.size() == nums.length) {
            res.add(new ArrayList<>(permutation));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            
            //!!!
            if (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1]) {
                continue;
            }
            
            permutation.add(nums[i]);
            visited[i] = true;
            dfs(nums, visited, permutation, res);
            visited[i] = false;
            permutation.remove(permutation.size() - 1);
        }
    }
};

//non-recursion
class Solution {
    private boolean nextPermutation(int[] nums) {
        int index = 0;
        for (int i = nums.length - 1; i > 0; i--) {
            if (nums[i] > nums[i - 1]) {
                index = i;
                for (int j = nums.length - 1; j >= index; j--) {
                    if (nums[j] > nums[index - 1]) {
                        swap(nums, j, index - 1);
                        break;
                    }
                }
                break;
            }
        }
        
        if (index == 0) {
            return false;
        }
        
        reverse(nums, index, nums.length - 1);
        return true;
    }
    
    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            swap(nums, start++, end--);
        }
    }
    
    public void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        
        Arrays.sort(nums);
        boolean hasNext = true;
        while (hasNext) {
            List<Integer> permutation = new ArrayList<>();
            for (int num: nums) {
                permutation.add(num);
            }
            
            res.add(permutation);
            hasNext = nextPermutation(nums);
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

