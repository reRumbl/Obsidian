**SQLAlchemy ORM**.

**Создание декларативной базы данных:**

```Python
from sqlalchemy.orm import DeclarativeBase


class Database(DeclarativeBase):
	pass
```

**Создание таблиц и запросов в декларативной базе данных:**

```Python
from sqlalchemy.orm import Mapped, mapped_column
from sessions import session_factory  # Фабрика сессий


class WorkersORM(Database):
	__tablename__ = 'workers'
	
	id: Mapped[int] = mapped_column(primary_key=True)
	username: Mapped[str]


with session_factory() as session:
	new_worker1 = WorkersORM(username='Andrew')
	new_worker2 = WorkersORM(username='Victor')
	session.add_all([new_worker1, new_worker2])
	session.commit()
```