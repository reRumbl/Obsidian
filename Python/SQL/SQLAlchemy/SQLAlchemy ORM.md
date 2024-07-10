**SQLAlchemy ORM**.

**Создание декларативной базы данных:**

```Python
from sqlalchemy import DeclarativeBase


class Database(DeclarativeBase):
	pass
```

**Создание таблиц в декларативной базе данных:**

```Python
from sqlalchemy.orm import Mapped, mapped_column


class WorkersORM(Database):
	id: Mapped[int] = mapped_column(primary_key=True)
	username: Mapped[str]
	
```