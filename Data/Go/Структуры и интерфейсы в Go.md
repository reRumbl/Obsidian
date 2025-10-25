**Структура** — это коллекция полей, аналог классов без наследования.

**Пример структуры:**

```Go
type User struct {
	Name string
	Age int
	Email string `json:"email_address"`  // tag для JSON/ORM
}
```

**Пример методов структуры:**

```Go
func (u User) GetInfo() string {
	return fmt.Sprintf("%s (%d)", u.Name, u.Age)
}


func (u *User) IncreaseAge() 
```