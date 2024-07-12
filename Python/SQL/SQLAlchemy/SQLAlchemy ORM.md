**SQLAlchemy ORM**.

**Создание декларативной базы данных:**

```Python
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy import String

	str_200 = Annotated[str, 256]


class Database(DeclarativeBase):
	# Можно задать параметры, например:
	type_annotation_map = {
		str_256: String(256)
	}
```

**Создание таблиц и запросов в декларативной базе данных:**

```Python
from enum import Enum
from typing import Annotated
from sqlalchemy.orm import Base, Mapped, mapped_column
from sqlalchemy import ForeignKey, text
from engines import engine  # Движок БД
import datetime

intpk = Annotated[int, mapped_column(primary_key=True)]
created_at = Annotated[
	datetime.datetime,
	mapped_column(server_default=text('TIMEZONE("utc", now())'))
]
updated_at = Annotated[
	datetime.datetime, 
	mapped_column(default=datetime.utcnow(), onupdate=datetime.utcnow())
]


class Workers(Base):
	__tablename__ = 'workers'

	id: Mapped[intpk]
	username: Mapped[str]


class Workload(enum.Enum):
	parttime = 'parttime'
	fulltime = 'fulltime'


class Resumes(Base):
	__tablename__ = 'resumes'

	id: Mapped[intpk]
	title: Mapped[str]
	compensation: Mapped[int | None]
	worker_id: Mapped[int] = mapped_column(ForeignKey('workers.id', ondelete='CASCADE'))  # Можно Workers.id
	created_at: Mapped[created_at]
	updated_at: Mapped[updated_at]


Database.metadata.create_all(engine)

with session_factory() as session:
	new_worker1 = WorkersORM(username='Andrew')
	new_worker2 = WorkersORM(username='Victor')
	session.add_all([new_worker1, new_worker2])
	session.commit()
```
