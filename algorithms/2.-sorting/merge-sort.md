# Merge Sort

{% tabs %}
{% tab title="Notes" %}
* time: O\(nlogn\)
* space: O\(n\)
{% endtab %}

{% tab title="Solution" %}
```java
public static void mergeSort(int[] array) {
	int[] tmp = new int[array.length];
	mergeSortHelper(array, tmp, 0, array.Length - 1)
}

private static void mergeSortHelper(int[] array, int[] tmp, int left, int right) {
	//base case
	if (left >= right) {
		return;
	}

	//divide 
	int mid = left + (right - left) / 2;
	mergeSortHelper(array, tmp, left, mid);
	mergeSortHelper(array, tmp, mid + 1, right);

	//merge -> O(n)
	merge(array, tmp, left, right);
}

private static void merge(int[] array, int[] tmp, int left, int right) {
	int mid = left + (right - left) / 2;
	int i = left, j = mid + 1;
	//int[] tmp = new int[right - left + 1]; //heap: O(nlogn) -> O(n)
	for (int k = 0; k < right - left + 1; ++k) { //n: right - left + 1 each level
		if (i <= mid && (j > right || array[i] < array[j])) {
			tmp[k] = array[i++];
		} else {
			tmp[k] = array[j++];
		}
	}

	for (int k = 0; k < right - left + 1; ++k) {
		array[left + k] = tmp[k];
	}
}
```
{% endtab %}
{% endtabs %}

