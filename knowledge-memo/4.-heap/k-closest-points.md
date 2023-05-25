---
description: lc. 973 lintcode 612.
---

# k closest points

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance (i.e., `√(x1 - x2)2 + (y1 - y2)2`).

{% tabs %}
{% tab title="Notes" %}
* NlogK: priority queue
* N + KlogN: heapify and pop K elements, better if N >> k
* O(N) average O(N^2) worst quick select
{% endtab %}

{% tab title="Solution" %}
```java

class Point {
    int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Solution {
    public int[][] kClosest(int[][] points, int k) {
        int[][] res = new int[k][2];

        // max heap
        Queue<Point> pq = new PriorityQueue<>(k, new Comparator<Point>() {
            @Override
            public int compare(Point p1, Point p2) {
                return getDistance(p2) - getDistance(p1);
            }
        });
        for (int i = 0; i < points.length; i++) {
            pq.add(new Point(points[i][0], points[i][1]));
            if (pq.size() > k) {
                pq.poll();
            }
        }
        
        int i = 0;
        while (!pq.isEmpty()) {
            Point p = pq.poll();
            res[i][0] = p.x;
            res[i++][1] = p.y;
        }

        return res;
    }

    public int getDistance(Point p) {
        return p.x * p.x + p.y * p.y;
    }
}
```
{% endtab %}
{% endtabs %}
