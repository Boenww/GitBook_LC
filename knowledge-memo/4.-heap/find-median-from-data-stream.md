# find median from data stream

{% tabs %}
{% tab title="Notes" %}
* use a maxheap to store the smaller half\(n/n + 1\) and a minheap to store the larger half\(n\): O\(logn\) insert and O\(1\) findMedian
* bst method: it is difficult to implement balanced bst? O\(n\) insert for unbalanced
{% endtab %}

{% tab title="Solution" %}
```java
class MedianFinder {
    public Queue<Integer> small, large;

    public MedianFinder() {
        small = new PriorityQueue<>(Comparator.reverseOrder());
        large = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        small.offer(num);
        large.offer(small.poll());
        
        if (small.size() < large.size()) {
            small.offer(large.poll());
        }
        
    }
    
    public double findMedian() {
        return small.size() > large.size() ? small.peek() : (small.peek() + large.peek()) / 2.0;
    }
}
```
{% endtab %}
{% endtabs %}

