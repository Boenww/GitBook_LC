# \* binary indexed tree

Regarding to an array of size N, BIT supports updating value in certain index and getting prefix sum in log\(N\) time. BIT\[0\] is set as empty.

## getPrefixSum\(idx\)

```text
while idx > 0
 sum += BIT[idx]
 idx -= lowbit(idx)
```

## update\(idx, val\)

```text
delta = val - A[idx]
while idx <= N
    BIT[idx] += delta
    idx += lowbit(idx)
```

## lowbit\(x\)

```text
x & (-x)
```

