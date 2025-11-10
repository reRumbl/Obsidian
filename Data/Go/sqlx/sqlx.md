**sqlx** - это популярная библиотека, которая расширяет стандартный [[Go/Стандартные пакеты Go/database/sql|database/sql]], добавляя удобные функции для маппинга (например, `db.Get()` для одной строки, `db.Select()` для среза структур). Использует теги полей (`db:"column_name"`) для автоматического заполнения структур.

## Основные возможности

**Создание БД:**

```Go
var db *sqlx.DB

// New db
db = sqlx.Open("sqlite3", ":memory:")

// From other db
db = sqlx.NewDb(sql.Open("sqlite3", ":memory:"), "sqlite3")

// Test connection
err = db.Ping()
```

**Подключение к БД:**

```Go
var err error

// Open and connect
db, err = sqlx.Connect("sqlite3", ":memory:")

db = sqlx.MustConnect("sqlite3", ":memory:")
```