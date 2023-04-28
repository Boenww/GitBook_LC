---
description: leetcode
---

# 706. design hashmap

Design a HashMap without using any built-in hash table libraries.

To be specific, your design should include these functions:

* `put(key, value)` : Insert a (key, value) pair into the HashMap. If the value already exists in the HashMap, update the value.
* `get(key)`: Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key.
* `remove(key)` : Remove the mapping for the value key if this map contains the mapping for the key.

{% tabs %}
{% tab title="Notes" %}
* // to notice&#x20;
{% endtab %}

{% tab title="Solution" %}
```java
class MyHashMap {
    class ListNode {
        public int key, value;
        public ListNode next;
        public ListNode(int key, int value) {
            this.key = key;
            this.value = value;
            next = null;
        }
    }
    
    public ListNode[] buckets;
    public MyHashMap() {
        buckets = new ListNode[100];
    }
    
    public void put(int key, int value) {
        ListNode head = buckets[hash(key)];
        if (head == null) {
            buckets[hash(key)] = new ListNode(key, value); //
            return;
        } 
        
        if (head.key == key) { //
            head.value = value;
            return;
        }
        
        while (head.next != null && head.next.key != key) {
            head = head.next;
        }
        
        if (head.next == null) { //
            head.next = new ListNode(key, value);
        } else {
            head.next.value = value;
        }
    }
    
    public int get(int key) {
        ListNode head = buckets[hash(key)];
     
        while (head != null) {
            if (head.key == key) {
                return head.value;
            }
            
            head = head.next;
        }
        
        return -1;
    }
    
    public void remove(int key) {
        ListNode head = buckets[hash(key)];
        if (head == null) { //
            return;
        }
        
        if (head != null && head.key == key) { //
            buckets[hash(key)] = buckets[hash(key)].next;
            return;
        }
        
        while (head.next != null && head.next.key != key) {
            head = head.next;
        }
        
        if (head.next != null) { //
            head.next = head.next.next;
        }
    }
    
    public int hash(int key) {
        int capacity = buckets.length;
        
        return (key % capacity + capacity) % capacity;
    }
}
```
{% endtab %}
{% endtabs %}
