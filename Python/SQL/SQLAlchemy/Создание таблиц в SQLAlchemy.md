Создание таблиц в [[SQLAlchemy|SQLAlchemy]] происходит при помощи [[Классы|класса]] Table.

**Пример создания таблицы:**

```Python
from sqlalchemy import Table, Column, Integer, String, MetaData

metadata = MetaData()


workers_table = Table(
	'workers',
	metadata,
	Column('id', Integer, primary_key=True)
	Column('username', String)
)


metadata.create_all(engine)
```