# top k frequent words

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

{% tabs %}
{% tab title="Notes" %}
* O\(NlogK\): heap
* O\(N\): array\[freq\]
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

