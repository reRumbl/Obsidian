**GeoPy** - модуль, который предоставляет различные инструменты работы с географическими данными.

![[GeoPy.png]]

**Установка через cmd или terminal:**

```Python
pip install geopy
```

**Подключение в проект:**

```Python
import geopy
```

**Геокодирование:** Этот процесс преобразует текстовые адреса или названия мест в географические координаты. Геокодирование позволяет ассоциировать данные с конкретными местами на карте.

**Пример геокодирования при помощи GeoPy:**

```Python
geolocator = geopy.geocoders.Nominatim(user_agent="geoapiExercises")
address = "1600 Amphitheatre Parkway, Mountain View, CA"

location = geolocator.geocode(address)

print("Адрес:", address)
print("Широта:", location.latitude)
print("Долгота:", location.longitude)
```
