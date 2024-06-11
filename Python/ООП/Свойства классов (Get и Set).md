**Свойства классов** - это специальные методы для работы с полями [[Классы|класса]]. В языках ООП геттеры и сеттеры используются для извлечения и обновления данных. Метод получения извлекает текущее значение атрибута объекта, тогда как средство установки изменяет значение атрибута объекта.

Геттеры и сеттеры в Python отличаются от методов в других языках ООП. Основное использование методов получения и установки – обеспечение инкапсуляции данных в объектно-ориентированных программах. В отличие от других объектно-ориентированных языков, частные переменные в Python не являются скрытыми полями. Некоторые языки ООП используют методы получения и установки для инкапсуляции данных. Мы хотим скрыть атрибуты класса объекта от других классов, чтобы методы других классов случайно не изменили данные.

**Реализация простых get и set на примере обычного класса:**

```Python
class People:
	def __init__(self, name, surname, age, profession):  # Конструктор класса
		self._name = name
		self._surname = surname
		self._age = age
		self._profession = profession

	def set_age(self, age):  # Метод Get для поля age
		self._age = age

	def get_age(self):  # Метод Set для поля age
		return self._age


dima = People('Дмитрий', 'Чеботков', 19, 'Ozon-Фреш Консультант')
dima.set_age(1488)
print(dima.get_age() == dima._age)
```

## Использование функции property() в качестве геттеров и сеттеров

В Python property() является встроенной функцией для создания и возврата свойства объекта. Есть три метода: getter(), setter() и delete(). В Python функция property() принимает четыре аргумента: свойства (fget, fset, fdel, doc). Функция fget используется для получения значения атрибута. Функция fset используется для установки значения атрибута. Функция fdel используется для удаления значения атрибута. Атрибуту присваивается строка документации doc.

**Пример класса с функцией property():**

```Python
class People:
	def __init__(self, name, surname, age, profession):  # Конструктор класса
		self._name = name
		self._surname = surname
		self._age = age
		self._profession = profession

	def set_age(self, age):  # Метод Get для поля age
		self._age = age

	def get_age(self):  # Метод Set для поля age
		return self._age

	def del_age(self):  # Метод Del для поля age
		del self._age

	age = property(get_age, set_age, del_age, 'Возраст')


dima = People('Дмитрий', 'Чеботков', 19, 'Ozon-Фреш Консультант')
dima.age = 1488
print(dima.age)
```

**Пример класса с декораторами @property:**

```Python
class People:
	def __init__(self):  # Конструктор класса
		self._age = age

	def set_age(self, age):  # Метод Get для поля age
		self._age = age

	def get_age(self):  # Метод Set для поля age
		return self._age

	def del_age(self):  # Метод Del для поля age
		del self._age

	age = property(get_age, set_age, del_age, 'Возраст')


dima = People('Дмитрий', 'Чеботков', 19, 'Ozon-Фреш Консультант')
dima.age = 1488
print(dima.age)
```