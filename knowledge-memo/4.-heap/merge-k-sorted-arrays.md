# 486. merge k sorted arrays

Given _k_ sorted integer arrays, merge them into one sorted array.

```text
Example:
[
  [1, 3, 5, 7],
  [2, 4, 6],
  [0, 8, 9, 10, 11]
]
```

return `[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]`.

{% tabs %}
{% tab title="Notes" %}
* Same methods as merge k sorted list
* PriorityQueue
* divide and conquer 
* bottom up
* O\(nlogk\)
* [merge k sorted interval lists](../interval/577.-merge-k-sorted-interval-lists.md)
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    class Element {
        public int row, col, val;
        public Element(int row, int col, int val) {
            this.row = row;
            this.col = col;
            this.val = val;
        }
    }

    public int[] mergekSortedArrays(int[][] arrays) {
        int k = arrays.length, n = 0;
        Queue<Element> minHeap = new PriorityQueue<>(k, new Comparator<Element>() {
            @Override
            public int compare(Element e1, Element e2) {
                return e1.val - e2.val;
            }            
        });
        
        for (int i = 0; i < k; i++) {
            if (arrays[i] == null || arrays[i].length == 0) { //!!! case:[[],[]]
                continue;
            }
            
            minHeap.offer(new Element(i, 0, arrays[i][0]));
            n += arrays[i].length;
        }
        
        int[] res = new int[n];
        int index = 0;
        while (!minHeap.isEmpty()) {
            Element min = minHeap.poll();
            res[index++] = min.val;
            if (min.col + 1 < arrays[min.row].length) {
                minHeap.offer(new Element(min.row, min.col + 1, arrays[min.row][min.col + 1]));
            }
        }
        
        return res;
    }
}

public class Solution {
    public int[] mergekSortedArrays_dc(int[][] arrays) {
        return mergekSortedArraysHelper(arrays, 0, arrays.length - 1);
    }
    
    public int[] mergekSortedArraysHelper(int[][] arrays, int start, int end) {
        if (start == end) {
            return arrays[start];
        }
        
        int mid = start + (end - start) / 2;
        int[] left = mergekSortedArraysHelper(arrays, start, mid);
        int[] right = mergekSortedArraysHelper(arrays, mid + 1, end);
        
        return mergeHelper(left, right);
    }
    
    //bottom up
    public int[] mergekSortedArrays_bottomUp(int[][] arrays) {
        while (arrays.length > 1) {
            int n = arrays.length / 2;
            if (arrays.length % 2 == 1) {
                n++;
            }
            
            int[][] tmp = new int[n][0];
            int index = 0;
            for (int i = 0; i < arrays.length - 1; i += 2) {
                tmp[index++] = mergeHelper(arrays[i], arrays[i + 1]);
            }
            
            if (index != n) {
                tmp[index] = arrays[arrays.length - 1];
            }
            
            arrays = tmp;
        }
        
        return arrays[0];
    }
    
    private int[] mergeHelper(int[] left, int[] right) {
        int[] res = new int[left.length + right.length];
        
        int i = 0, j = 0, index = 0;
        while (i < left.length && j < right.length) {
            if (left[i] < right[j]) {
                res[index++] = left[i++];
            } else {
                res[index++] = right[j++];
            }
        }
        
        while (i < left.length) {
            res[index++] = left[i++];
        }
        
        while (j < right.length) {
            res[index++] = right[j++];
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

