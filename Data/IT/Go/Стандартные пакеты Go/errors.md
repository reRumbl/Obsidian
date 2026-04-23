
**Сопоставления ошибки при помощи `errors.As`:**

```Go
var jsonErr *json.SyntaxError

if err != nil {
	if errors.As(err, &jsonErr) {
		fmt.Println("JSON Syntax Error occurred!")
	} else {
		fmt.Println("A different error occurred: ", err)
	}
}
```