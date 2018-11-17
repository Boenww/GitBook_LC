---
description: '# of connected-one areas'
---

# number of islands

{% tabs %}
{% tab title="Notes" %}
* Traverse and bfs each island
* Magic numbers
* Notice the type of the input matrix, corner case and modularity
{% endtab %}

{% tab title="Solution" %}
```java
class Coordinate {
    public int x, y;
    public Coordinate(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Solution {
    public int numIslands(int[][] grid) {
        //define return type
        int res = 0;
        
        //corner case
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return res;
        }
        
        for (int r = 0; r < grid.length; r++) {
            for (int c = 0; c < grid[0].length; c++) {
                if (grid[r][c] == 0) {
                    continue;
                }
                grid[r][c] = 0;
                bfs(new Coordinate(r, c), grid);
                res++;
            }
        }
        
        return res;
    }
    
    public void bfs(Coordinate start, int[][] grid) {
        Queue<Coordinate> queue = new LinkedList<>();
        queue.offer(start);
        
        int[] deltaX = {0, 0, -1, 1};
        int[] deltaY = {1, -1, 0, 0};
        
        while (!queue.isEmpty()) {
            Coordinate coor = queue.poll();
            for (int dir = 0; dir < 4; dir++) {
                Coordinate nb = new Coordinate(coor.x + deltaX[dir], 
                    coor.y + deltaY[dir]);
                if (!inBound(nb, grid.length, grid[0].length) ||
                    grid[nb.x][nb.y] == 0) {
                    continue;
                }
                grid[nb.x][nb.y] = 0;
                queue.offer(nb);
            }
        }
    }
    
    public boolean inBound(Coordinate coor, int rowSize, int colSize) {
        return coor.x >= 0 && coor.x < rowSize && coor.y >= 0 && 
            coor.y < colSize;
    }
}
    
```
{% endtab %}
{% endtabs %}

