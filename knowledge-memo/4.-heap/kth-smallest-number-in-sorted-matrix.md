# kth smallest number in sorted matrix

Find the _k_th smallest number in a row and column sorted matrix.

```text
Example:
Given k = 4 and a matrix:
[
  [1 ,5 ,7],
  [3 ,7 ,8],
  [4 ,8 ,9],
]
```

return `5`

{% tabs %}
{% tab title="Notes" %}
Time Complexity: O\(klog\(min\(m,n,k\)\)\)，队列最大长度是最长对角线的元素的个数，也就是行和列长度的更小者；还有一点是当k最小时，队列的最大长度是k  
Space Complexity: O\(min\(m,n,k\) + mn\)，pq和visited数组的大小
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public int[] deltaX = new int[]{0, 1};
    public int[] deltaY = new int[]{1, 0};
    
    public int kthSmallest(int[][] matrix, int k) {
        Queue<int[]> pq = new PriorityQueue<>(new Comparator<int[]>() {
            @Override
            public int compare(int[] point1, int[] point2) {
                return matrix[point1[0]][point1[1]] - matrix[point2[0]][point2[1]];
            }
        });
        
        pq.offer(new int[2]);
        
        boolean[][] visited = new boolean[matrix.length][matrix[0].length];
        visited[0][0] = true;
        for (int i = 0; i < k - 1; i++) {
            int[] point = pq.poll();
            for (int j = 0; j < 2; j++) {
                int[] next = new int[]{point[0] + deltaX[j], point[1] + deltaY[j]};
                if (!inBound(next, matrix) || visited[next[0]][next[1]]) {
                    continue;
                }
                
                visited[next[0]][next[1]] = true;
                pq.offer(next);
            }
        }
        
        int[] res = pq.poll();
        return matrix[res[0]][res[1]];
    }
    
    public boolean inBound(int[] point, int[][] matrix) {
        int m = matrix.length, n = matrix[0].length;
        return point[0] >= 0 && point[0] < m && point[1] >= 0 && point[1] < n;
    }
}
```
{% endtab %}
{% endtabs %}



