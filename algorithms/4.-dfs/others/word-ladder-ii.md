# word ladder II

Given two words \(_beginWord_ and _endWord_\), and a dictionary's word list, find all shortest transformation sequence\(s\) from _beginWord_ to _endWord_, such that:

1. Only one letter can be changed at a time
2. Each transformed word must exist in the word list. Note that _beginWord_ is _not_ a transformed word.

**Note:**

* Return an empty list if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume _beginWord_ and _endWord_ are non-empty and are not the same.

{% tabs %}
{% tab title="Notes" %}
* take care whether beginWord and endWord exist in the word list
* endWord -&gt; beginWord: bfs, beginWord -&gt; endWord: dfs
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        List<List<String>> ladders = new ArrayList<>();
        Map<String, List<String>> graph = new HashMap<>();
        Map<String, Integer> distanceMap = new HashMap<>();
        Set<String> wordSet = new HashSet<>(wordList);
        if (!wordSet.contains(endWord)) {
            return ladders;
        }
        
        wordSet.add(beginWord);
        
        bfs(graph, distanceMap, endWord, wordSet);
        dfs(ladders, new ArrayList<>(), graph, distanceMap, beginWord, endWord);
        
        return ladders;
    }
    
    public void bfs(Map<String, List<String>> graph, Map<String, Integer> distanceMap, String endWord, Set<String> wordSet) {
        Queue<String> queue = new LinkedList<>();
        queue.offer(endWord);
        distanceMap.put(endWord, 0);
        
        for (String word: wordSet) {
            graph.put(word, new ArrayList<>());
        }
        
        while (!queue.isEmpty()) {
            String cur = queue.poll();
            
            for (String nb: getNeighbors(cur, wordSet)) {
                graph.get(nb).add(cur);
                
                if (!distanceMap.containsKey(nb)) {
                    distanceMap.put(nb, distanceMap.get(cur) + 1);
                    queue.offer(nb);
                }
            }
        }
    }
    
    public void dfs(List<List<String>> ladders, List<String> ladder, Map<String, List<String>> graph, Map<String, Integer> distanceMap, String cur, String endWord) {
        if (cur.equals(endWord)) {
            ladder.add(cur);
            ladders.add(new ArrayList<>(ladder));
            ladder.remove(cur);
            return;
        }
        
        for (String nb: graph.get(cur)) {
            if (distanceMap.containsKey(nb) && distanceMap.get(nb) == distanceMap.get(cur) - 1) {
                ladder.add(cur);
                dfs(ladders, ladder, graph, distanceMap, nb, endWord);
                ladder.remove(ladder.size() - 1);
            }
        }
}
    
    public List<String> getNeighbors(String str, Set<String> wordSet) {
        List<String> nbs = new ArrayList<>();
        
        for (int i = 0; i < str.length(); i++) {
            for (char c = 'a'; c <= 'z'; c++) {
                if (str.charAt(i) != c) {
                    String nb = str.substring(0, i) + c + str.substring(i + 1);
                    
                    if (wordSet.contains(nb)) {
                        nbs.add(nb);
                    }
                }
            }
        }
        
        return nbs;
    }
}
```
{% endtab %}
{% endtabs %}

