---
description: >-
  The degree of an non-empty array is defined as the maximum frequency of any
  one of its elements. Find the smallest possible length of a (contiguous)
  subarray of it, that has the same degree.
---

# degree of an array

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public int findShortestSubArray(int[] nums) {
    int degree = 0, shortest = Integer.MAX_VALUE;
    Map<Integer, List<Integer>> numToIndex = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        numToIndex.putIfAbsent(nums[i], new ArrayList<>());
        numToIndex.get(nums[i]).add(i);
        degree = Math.max(degree, numToIndex.get(nums[i]).size());
    }

    for (List<Integer> indices : numToIndex.values()) {
        if (indices.size() == degree) {
            shortest = Math.min(shortest, indices.get(indices.size() - 1) - indices.get(0) + 1);
        }
    }

    return shortest;
}

//one pass with two hashmaps
public int findShortestSubArray(int[] nums) {
    Map<Integer, Integer> numToDegree = new HashMap<>();
    Map<Integer, Integer> numToFirstIndex = new HashMap<>();
    int res = 0, degree = 0;
    for (int i = 0; i < nums.length; i++) {
        numToFirstIndex.putIfAbsent(nums[i], i);
        if (!numToDegree.containsKey(nums[i])) {
            numToDegree.put(nums[i], 1);
        } else {
            numToDegree.put(nums[i], numToDegree.get(nums[i]) + 1);
        }

        if (numToDegree.get(nums[i]) > degree) {
            degree = numToDegree.get(nums[i]);
            res = i - numToFirstIndex.get(nums[i]) + 1;
        } else if (numToDegree.get(nums[i]) == degree) {
            res = Math.min(res, i - numToFirstIndex.get(nums[i]) + 1);
        }
    }

    return res;
}
```
{% endtab %}
{% endtabs %}

