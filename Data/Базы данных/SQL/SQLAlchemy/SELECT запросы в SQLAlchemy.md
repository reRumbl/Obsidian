В [[SQLAlchemy|SQLAlchemy]] можно делать как сырые [[SQL|SQL]] запросы через движок, так и построенные запросы. Сырые запросы делаются при помощи простой конструкции с методом execute и требуют полностью писать запрос на [[SQL|SQL]], а построенные запросы происходят при помощи [[SQLAlchemy ORM| SQLAlchemy ORM]] и методов в специальных [[Классы|классах]].

## Простые Select запросы

**Простой запрос всех столбцов таблицы при помощи SQL:**

```Python
from sqlalchemy import text
from database import db  # Сессия

result = db.execute(text('SELECT * FROM tracks'))
```

**Простой запрос всех столбцов таблицы при помощи ORM:**

```Python
import models  # ORM модели

result = db.execute(select(models.Track))
```

## Запросы с фильтрами

**Пример выражения с offset:**

```Python
skip = 0
result = db.execute(  
    select(models.Track)
    .offset(skip)
)
```

**Пример выражения с limit:**

```Python
prompt = 'Love'
skip = 0
limit = 10
result = db.execute(  
    select(models.Track)
    .limit(limit)
)
```

**Пример выражения с like:**

```Python
prompt = 'Master of Puppets'
result = db.execute(  
	select(models.Track)  
	.filter(models.Track.name.like(f'%{prompt}%'))
)
```

**Пример комбинации фильтров:**

```Python
prompt = 'Love'
skip = 0
limit = 10
result = db.execute(  
    select(models.Track)  
    .filter(models.Track.name.like(f'%{prompt}%'))
    .offset(skip)
    .limit(limit)
)
```

## Запросы с Join

**Пример выражения с join:**

```Python
artist_id = 1
result = db.execute(
    select(models.Album)
    .join(models.M2MAlbumsArtists)
    .filter_by(id_artist=artist_id)
)
```