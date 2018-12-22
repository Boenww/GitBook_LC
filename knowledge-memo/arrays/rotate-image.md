---
description: >-
  Given an n x n 2D matrix representing an image. Rotate it by 90 degrees
  clockwise or anticlockwise.
---

# rotate image

{% tabs %}
{% tab title="Notes" %}
* Rotate clockwise: transpose -&gt; rotate horizontally 
* Rotate anti-clockwise: transpose -&gt; rotate vertically 
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {  
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int r = 0; r < n; r++) {
            for (int c = r; c < n; c++) {
                int tmp = matrix[r][c];
                matrix[r][c] = matrix[c][r];
                matrix[c][r] = tmp;
            }
        }
        
        for (int r = 0; r < n; r++) {
            for (int c = 0; c < n / 2; c++) {
                int tmp = matrix[r][c];
                matrix[r][c] = matrix[r][n - c - 1];
                matrix[r][n - c - 1] = tmp;
            }
        }
    }
    
    public void anti-rotate(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }
        
        int n = matrix.length;
        for (int r = 0; r < n; r++) {
            for (int c = r; c < n; c++) {
                int tmp = matrix[r][c];
                matrix[r][c] = matrix[c][r];
                matrix[c][r] = tmp;
            }
        }
        
        for (int r = 0; r < n / 2; r++) {
            for (int c = 0; c < n; c++) {
                int tmp = matrix[r][c];
                matrix[r][c] = matrix[n - r - 1][c];
                matrix[n - r - 1][c] = tmp;
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

