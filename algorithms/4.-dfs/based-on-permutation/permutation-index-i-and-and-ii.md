# permutation index I && II

## I

Given a permutation which contains no repeated number, find its index in all the permutations of these numbers, which are ordered in lexicographical order. The index begins at 1.

{% tabs %}
{% tab title="Notes" %}
* exchange A\[i\] and smaller A\[j\]
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public long permutationIndex(int[] A) {
        long res = 1;
        long[] fac = new long[A.length];
        for (int i = 0; i < A.length; i++) {
            for (int j = i + 1; j < A.length; j++) {
                if (A[j] < A[i]) {
                    if (fac[A.length - 1 - i] != 0) {
                        res += fac[A.length - 1 - i];
                    } else {
                        long tmp = factorial(A.length - 1 - i);
                        res += tmp;   
                        fac[A.length - 1 - i] = tmp;
                    }
                }
            }
        }
        
        return res;
    }
    
    public long factorial(int n) {
        long res = 1;
        while (n > 0) {
            res *= n;
            n--;
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

## II

Given a permutation which may contain repeated numbers, find its index in all the permutations of these numbers, which are ordered in lexicographical order. The index begins at 1.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public long permutationIndexII(int[] A) {
        long res = 1;
        Map<Integer, Integer> count = getCount(A);
        for (int i = 0; i < A.length; i++) {
            Set<Integer> visited = new HashSet<>();
            for (int j = i + 1; j < A.length; j++) {
                if (A[j] < A[i] && !visited.contains(A[j])) {
                    visited.add(A[j]);
                    count.put(A[j], count.get(A[j]) - 1);
                    res += getPartial(count);
                    count.put(A[j], count.get(A[j]) + 1);
                }
            }
            
            count.put(A[i], count.get(A[i]) - 1);
        }
        
        return res;
    }
    
    public Map<Integer, Integer> getCount(int[] A) {
        Map<Integer, Integer> count = new HashMap<>();
        for (int i = 0; i < A.length; i++) {
            if (!count.containsKey(A[i])) {
                count.put(A[i], 1);
            } else {
                count.put(A[i], count.get(A[i]) + 1);
            }
        }
        
        return count;
    }
    
    public long getPartial(Map<Integer, Integer> count) {
        int sum = 0;
        long denominator = 1;
        for (Integer val: count.values()) {
            sum += val;
            denominator *= fac(val);
        }
        
        if (sum == 0) { // !!!
            return sum;
        }
        
        return fac(sum) / denominator;
    }
    
    public long fac(int num) {
        long res = 1;
        while (num > 0) {
            res *= num;
            num--;
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

