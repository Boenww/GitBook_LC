# alien dictionary

{% tabs %}
{% tab title="Notes" %}
* Modularity:

1. construct the graph: create all nodes and create all edges
2. get the in-degree map
3. topo sorting

* Not hard but long; difference between lintcode and leetcode, which is if it is necessary to return a lexi ordered result
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {        
    public String alienOrder(String[] words) {
        if (words.length == 0) {
            return "";
        }
        
        Map<Character, Set<Character>> preToChar = constructGraph(words);
        Map<Character, Integer> IndegreeMap = getIndegreeMap(preToChar);
        
        Queue<Character> queue = new PriorityQueue<>();
        for (Character c: IndegreeMap.keySet()) {
            if (IndegreeMap.get(c) == 0) {
                queue.offer(c);
            }
        }
        
        StringBuilder sb = new StringBuilder();
        while (!queue.isEmpty()) {
            Character pre = queue.poll();
            sb.append(pre);
            for (Character next: preToChar.get(pre)) {
                if (IndegreeMap.get(next) - 1 == 0) {
                    queue.offer(next);
                }
                IndegreeMap.put(next, IndegreeMap.get(next) - 1);
            }
        }
        
        return sb.length() == preToChar.size()? sb.toString() : "";
    }

    public Map<Character, Set<Character>> constructGraph(String[] words) {
        Map<Character, Set<Character>> graph = new HashMap<>();
        //create nodes
        for (int i = 0; i < words.length; i++) {
            for (int j = 0; j < words[i].length(); j++) {
                if (!graph.containsKey(words[i].charAt(j))) {
                    graph.put(words[i].charAt(j), new HashSet<>());    
                }
            }
        }
        
        //create edges
        for (int i = 0; i < words.length - 1; i++) {
            int index = 0;
            while (index < words[i].length() && index < words[i + 1].length()) {
                if (words[i].charAt(index) != words[i + 1].charAt(index)) {
                    graph.get(words[i].charAt(index)).add(words[i + 1].charAt(index));
                    break;
                }
                index++;
            }
        }
        
        return graph;
    }

    public Map<Character, Integer> getIndegreeMap(Map<Character, Set<Character>> preToChar) {
    	Map<Character, Integer> IndegreeMap = new HashMap<>();
        
        for (Character pre: preToChar.keySet()) {
            IndegreeMap.put(pre, 0);
        }

        for (Character pre: preToChar.keySet()) {
            for (Character c: preToChar.get(pre)) {
                IndegreeMap.put(c, IndegreeMap.get(c) + 1);
            }
        }

        return IndegreeMap;
    }
}

```
{% endtab %}
{% endtabs %}

