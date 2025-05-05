Для создания таблиц в [[SQLModel|SQLModel]], нужно наследовать новый класс от одноименного класса из данной библиотеки и объявить поля.

**Пример создания таблицы:**

```Python
from sqlmodel import SQLModel, Field


class Hero(SQLModel, table=True):
	id: int | None = Field(default=None, primary_key=True)
	name: str
	secret_name: str
	age: int | None = None
```

**Пример создания записей в таблице:**

```Python
hero_1 = Hero(name='Deadpond', secret_name='Dive Wilson')
hero_2 = Hero(name='Spider-Boy', secret_name='Pedro Parqueador')
hero_3 = Hero(name='Rusty-Man', secret_name='Tommy Sharp', age=48)
```

