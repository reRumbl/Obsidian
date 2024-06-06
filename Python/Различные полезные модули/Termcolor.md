**Termcolor** - это модуль, который позволяет выводить форматированный текст в консоль через удобные функции. Данный модуль позволяет красить текст и добавлять ему атрибуты.

![[Termcolor.png]]

**Установка через cmd или terminal:**

```Python
pip install termcolor
```

**Подключение в проект:**

```Python
import termcolor
```

**Пример вывода цветного текста с атрибутами в консоль:**

```Python
print(termcolor.colored("Hello, World!", "red", attrs=["reverse", "blink"]))
```
