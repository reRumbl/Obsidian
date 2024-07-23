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

## Запросы с Join

При