# 295. find median from data stream

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.For example,

`[2,3,4]`, the median is `3`

`[2,3]`, the median is `(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

* void addNum\(int num\) - Add a integer number from the data stream to the data structure.
* double findMedian\(\) - Return the median of all elements so far.

```text
Example:
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

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

