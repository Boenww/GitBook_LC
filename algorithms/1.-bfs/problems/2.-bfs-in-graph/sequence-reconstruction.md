---
description: >-
  Check whether the original sequence org can be uniquely reconstructed from the
  sequences in seqs.
---

# sequence reconstruction

{% tabs %}
{% tab title="Notes" %}
The graph can be built with a list of neighbors, which would not make any effect on BFS. Otherwise or to use a set, the indegree map should be initialized according to the built graph since there could be repeated seqs.
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param org: a permutation of the integers from 1 to n
     * @param seqs: a list of sequences
     * @return: true if it can be reconstructed only one or false
     */
    public boolean sequenceReconstruction(int[] org, int[][] seqs) {
        Map<Integer, Integer> indegree = new HashMap<>();
        Map<Integer, List<Integer>> graph = new HashMap<>(); 
        
        for (int i = 0; i < seqs.length; i++) {
            for (int j = 0; j < seqs[i].length; j++) {
                indegree.putIfAbsent(seqs[i][j], 0);
                graph.putIfAbsent(seqs[i][j], new ArrayList<>());
                
                if (j > 0) {
                    indegree.put(seqs[i][j], indegree.get(seqs[i][j]) + 1);
                    graph.get(seqs[i][j - 1]).add(seqs[i][j]);
                }
            }
        }
        
        if (indegree.size() != org.length) {
            return false;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 1; i <= org.length; i++) {
            if (indegree.get(i) == 0) {
                queue.offer(i);
            }
        }
        
        int index = 0;
        while (queue.size() == 1) {
            Integer num = queue.poll();
            if (org[index++] != num) {
                return false;
            }
            
            for (Integer nb: graph.get(num)) {
                if (indegree.get(nb) == 1) {
                    queue.offer(nb);
                }
                indegree.put(nb, indegree.get(nb) - 1);
            }
        }
        
        return index == org.length;
    }
}
```
{% endtab %}
{% endtabs %}

