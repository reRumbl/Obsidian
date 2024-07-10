**SQLAlchemy ORM**.

**Создание декларативной базы данных:**

```Python
from sqlalchemy.orm import DeclarativeBase


class Database(DeclarativeBase):
	pass
```

**Создание таблиц в декларативной базе данных:**

```Python
from sqlalchemy.orm import Mapped, mapped_column
from ... import session


class WorkersORM(Database):
	id: Mapped[int] = mapped_column(primary_key=True)
	username: Mapped[str]


new_worker = WorkersORM(username='Andrew')
with session() as session:
	session.add(new_worker)
```