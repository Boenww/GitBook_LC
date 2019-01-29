# 295. find median from data stream

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O\(log \(m+n\)\).

You may assume **nums1** and **nums2** cannot be both empty.

```text
Example 1:
nums1 = [1, 3]
nums2 = [2]

The median is 2.0

Example 2:
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
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

