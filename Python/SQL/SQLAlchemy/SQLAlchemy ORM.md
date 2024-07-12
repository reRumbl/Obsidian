**SQLAlchemy ORM**.

**Создание декларативной базы данных:**

```Python
from sqlalchemy.orm import DeclarativeBase


class Database(DeclarativeBase):
	pass
```

**Создание таблиц и запросов в декларативной базе данных:**

```Python
from enum import Enum
from sqlalchemy.orm import Base, Mapped, mapped_column
from sqlalchemy import ForeignKey


class Workers(Base):
	__tablename__ = 'workers'

	id: Mapped[int] = mapped_column(primary_key=True)
	username: Mapped[str]


class Workload(enum.Enum):
	parttime = 'parttime'
	fulltime = 'fulltime'


class Resumes(Base):
	__tablename__ = 'resumes'

	id: Mapped[int] = mapped_column(primary_key=True)
	title: Mapped[str]
	compensation: Mapped[int | None]
	worker_id: Mapped[int] = mapped_column(ForeignKey('workers.id', ondelete='CASCADE'))  # Можно Workers.id
	created_at: Mapped[datetime.]


with session_factory() as session:
	new_worker1 = WorkersORM(username='Andrew')
	new_worker2 = WorkersORM(username='Victor')
	session.add_all([new_worker1, new_worker2])
	session.commit()
```