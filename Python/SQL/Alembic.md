**Alembic** – это инструмент миграции базы данных для языка [[Python|Python]]. Его основное преимущество заключается в том, что он позволяет легко изменять схему [[SQL|базы данных]] на разных этапах разработки проекта.

![[Alembic.png]]

**Установка через cmd или terminal:**

```Python
pip install alembic
```

**Подключение в проект:**

```Python
import alembic
```

## Инициализация и конфигурация Alembic

Инициализация **Alembic** происходит при помощи специальной консольной команды в определенной директории.

**Инициализация Alembic через cmd или terminal:**

```Python
alembic init alembic  # Название новой директории
```

**После инициализации появляется набор файлов:**

- **alembic.ini** - В директории вызова команды.

- **env.py** - В выбранной директории.

- **Readme** - В выбранной директории.

- **script.py.mako** - В выбранной директории.

- **Директория versions** - В выбранной директории.

**Базовая конфигурация строится из следующих шагов:**

1. **Изменение ссылки на БД в alembic.ini:** 

```Python
sqlalchemy.url = %(DB_URL)s?async_fallback=True
```

2. **Передача переменных для подстановки через env.py:**

```Python
from config import settings

# this is the Alembic Config object, which provides  
# access to the values within the .ini file in use.  
config = context.config  # Сгенерировано автоматически, остальное добавлено

section = config.config_ini_section  
config.set_section_option(section, 'DB_URL', settings.database_url_asyncpg)
```

3. **Передача метаданных в env.py:**

```Python
from app.database import Base

# add your model's MetaData object here  
# for 'autogenerate' support  
# from myapp import mymodel  
# target_metadata = mymodel.Base.metadata  
target_metadata = Base.metadata  # Изначально записано, как None
```

## Работа с версиями в Alembic

После инициализации и конфигурации требуется создать ревизию. **Ревизия** - разница между текущим состоянием базы данных и ее состоянием в коде.

**Создание ревизии через cmd или terminal:**

```Python
alembic revision --autogenerate -m "Database creation"
```


Для обновления до каких-либо версий используется команда upgrade.

**Обновление до последней версии через cmd или terminal:**

```Python
alembic upgrade head
```