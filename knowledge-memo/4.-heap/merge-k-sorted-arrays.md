# merge k sorted arrays

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
            if (arrays[i] == null || arrays[i].length == 0) {
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
```
{% endtab %}
{% endtabs %}

