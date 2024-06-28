При работе с [[SQLAlchemy|SQLAlchemy]] для любой СУБД требуется подключать соответствующий драйвер. Например, при работе с [[PostgreSQL|PostgreSQL]] можно подключить psycopg или asyncpg. Подключение драйвера и СУБД происходит по специальной ссылке.

**Формат ссылки:**

```Python
{СУБД}+{Драйвер}://{Пользователь}:{Пароль}@{Адрес}:{Порт}/{Название}
```

**Создание движка:**

```Python
engine = create_engine(
	url='postgresql+psycopg://postgres:postgres@localhost:5432/name',
	echo=True,  # Вывод запросов в консоль
	pool_size=5,  # Максимум подключений
	max_overflow=10  # Максимум подключений сверх максимума
)
```

**Создание сырого запроса через движок:**

```Python
with engine.connect() as conn:
	res = conn.execute('SELECT VERSION()')
```

