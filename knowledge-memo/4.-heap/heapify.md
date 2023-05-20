---
description: lintcode
---

# 130. heapify

Given an integer array, heapify it into a min-heap array.For a heap array A, A\[0] is the root of heap, and for each A\[i], A\[i \* 2 + 1] is the left child of A\[i] and A\[i \* 2 + 2] is the right child of A\[i].

{% tabs %}
{% tab title="Notes" %}
* sift up O(nlogn)
* sift down O(n)

由于所有的leaf node本身都能被看成是一个min heap，所以算法从倒数第二层开始进行siftdown操作，就是第 n/2 个数开始（# of the leaf node = 2^(n - 1) = (2^n - 1) / 2。倒数第二层的节点大约有 n/4 个， 这 n/4 个数，最多 siftdown 1次就到底了，所以这一层的时间复杂度耗费是 O(n/4)，然后倒数第三层差不多 n/8 个点，最多 siftdown 2次就到底了。所以这里的耗费是 O(n/8 \* 2), 倒数第4层是 O(n/16 \* 3)，倒数第5层是 O(n/32 \* 4) ... 因此累加所有的时间复杂度耗费为：

```
T(n) = O(n/4) + O(n/8 * 2) + O(n/16 * 3) ...
```

然后我们用 2T - T 得到：

```
2 * T(n) = O(n/2) + O(n/4 * 2) + O(n/8 * 3) + O(n/16 * 4) ... 
T(n)     =          O(n/4)     + O(n/8 * 2) + O(n/16 * 3) ...

2 * T(n) - T(n) = O(n/2) +O (n/4) + O(n/8) + ...
                = O(n/2 + n/4 + n/8 + ... )
                = O(n)
```

因此得到 `T(n) = 2 * T(n) - T(n) = O(n)`
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public void heapify(int[] A) {
        for (int i = 0; i < A.length; i++) {
            siftup(A, i);
        }
    }
    
    private void siftup(int[] A, int k) {
        while (k != 0) {
            int parent = (k - 1) / 2;
            if (A[k] >= A[parent]) {
                break;
            }
            int temp = A[k];
            A[k] = A[parent];
            A[parent] = temp;
            
            k = parent;
        }
    }
}

public class Solution {
    private void siftdown(int[] A, int k) {
        while (2 * k + 1 < A.length) {
            int child = 2 * k + 1;
            
            if (2 * k + 2 < A.length && A[2 * k + 2] < A[child]) {
                child = k * 2 + 2;
            }
            
            if (A[k] <= A[child]) {
                break;
            }
            
            int tmp = A[k];
            A[k] = A[child];
            A[child] = tmp;
            
            k = child;
        }
    }
    
    public void heapify(int[] A) {
        for (int i = A.length / 2 - 1; i >= 0; i--) {
            siftdown(A, i);
        }
    }
}
```
{% endtab %}
{% endtabs %}

