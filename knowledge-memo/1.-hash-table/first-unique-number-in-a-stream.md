# first unique number in a stream

We need to implement a data structure named `DataStream`. There are `two` methods required to be implemented:

1. `void add(number)` // add a new number
2. `int firstUnique()` // return first unique number

```text
Example:
add(1)
add(2)
firstUnique() => 1
add(1)
firstUnique() => 2
```

{% tabs %}
{% tab title="Notes" %}
1. LinkedList + hashmap
2. LinkedHashSet
{% endtab %}

{% tab title="Solution" %}
```java
//1.
public class DataStream {
    class ListNode {
        public int val;
        public ListNode next;
        public ListNode(int val) {
            this.val = val;
            next = null;
        }
    }
    
    public ListNode dummy, tail;
    public Map<Integer, ListNode> uniqueToPrev;
    public Set<Integer> set;
    
    public DataStream(){
        dummy = new ListNode(0);
        tail = dummy;
        uniqueToPrev = new HashMap<>();
        set = new HashSet<>();
    }
    /**
     * @param num: next number in stream
     * @return: nothing
     */
    public void add(int num) {
        if (uniqueToPrev.containsKey(num)) {
            remove(num);
        } else {
            uniqueToPrev.put(num, tail);
            
            ListNode node = new ListNode(num);
            tail.next = node;
            tail = tail.next;
        }
        set.add(num);
    }
    
    public void remove(int num) {
        ListNode prev = uniqueToPrev.get(num);
        prev.next = prev.next.next;
        uniqueToPrev.remove(num);
        
        if (prev.next == null) {
            tail = prev;
        } else {
            uniqueToPrev.put(prev.next.val, prev);
        }
    }

    /**
     * @return: the first unique number in stream
     */
    public int firstUnique() {
        if (dummy.next == null) {
            return -1;
        }
        
        return dummy.next.val;
    }
}

//2.
public class DataStream {
    public Set<Integer> unique;
    public Set<Integer> set;
    
    public DataStream(){
        unique = new LinkedHashSet<>();
        set = new HashSet<>();
    }
    /**
     * @param num: next number in stream
     * @return: nothing
     */
    public void add(int num) {
        if (set.contains(num)) {
            unique.remove(num);
        } else {
            set.add(num);
            unique.add(num);
        }
    }

    /**
     * @return: the first unique number in stream
     */
    public int firstUnique() {
        return unique.iterator().next();
    }
}
```
{% endtab %}
{% endtabs %}

