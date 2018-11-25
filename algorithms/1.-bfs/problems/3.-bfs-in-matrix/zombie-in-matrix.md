# zombie in matrix

Given a 2D grid, each cell is either a wall `2`, a zombie `1` or people `0` \(the number zero, one, two\).Zombies can turn the nearest people\(up/down/left/right\) into zombies every day, but can not through wall. How long will it take to turn all people into zombies? Return `-1` if can not turn all people into zombies.

{% tabs %}
{% tab title="Notes" %}
* Level information is useful to find the number of days needed
* res - 1 is necessary for the final correct output\(one extra day if not\)
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

public class Solution {
    /**
     * @param grid: a 2D integer grid
     * @return: an integer
     */
    public int zombie(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        
        Queue<Coordinate> queue = new LinkedList<>();
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    queue.offer(new Coordinate(i, j));
                    visited[i][j] = true;
                }
            }
        }
        
        int res = 0, zombieNum = 0, wallNum = 0;
        int[] deltaX = new int[]{0, 0, 1, -1};
        int[] deltaY = new int[]{1, -1, 0, 0};
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Coordinate cur = queue.poll();
                zombieNum++;
                for (int j = 0; j < 4; j++) {
                    int x = cur.x + deltaX[j], y = cur.y + deltaY[j];
                    if (!inBound(grid, x, y) || visited[x][y]) {
                        continue;
                    }
                
                    visited[x][y] = true;
                    if (grid[x][y] == 0) {
                        queue.offer(new Coordinate(x, y));
                        grid[x][y] = 1;
                    } else {
                        wallNum++;
                    }
                }
            }
            res++;
        }

        return zombieNum == grid.length * grid[0].length - wallNum ? res - 1 : -1;
    }
    
    public boolean inBound(int[][] grid, int x, int y) {
        return x >= 0 && x < grid.length && y < grid[0].length && y >= 0;
    }
    
}
```
{% endtab %}
{% endtabs %}

