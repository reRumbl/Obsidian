**Структура** — это коллекция полей, аналог классов без наследования.

**Пример структуры:**

```Go
type User struct {
	Name string
	Age int
	Email string `json:"email_address"`  // tag для JSON/ORM
}
```

**Методы** - функции, привязанные к структуре через получателя.

**Пример методов структуры:**

*Метод, который не изменяет значение структуры:*

```Go
func (u User) GetInfo() string {
	return fmt.Sprintf("%s (%d)", u.Name, u.Age)
}
```

*Метод, который изменяет структуру:*

```Go
func (u *User) IncreaseAge() {
	u.Age += 1
}
```

## Интерфейсы

**Интерфейс** - это набор сигнатур методов.

```Go
type Sharable
```