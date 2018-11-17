---
description: Similar with the problem of number of islands
---

# knight shortest path

{% tabs %}
{% tab title="Notes" %}
* eight groups of magic numbers
* 分层 -&gt; When to update the shortest length
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

class Solution {
	public int shortestPath(int[][] grid, Point source, Point destination) {
		if (grid == null || grid.length == 0 || grid[0].length == 0 ||
				!inBound(source, grid) || !inBound(destination, grid)) {
			return -1;
		}

		int res = 0;
		if (isSame(source, destination)) {
			return res;
		}

		int[] deltaX = {-2, -1, 1, 2, -2, -1, 1, 2};
		int[] deltaY = {1, 2, 2, 1, -1, -2, -2, -1};

		Queue<Point> queue = new LinkedList<>();
		grid[source.x][source.y] = 1;
		queue.offer(source);

		while (!queue.isEmpty()) {
			int size = queue.size();
			res++;
			for (int i = 0; i < size; i++) {
				Point point = queue.poll();
				for (int dir = 0; dir < 8; dir++) {
					Point next = new Point(point.x + deltaX[dir], point.y + deltaY[dir]);
					if (!inBound(next, grid) || grid[next.x][next.y] == 1) {
						continue;
					}

					if (isSame(next, destination)) {
						return res;
					}

					grid[next.x][next.y] = 1;
					queue.offer(next);
				}
			}
		}

		return -1;
	}

	public boolean inBound(Point point, int[][] grid) {
		return point.x >= 0 && point.x < grid.length && point.y >= 0 && point.y < grid[0].length;
	}

	public boolean isSame(Point source, Point destination) {
		return source.x == destination.x && source.y == destination.y;
	}

}
```
{% endtab %}
{% endtabs %}

