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

Для подстановки значений в запрос используются **bindvars** (они предотвращают SQL-инъекции). В MySQL это символы `?`, в [[PostgreSQL|PostgreSQL]] это `$1`, `$2` и т.д. [[SQLite|SQLite]] принимает оба варианта. Можно использовать функцию `sqlx.DB.Rebind(string) string` с `?` для получения запроса, который подойдет для используемой БД.

## Query

`Query` является основным способом выполнять запросы к БД (возвращает результат).

```Go
rows, err := db.Query("SELECT country, city, telcode FROM place")

for rows.Next() {
	var country string
	var city    sql.NullString
	var telcode int
	err = rows.Scan(&country, &city, &telcode)
}

err = rows.Err()
```