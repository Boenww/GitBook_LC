# top k largest number I && II

## I

Given an integer array, find the top _k_ largest numbers in it.

#### Example

Given `[3,10,1000,-99,4,100]` and _k_ = `3`.  
Return `[1000, 100, 10]`.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
     //minHeap
    public int[] topk(int[] nums, int k) {
        Queue<Integer> pq = new PriorityQueue<>();
        for (int i = 0; i < nums.length; i++) {
            pq.offer(nums[i]);
        }
        
        while (pq.size() > k) {
            pq.poll();
        }
        
        int[] res = new int[k];
        while (k > 0) {
            res[--k] = pq.poll();
        }
    
        return res;
    }
    
    //maxHeap
    public int[] topk(int[] nums, int k) {
        Queue<Integer> maxHeap = new PriorityQueue<>(k, new Comparator<Integer>() {
            @Override
            public int compare(Integer num1, Integer num2) {
                return num2 - num1;
            }
        });
        
        for (int num: nums) {
            maxHeap.offer(num);
        }
        
        int[] res = new int[k];
        for (int i = 0; i < k; i++) {
            res[i] = maxHeap.poll();
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

## II

Implement a data structure, provide two interfaces:

1. `add(number)`. Add a new number in the data structure.
2. `topk()`. Return the top _k_ largest numbers in this data structure. _k_ is given when we create the data structure.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public Queue<Integer> pq;
    public int k;

    public Solution(int k) {
        pq = new PriorityQueue<>();
        this.k = k;
    }

    public void add(int num) {
        pq.offer(num);
        if (pq.size() > k) {
            pq.poll();
        }
    }

    public List<Integer> topk() {
        List<Integer> res = new ArrayList<>(pq);
        Collections.sort(res, Collections.reverseOrder());
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

