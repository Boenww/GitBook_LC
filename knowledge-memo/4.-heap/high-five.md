# high five

There are two properties in the node student `id` and `scores`, to ensure that each student will have at least 5 points, find the average of 5 highest scores for each person.

{% tabs %}
{% tab title="Notes" %}
* take care when to use min heap or max heap &lt;– poll\(\) 
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public Map<Integer, Double> highFive(Record[] results) {
        Map<Integer, Double> records = new HashMap<>();
        Map<Integer, Queue<Integer>> hF = new HashMap<>();
        
        for (Record record: results) {
            hF.putIfAbsent(record.id, new PriorityQueue<>(5));
            
            Queue<Integer> pq = hF.get(record.id);
            pq.offer(record.score);
            if (pq.size() > 5) {
                pq.poll();
            }
        }
        
        for (Map.Entry<Integer, Queue<Integer>> entry: hF.entrySet()) {
            records.put(entry.getKey(), getAverage(entry.getValue()));
        }
        
        return records;
    }
    
    public double getAverage(Queue<Integer> pq) {
        double sum = 0;
        for (Integer score: pq) {
            sum += score;
        }
        
        return sum / 5;
    }
}
```
{% endtab %}
{% endtabs %}

