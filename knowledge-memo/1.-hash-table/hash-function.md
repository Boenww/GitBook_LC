---
description: lintcode
---

# 128. hash function

A widely used hash function algorithm is using a magic number 33, consider any string as a 33 based big integer like follow:

hashcode("abcd") = (ascii(a) \* 33^3 + ascii(b) \* 33^2 + ascii(c) \*33 + ascii(d)) % HASH\_SIZE&#x20;

&#x20;                             \= (97\* 33^3 + 98 \* 33^2 + 99 \* 33 +100) % HASH\_SIZE

&#x20;                             \= 3595978 % HASH\_SIZE

here HASH\_SIZE is the capacity of the hash table (you can assume a hash table is like an array with index 0 \~ HASH\_SIZE-1).

Given a string as a key and the size of hash table, return the hash value of this key.

{% tabs %}
{% tab title="Notes" %}
(a + b) % y = (a % y + b % y) % y

(ab) % y = (a % y)(b % y) % y
{% endtab %}

{% tab title="Solution" %}
```java
public int hashCode(char[] key, int HASH_SIZE) {
    long res = 0;
    for (int i = 0; i < key.length; i++) {
        res = (res * 33 + key[i]) % HASH_SIZE;
    }

    return (int)res; //HASH_SIZE is int -> not overflow
}
```
{% endtab %}
{% endtabs %}
