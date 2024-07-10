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
from database import session_factory


class WorkersORM(Database):
	__table
	
	id: Mapped[int] = mapped_column(primary_key=True)
	username: Mapped[str]



with session_factory() as session:
	new_worker1 = WorkersORM(username='Andrew')
	new_worker2 = WorkersORM(username='Victor')
	session.add_all([new_worker1, new_worker2])
	session.commit()
```