При работе с [[SQLAlchemy|SQLAlchemy]] для любой СУБД требуется подключать соответствующий драйвер. Например, при работе с [[PostgreSQL|PostgreSQL]] можно подключить psycopg или asyncpg. Подключение драйвера и СУБД происходит по специальной ссылке.

**Формат ссылки:**

```Python
{СУБД}+{Драйвер}://{Пользователь}:{Пароль}@{Адрес}:{Порт}/{Название}
```

*Удобное форматирование ссылок при помощи класса, используя [[Dotenv|переменное окружение]] и [[Pydantic|Pydantic]]:*

```Python
from pydantic_settings import BaseSettings, SettingsConfigDict


class Settings(BaseSettings):
	DB_HOST: str
	DB_PORT: int
	DB_USER: str
	DB_PASS: str
	DB_NAME: str

	@property
	def DATABASE_URL_asyncpg(self):
		pass

	@property
	def DATABASE_URL_psycopg(self):
		return f'postgresql+psycopg://{self.DB_USER}:{self.DB_PASS}@{self.DB_HOST}:{self.DB+}'
```

**Создание движка:**

```Python
from sqlalchemy import create_engine, text

engine = create_engine(
	url='postgresql+psycopg://postgres:postgres@localhost:5432/name',
	echo=True,  # Вывод запросов в консоль
	pool_size=5,  # Максимум подключений
	max_overflow=10  # Максимум подключений сверх максимума
)
```

**Создание сырого запроса через движок:**

*Через connect (В конце происходит ROLLBACK):*

```Python
with engine.connect() as conn:
	res = conn.execute(text('SELECT VERSION()'))
	print(f'Result:\n{res.first()}')
```

*Через begin (В конце происходит COMMIT):*

```Python
with engine.begin() as conn:
	res = conn.execute(text('SELECT VERSION()'))
	print(f'Result:\n{res.first()}')
```

*В случае [[Асинхронность|асинхронного]] движка:*

```Python
import asyncio


async def get_version():
	async with engine.connect() as conn:
		res = await conn.execute(text('SELECT VERSION()'))
		print(f'Result:\n{res.first()}') 


asyncio.run(get_version())
```