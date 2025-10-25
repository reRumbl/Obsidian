**Структура** — это коллекция полей, аналог классов без наследования.

```Go
type User struct {
	Name string
	Age int
	Email string `json:"email_address"`  // tag для JSON/ORM
}
```

