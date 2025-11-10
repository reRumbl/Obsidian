Работа с запросами в [[sqlx|sqlx]] осуществляется похожим образом со стандартным пакетом [[Go/Стандартные пакеты Go/database/sql|database/sql]].

## Exec

`Exec` позволяет выполнить любой SQL запрос (не возвращает результат). Его аналог `MustExec` работает также, но вызывает панику при ошибке.

**Пример Exec:**

```Go
schema := `CREATE TABLE place (
	country text,
	city text NULL,
	telcode integer);`
result, err := db.Exec(schema)
```

**Пример MustExec:**

```Go
cityState := `INSERT INTO place (country, telcode) VALUES (?, ?)`
db.MustExec(cityState, "Hong Kong", 852)
```

## Bindvars

Для подстановки значений в запрос используются **bindvars**. В MySQL это символы `?`, в PostgreSQL это `$1`, `$2` и т.д. SQLite принимает оба варианта.