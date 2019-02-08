# 692/347. top k frequent words/elements

## 692.

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

{% tabs %}
{% tab title="Notes" %}
* O\(NlogK\): heap
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> count = new HashMap<>();
        for (String word: words) {
            if (!count.containsKey(word)) {
                count.put(word, 1);    
            } else {
                count.put(word, count.get(word) + 1);   
            }
        }
        
        Queue<String> pq = new PriorityQueue<>(k, new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                int diff = count.get(s1) - count.get(s2);
                
                if (diff == 0) {
                    return s2.compareTo(s1); //reverse because of minHeap
                    //poll elements with small count and high lexi order
                    //positive if s2 follows s1 and negative if s2 precedes s1
                }
                
                return diff;
            }
        });
        
        for (String word: count.keySet()) {
            pq.offer(word);
            if (pq.size() > k) {
                pq.poll();
            }
        }
        
        List<String> res = new ArrayList<>();
        while (!pq.isEmpty()) {
            res.add(0, pq.poll());
        }
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

## 347.

Given a non-empty array of integers, return the **k** most frequent elements.

```text
Example 1:
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:
Input: nums = [1], k = 1
Output: [1]
```

* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity **must be** better than O\(n log n\), where n is the array's size.

{% tabs %}
{% tab title="Notes" %}
* Same pq method as 692, but the order doesn't matter here if the frequencies are the same, so can use O\(N\) bucket method
* O\(N\): array\[freq\]
{% endtab %}

{% tab title="Solution" %}
```java
//O(n)
public List<Integer> topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    for (int num: nums) {
        count.put(num, count.getOrDefault(num, 0) + 1);
    }

    //if nums are all the same -> largest freq: nums.length
    List<Integer>[] buckets = new List[nums.length + 1];
    for (Integer key: count.keySet()) {
        int freq = count.get(key);
        if (buckets[freq] == null) {
            buckets[freq] = new ArrayList<>();
        }
        buckets[freq].add(key);
    }

    List<Integer> res = new ArrayList<>();
    for (int i = buckets.length - 1; i >= 0 && res.size() < k; i--) {
        if (buckets[i] != null) {
            res.addAll(buckets[i]);    
        }
    }

    return res;
}
```
{% endtab %}
{% endtabs %}

