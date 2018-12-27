# knight shortest path II

If the knight is at \(x, y\), he can get to the following positions in one step:

```text
(x + 1, y + 2)
(x - 1, y + 2)
(x + 2, y + 1)
(x - 2, y + 1)
```

{% tabs %}
{% tab title="Notes" %}
* Use visited matrix to store the information of whether it is visited or not, rather than a set because of new class needed.
* bidirectional bfs should pay attention to deltaX and deltaY for the destination\(reverse\).
{% endtab %}

{% tab title="Solution" %}
```java
class Point {
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

public class Solution {
    /**
     * @param grid: a chessboard included 0 and 1
     * @return: the shortest path
     */
    private static final int[] startDeltaX = new int[]{1, -1, 2, -2};
    private static final int[] startDeltaY = new int[]{2, 2, 1, 1};
    private static final int[] endDeltaX = new int[]{-1, 1, -2, 2};
    private static final int[] endDeltaY = new int[]{-2, -2, -1, -1};
    
    public int shortestPath2(boolean[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0 || grid[0][0]
            || grid[grid.length - 1][grid[0].length - 1]) {
            return -1;
        }
        
        int n = grid.length, m = grid[0].length, shortest = 0;
        if (n == 1 && m == 1) {
            return shortest;
        }
        
        Queue<Point> startQueue = new LinkedList<>();
        startQueue.offer(new Point(0, 0));
        
        Queue<Point> endQueue = new LinkedList<>();
        endQueue.offer(new Point(n - 1, m - 1));
        
        boolean[][] startVisited = new boolean[n][m];
        boolean[][] endVisited = new boolean[n][m];
        startVisited[0][0] = true;
        endVisited[n - 1][m - 1] = true;
        while (!startQueue.isEmpty() && !endQueue.isEmpty()) {
            shortest++;
            int startSize = startQueue.size();
            for (int i = 0; i < startSize; i++) {
                Point start = startQueue.poll();
                for (int dir = 0; dir < 4; dir++) {
                    Point next = new Point(start.x + startDeltaX[dir], start.y + startDeltaY[dir]);
                    if (!inBound(next, n, m) || grid[next.x][next.y] || startVisited[next.x][next.y]) {
                        continue;
                    }
                    
                    if (endVisited[next.x][next.y]) {
                        System.out.println("n = " + n + " m = " + m);
                        System.out.println("x = " + next.x + " y = " + next.y + " val = " + grid[next.x][next.y]);
                        return shortest;
                    }
                    
                    startVisited[next.x][next.y] = true;
                    startQueue.offer(next);
                }
            }
            
            shortest++;
            int endSize = endQueue.size();
            for (int i = 0; i < endSize; i++) {
                Point end = endQueue.poll();
                for (int dir = 0; dir < 4; dir++) {
                    Point endNext = new Point(end.x + endDeltaX[dir], end.y + endDeltaY[dir]);
                    if (!inBound(endNext, n, m) || grid[endNext.x][endNext.y] || endVisited[endNext.x][endNext.y]) {
                        continue;
                    }
                    
                    if (startVisited[endNext.x][endNext.y]) {
                        return shortest;
                    }
                    
                    endVisited[endNext.x][endNext.y] = true;
                    endQueue.offer(endNext);
                }
            }
        }
        
        return -1;
    }
    
    public boolean inBound(Point p, int n, int m) {
        return p.x >= 0 && p.x < n && p.y >= 0 && p.y < m;
    }
}
```
{% endtab %}
{% endtabs %}

