# Quick Sort

{% tabs %}
{% tab title="Notes" %}
1. determine a pivot 

2. partition \(&lt;= pivot, &gt;= pivot\):

```text
i -> head, j -> tail
if i < pivot, right shift i
if j > pivot, left shift j
else 
swap i and j, repeat
```

* time: O\(n^2\) worst case\(sorted and pivot chosen as head\), O\(nlogn\) best case
* space: O\(logn\)
* case ==pivot: also swap value -&gt; reduce problem scale and let them be as equal as possible
{% endtab %}

{% tab title="Solution" %}
```java
public static void quickSort(int[] array) {
	quickSortHelper(array, 0, array.length - 1);
}

private static void quickSortHelper(int[] array, int left, int right) {
	if (left >= right) {
		return;
	}

	int i = left, j = right;
	int pivot = array[left + (right - left) / 2];

	while (i <= j) {
		while (i <= j && array[i] < pivot) { // 
			i++;
		}

		while (i <= j && array[j] > pivot) {
			j--;
		}

		if (i <= j) {
			swap(array, i++, j--);
		}
	}

	quickSortHelper(array, left, j);
	quickSortHelper(array, i, right);
}

public static void swap(int[] array, int left, int right) {
	int tmp = array[left];
	array[left] = array[right];
	array[right] = tmp;
}
```
{% endtab %}
{% endtabs %}

