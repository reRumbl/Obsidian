Работа с запросами в [[sqlx|sqlx]] осуществляется похожим образом со стандартным пакетом [[Go/Стандартные пакеты Go/database/sql|database/sql]].

## Exec

**Exec** позволяет выполнить любой SQL запрос (не возвращает результат). Его аналог MustExec вы

**Пример Exec:**

```Go
schema := `CREATE TABLE place (
	country text,
	city text NULL,
	telcode integer);`

result, err := db.Exec(schema)

// MustExec
cityState := `INSERT INTO place (country, telcode) VALUES (?, ?)`
db.MustExec(cityState, "Hong Kong", 852)
```