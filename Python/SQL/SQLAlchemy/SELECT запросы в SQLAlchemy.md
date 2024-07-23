## Простые Select запросы



## Запросы с фильтрами

**Выражение с like:**

```

posts = Post.query.filter(Post.tags.like(search)).all()
```

## Запросы с Join