# lru cache

Design and implement a data structure for [Least Recently Used \(LRU\) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations: `get`and `put`.

`get(key)` - Get the value \(will always be positive\) of the key if the key exists in the cache, otherwise return -1.  
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Follow up:**  
Could you do both operations in **O\(1\)** time complexity?

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class LRUCache {
    class ListNode {
        public int key, val;
        public ListNode prev, next;
        public ListNode(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
    
    public int capacity, size;
    public ListNode dummy, tail;
    public Map<Integer, ListNode> map;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        size = 0;
        dummy = new ListNode(0, 0);
        tail = new ListNode(0, 0);
        dummy.next = tail;
        tail.prev = dummy;
        map = new HashMap<>();
    }
    
    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;   
        }
        
        ListNode node = map.get(key);
        moveToHead(node);
        
        return node.val;
    }
    
    public void put(int key, int value) {
        if (get(key) != -1) {
            map.get(key).val = value;
            return;
        }
        
        ListNode node = new ListNode(key, value);
        map.put(key, node);
        addNode(node);
        if (size > capacity) {
            removeNode(tail.prev);   
        }
    }
    
    public void moveToHead(ListNode node) {
        removeNode(node);
        addNode(node);
    }
    
    public void removeNode(ListNode node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
        map.remove(node.key);
        size--;
    }
    
    public void addNode(ListNode node) {
        node.next = dummy.next;
        dummy.next.prev = node;
        dummy.next = node;
        node.prev = dummy;
        map.put(node.key, node);
        size++;
    }
}
```
{% endtab %}
{% endtabs %}

