Существуют разные способы создания таблиц в [[SQLAlchemy|SQLAlchemy]], начиная с простого [[SQL|SQL]] запроса и заканчивая созданием таблицы на основе [[Классы|классов]].
## Создание и заполнение таблицы при помощи Table

Создание таблиц данным способом в [[SQLAlchemy|SQLAlchemy]] происходит при помощи [[Классы|класса]] Table. Перед созданием таблиц необходимо создать объект метаданных и передавать его при создании.

**Пример создания таблицы через Table:**

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

**Пример внесения данных в таблицу на основе Table:**

*Через сырой запрос:*

```Python
from sqlalchemy import text


def insert_data():
	with engine.connect() as conn:
		statement = 'INSERT INTO users (username) VALUES ("User1"), ("User2")'
		conn.exec(text(statement))
		conn.commit()


insert_data()
```

*Через построитель запросов:*

```Python
from sqlalchemy import insert

def insert_data():
	with engine.connect() as conn:
		statement = insert(users_table).values(
			[
				{'username': 'User1'},
				{'username': 'User2'}
			]
		)
		conn.exec(statement)
		conn.commit()


insert_data()
```

## Создание и заполнение таблицы при помощи ORM

Создание таблиц данным способом в [[SQLAlchemy|SQLAlchemy]] происходит при помощи [[Классы|класcа]] DeclarativeBase. Для этого следует [[Наследование|наследовать]] данный [[Классы|класс]]  для создания базы данных и создать [[Классы|классы]] таблиц с полями при помощи Mapped и mapped_column.

**Пример создания таблицы при помощи ORM:**

```Python
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column


class Database(DeclarativeBase):
	# Можно задать параметры
	pass


class WorkersORM(Database):
	__tablename__ = 'workers'
	
	id: Mapped[int] = mapped_column(primary_key=True)
	username: Mapped[str]
```

**Пример заполнения ORM таблицы:**

```Python
from sessions import session_factory  # Фабрика сессий

with session_factory() as session:
	new_worker1 = WorkersORM(username='Andrew')
	new_worker2 = WorkersORM(username='Victor')
	session.add_all([new_worker1, new_worker2])
	session.commit()
```