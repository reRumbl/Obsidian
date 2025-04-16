[[FastAPI|FastAPI]] не вынуждает придерживаться определенной **структуры**, но если требуется создать хорошо масштабируемый и понятный проект, то лучше всего использовать одну из следующих структур:

- Микросервисный подход с делением по типам.

- Монолитный подход с делением по сущностям.

## Микросервисный подход

В микросервисном подходе используется структура, позволяющая разделить модели, схемы и т.д. по соответствующим папкам. Данная структура хорошо подхо

## Монолитный подход

В монолитном подходе используется структура, позволяющая выделить для каждой сущности свой файл с моделями, схемам и т.д. Данная структура хорошо подходит для огромных проектов с несколькими тысячами строк кода.

**Пример структуры:**

```plaintext
├── alembic/
├── app
│   ├── auth
│   │   ├── router.py
│   │   ├── schemas.py  # pydantic models
│   │   ├── models.py  # db models
│   │   ├── dependencies.py
│   │   ├── config.py  # local configs
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   ├── service.py
│   │   └── utils.py
│   ├── aws
│   │   ├── client.py  # client model for external service communication
│   │   ├── schemas.py
│   │   ├── config.py
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   └── utils.py
│   └── posts
│   │   ├── router.py
│   │   ├── schemas.py
│   │   ├── models.py
│   │   ├── dependencies.py
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   ├── service.py
│   │   └── utils.py
│   ├── config.py  # global configs
│   ├── models.py  # global models
│   ├── exceptions.py  # global exceptions
│   ├── pagination.py  # global module e.g. pagination
│   ├── database.py  # db connection related stuff
│   └── main.py
├── tests/
│   ├── auth
│   ├── aws
│   └── posts
├── templates/
│   └── index.html
├── requirements
│   ├── base.txt
│   ├── dev.txt
│   └── prod.txt
├── .env
├── .gitignore
├── logging.ini
└── alembic.ini
```