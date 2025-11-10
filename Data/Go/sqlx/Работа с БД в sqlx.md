Работа с БД в [[sqlx|sqlx]] осуществляется похожим образом со стандартным пакетом [[Go/Стандартные пакеты Go/database/sql|database/sql]].

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

// Open and connect, panic on error
db = sqlx.MustConnect("sqlite3", ":memory:")
```