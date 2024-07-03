Создание таблиц в [[SQLAlchemy|SQLAlchemy]] происходит при помощи [[Классы|класса]] Table. Перед созданием таблиц необходимо создать объект метаданных и передавать его при создании.

**Пример создания таблицы:**

```Python
from sqlalchemy import Table, Column, Integer, String, MetaData
from engines import engine  # Движок БД

metadata = MetaData()


workers_table = Table(
	'workers',
	metadata,
	Column('id', Integer, primary_key=True)
	Column('username', String)
)


metadata.drop_all(engine)
metadata.create_all(engine)
```