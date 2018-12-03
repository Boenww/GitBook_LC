# minimum increment to make array unique

{% tabs %}
{% tab title="Notes" %}
Two methods:

* O\(nlogn\):

1. sort the input array
2. each element should be at least the previous element + 1

* O\(n\): 

1. record extra repeating times
2. when there is a slot and there are still duplicates, i.e. recorded times &gt; 0, take account the slot
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //Method 1
    public int minIncrementForUnique(int[] A) {
        int res = 0, min = 0;
        for (int i = 0; i < A.length; i++) {
            res += Math.max(min - A[i], 0);
            min = Math.max(min, A[i]) + 1;
        }
        
        return res;
    }
    
    //Method 2
    public int minIncrementForUnique(int[] A) {
        int[] count = new int[50000];
        for (int i: A) {
            count[i]++;
        }
        
        int res = 0, taken = 0;
        for (int i = 0; i < A.length; i++) {
            if (count[i] >= 2) {
                taken += count[i] - 1;
                res -= i * (count[i] - 1);
            } else if (count[i] == 0 && taken > 0) {
                taken--;
                res += i;
            }
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

