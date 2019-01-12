# rehashing

Double the size of the hash table and rehash every keys. 

{% tabs %}
{% tab title="Notes" %}
* when the total size of the keys is too large\(e.g. 10%, 20%, 30%, ...\)
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */    
    public ListNode[] rehashing(ListNode[] hashTable) {
        int capacity = hashTable.length * 2;
        ListNode[] res = new ListNode[capacity];
        for (int i = 0; i < hashTable.length; i++) {
            ListNode node = hashTable[i];
            while (node != null) {
                int index = hash(node.val, capacity);
                if (res[index] == null) {
                    res[index] = new ListNode(node.val);
                } else {
                    ListNode head = res[index];
                    while (head.next != null) {
                        head = head.next;
                    }
                    
                    head.next = new ListNode(node.val);
                }
                
                node = node.next;
            }
        }
        
        return res;
    }
    
    public int hash(int key, int capacity) {
        return (key % capacity + capacity) % capacity; //avoid negative results
    }
};

```
{% endtab %}
{% endtabs %}

