Создание таблиц в [[SQLAlchemy|SQLAlchemy]] происходит при помощи [[Классы|класса]] Table. Перед созданием таблиц необходимо создать объект метаданных и передавать его при создании.

**Пример создания таблицы:**

```Python
from sqlalchemy import Table, Column, Integer, String, MetaData
from engines import engine  # Движок БД

metadata = MetaData()


users_table = Table(
	'users',
	metadata,
	Column('id', Integer, primary_key=True)
	Column('username', String)
)


metadata.drop_all(engine)
metadata.create_all(engine)
```

**Пример внесения данных в таблицу:**

```Python
from sqlalchemy import text


def insert_data():
	with engine.connect() as conn:
		statement = 'INSERT INTO users (username) VALUES ("User1"), ("User2")'
		conn.exec(text(statement))
		conn.commit()
```