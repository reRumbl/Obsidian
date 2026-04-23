**Когда использовать**:

- Нужно перебрать все возможные комбинации

- Задачи на размещение, перестановки

**Шаблонный пример на [[Python|Python]]:**

```Python
def backtrack(path, choices):
    if {удовлетворяет условию}:
        {результат}.append(path[:])
        return
    
    for {выбор} in choices:
        if {выбор} {валиден}:
            path.append({выбор})
            backtrack(path, {новые_choices})
            path.pop()
```