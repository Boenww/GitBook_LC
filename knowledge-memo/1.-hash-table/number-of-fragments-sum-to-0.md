# number of fragments sum to 0

Write a function solution that, given an array A consisting of N integers, returns the number of fragments of A whose sum equals 0 (that is, pairs (P, Q) such that P<= Q and the sum A\[P] + A\[P+1] + ... + A\[Q] is 0). The function should return -1 if this number exceeds 1000000000.&#x20;

Example: Given A = \[2, -2, 3, 0, 4, -7], the function should return 4. Given A=\[0, 0, ..., 0] of length 100,000, the function should return -1.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
{% code fullWidth="false" %}
```java
// Some code
public int solution(int[] A) {
    int count = 0;
    int sum = 0;
    
    Map<Integer, Integer> sumToCount = new HashMap<>();
    for (int i = 0; i < A.length; i++) {
        sum += A[i];
        if (sum == 0) {
            count++;
        }
        
        if (sumToCount.containsKey(sum)) {
            count += sumToCount.get(sum);
        }
        sumToCount.put(sum, sumToCount.getOrDefault(sum, 0) + 1);

        if (count > 1000000000) {
            return -1;
        }
    }
    
    return count;
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
