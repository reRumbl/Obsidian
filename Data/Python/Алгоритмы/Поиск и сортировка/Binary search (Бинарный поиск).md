**Бинарный поиск** - алгоритм поиска в заранее отсортированном массиве. Он схож с методом двух указателей.

**Использовать для:** 

- "Поиск в отсортированном массиве".

- "Найти элемент в циклически сдвинутом массиве"

**Реализация на [[Python|Python]]:**

```Python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target: 
	        return mid
        if arr[mid] < target: 
	        left = mid + 1
        else: 
	        right = mid - 1
    return -1
```

