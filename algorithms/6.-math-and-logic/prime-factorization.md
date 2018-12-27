# prime factorization

Prime factorize a given integer.

{% tabs %}
{% tab title="Notes" %}
* Space O\(logn\), as the worst case would be that all prime factors are 2.
* Time O\(sqrt\(n\)\)
*  首先，约数是成对出现的。比如24,找到个约数3,那么一定有个约数8,因为24/3=8。然后，这对约数必须一个在根号n之前，一个在根号n之后。因为都在根号n之前的话，乘积一定小于n（根号nX根号n=n），同样，都在根号n之后的话，乘积一定大于n。所以，如果在根号n之前都找不到约数的话，那么根号n之后就不会有了。
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param num: An integer
     * @return: an integer array
     */
    public List<Integer> primeFactorization(int num) {
        List<Integer> res = new ArrayList<>();
        
        int up = (int) Math.sqrt(num); 
        for (int i = 2; i <= up; i++) { // can set the condition to be i * i <= num
            while (num % i == 0) {
                res.add(i);
                num /= i;
            }
        }
        
        if (num > 1) {
            res.add(num);
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

