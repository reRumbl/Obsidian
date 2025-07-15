Метод двух указателей - это алгоритм эффективного прохождения по массиву с двух концов одновременно.

**Использовать для:** 

- "Сумма двух чисел".

- "Триплеты с нулевой суммой".

- "Контейнер с водой".

**Пример на [[Python|Python]]:**

```Python
def two_pointers(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        s = arr[left] + arr[right]
        if s == target: 
	        return [left, right]
        if s < target: 
	        left += 1
        else: 
	        right -= 1
```