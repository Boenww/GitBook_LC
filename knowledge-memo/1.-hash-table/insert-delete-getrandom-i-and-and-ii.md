# insert delete getRandom I && II

## I

Design a data structure that supports all following operations in average `O(1)` time.

* `insert(val)`: Inserts an item val to the set if not already present.
* `remove(val)`: Removes an item val from the set if present.
* `getRandom`: Returns a random element from current set of elements. Each element must have the same probability of being returned.

{% tabs %}
{% tab title="Notes" %}
* arraylist + hashmap
* same question: load balancer
{% endtab %}

{% tab title="Solution" %}
```java
public class RandomizedSet {
    public List<Integer> list;
    public Map<Integer, Integer> valToIndex;
    public Random rand = new Random();
    
    public RandomizedSet() {
        list = new ArrayList<>();
        valToIndex = new HashMap<>();
    }

    /*
     * @param val: a value to the set
     * @return: true if the set did not already contain the specified element or false
     */
    public boolean insert(int val) {
        if (valToIndex.containsKey(val)) {
            return false;
        }
        
        list.add(val);
        valToIndex.put(val, list.size() - 1);
        return true;
    }

    /*
     * @param val: a value from the set
     * @return: true if the set contained the specified element or false
     */
    public boolean remove(int val) {
        if (!valToIndex.containsKey(val)) {
            return false;
        }
        
        int index = valToIndex.get(val);
        if (index != list.size() - 1) {
            int lastVal = list.get(list.size() - 1);
            list.set(index, lastVal);
            valToIndex.put(lastVal, index);
        }
        
        valToIndex.remove(val);
        list.remove(list.size() - 1);
        
        return true;
    }

    /*
     * @return: Get a random element from the set
     */
    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
        //random.nextInt(max - min + 1) + min
    }
}
```
{% endtab %}
{% endtabs %}

## II

Duplicate elements are allowed.

{% tabs %}
{% tab title="Notes" %}
* challenge for remove\(val\): change the "list.size\(\) - 1" index in map.get\(val\) would take more time
* Method to solve: use LinkedHashSet\(DLL internally and next call just returns the head of the Linkedlist which is first element in this case and moves the pointer to next element\) or store the index information in the list\(List&lt;numAndIndex&gt;\)
{% endtab %}

{% tab title="Solution" %}
```java
class RandomizedCollection {
    
    public Map<Integer, LinkedHashSet<Integer>> valToIndices;
    public List<Integer> list;
    public Random rand = new Random();
    
    /** Initialize your data structure here. */
    public RandomizedCollection() {
        valToIndices = new HashMap<>();
        list = new ArrayList<>();
    }
    
    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    public boolean insert(int val) {
        boolean res = !valToIndices.containsKey(val);
        list.add(val);
        
        if (res) {
            valToIndices.put(val, new LinkedHashSet<>());
        }
        
        valToIndices.get(val).add(list.size() - 1);
        return res;
    }
    
    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    public boolean remove(int val) {
        if (!valToIndices.containsKey(val)) {
            return false;
        }
        
        Set<Integer> valIndices = valToIndices.get(val);
        int index = valIndices.iterator().next();
        int replaceVal = list.get(list.size() - 1);
        
        list.set(index, replaceVal);
        valIndices.remove(index);
        if (valIndices.isEmpty()) {
            valToIndices.remove(val);
        }
        
        if (index != list.size() - 1) {
            Set<Integer> replaceIndices = valToIndices.get(replaceVal);
            replaceIndices.remove(list.size() - 1);
            replaceIndices.add(index);
        }
    
        list.remove(list.size() - 1);
        
        return true;
    }
    
    /** Get a random element from the collection. */
    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
    }
}
```
{% endtab %}
{% endtabs %}

