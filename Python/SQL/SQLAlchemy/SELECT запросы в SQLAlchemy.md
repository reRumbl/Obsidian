## Простые Select запросы



## Запросы с фильтрами

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
result = db.execute(
    select(models.Album)
    .join(models.M2MAlbumsArtists)
    .filter_by(id_artist=artist_id)
)
```