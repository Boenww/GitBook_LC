# first unique number in a stream I & II

## II

We need to implement a data structure named `DataStream`. There are `two` methods required to be implemented:

1. `void add(number)` // add a new number
2. `int firstUnique()` // return first unique number

```
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

## I

Given a data stream, write a function that returns the first unique number when the end number arrives (including the end number), and return -1 if cannot find the end number.

```
Example:
Input:
[1, 2, 2, 1, 3, 4, 4, 5, 6]
5

Output:
3

Input:
[1, 2, 2, 1, 3, 4, 4, 5, 6]
7

Output:
-1
```

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
// if iterates twice is allowed
public int firstUniqueNumber(int[] nums, int number) {
    // Write your code here
    Map <Integer, Integer> numToCounter = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        numToCounter.put(nums[i], numToCounter.getOrDefault(nums[i], 0) + 1);
        if (nums[i] == number) {
            break;
        }

        if (i == nums.length - 1) {
            return -1;
        }
    }

    for (int i = 0; i < nums.length; i++) {
        if (numToCounter.get(nums[i]) == 1) {
            return nums[i];
        }
    }

    return -1;
}

// if not allowed, same solution as II
```
{% endtab %}
{% endtabs %}
