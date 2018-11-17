# course schedule I && II

## course schedule I

There are a total of n courses you have to take, labeled from 0 to n-1. Some courses may have prerequisites, for example to take course 0 you have to first take course 1 as denoted as \[0, 1\].                Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish                   all courses?



{% tabs %}
{% tab title="Notes" %}
* Corner cases: when to return true directly; the number of pairs should be less or equal to n\(n - 1\) / 2, where n is the number of courses
* Two HashMaps: one preToCourse and the other IndegreeMap; preToCourse is needed for avoiding one more loop when checking the number of courses that require some pre, which can result in O\(n^3\); it is necessary to initialize  preToCourse with all possible keys from 0 to numCourses with some empty ArrayList to avoid NullPointerException when checking indegrees by getting values.
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses == 0 || prerequisites.length == 0) {
            return true;
        }
        
        Map<Integer, List<Integer>> preToCourse = new HashMap<>();
        Map<Integer, Integer> IndegreeMap = new HashMap<>();
        for (int n = 0; n < numCourses; n++) {
            preToCourse.put(n, new ArrayList<>());
        }
        
        for (int i = 0; i < prerequisites.length; i++) {
            preToCourse.get(prerequisites[i][1]).add(prerequisites[i][0]);
            if (!IndegreeMap.containsKey(prerequisites[i][0])) {
                IndegreeMap.put(prerequisites[i][0], 1);
            } else {
                IndegreeMap.put(prerequisites[i][0], IndegreeMap.get(prerequisites[i][0]) + 1);
            }
        }
        
        Queue<Integer> queue = new LinkedList<>();
        for (int n = 0; n < numCourses; n++) {
            if (!IndegreeMap.containsKey(n)) {
                queue.offer(n);
            }
        }
        
        List<Integer> order = new ArrayList<>();
        while (!queue.isEmpty()) {
            Integer pre = queue.poll();
            order.add(pre);
            for (Integer course: preToCourse.get(pre)) {
                if (IndegreeMap.get(course) - 1 == 0) {
                    queue.offer(course);
                }
                IndegreeMap.put(course, IndegreeMap.get(course) - 1);
            }
        }
        
        return order.size() == numCourses;
    }
}
```
{% endtab %}
{% endtabs %}

## course schedule II

Return one of the correct order and an empty array if it is impossible.

{% tabs %}
{% tab title="Notes" %}
* take account for the length of the result list and compare with numCourses to determine if there is a topological order
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int[] res = new int[numCourses];
        
        Map<Integer, List<Integer>> preToCourse = new HashMap<>();
        Map<Integer, Integer> IndegreeMap = new HashMap<>();
        for (int n = 0; n < numCourses; n++) {
            preToCourse.put(n, new ArrayList<>());
        }
        
        for (int i = 0; i < prerequisites.length; i++) {
            preToCourse.get(prerequisites[i][1]).add(prerequisites[i][0]);
            if (!IndegreeMap.containsKey(prerequisites[i][0])) {
                IndegreeMap.put(prerequisites[i][0], 1);
            } else {
                IndegreeMap.put(prerequisites[i][0], IndegreeMap.get(prerequisites[i][0]) + 1);
            }
        }
        
        Queue<Integer> queue = new LinkedList<>();
        for (int n = 0; n < numCourses; n++) {
            if (!IndegreeMap.containsKey(n)) {
                queue.offer(n);
            }
        }
        
        int count = 0; //
        while (!queue.isEmpty()) {
            Integer pre = queue.poll();
            res[count++] = pre; //

            for (Integer course: preToCourse.get(pre)) {
                if (IndegreeMap.get(course) - 1 == 0) {
                    queue.offer(course);
                }
                IndegreeMap.put(course, IndegreeMap.get(course) - 1);
            }
        }
        
        return count == numCourses ? res : new int[]{}; //
    }
}
```
{% endtab %}
{% endtabs %}

