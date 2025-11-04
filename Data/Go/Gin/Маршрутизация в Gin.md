Маршрутизация в [[Gin|Gin]] происходит при помощи роутеров и хендлеров.

## Роутеры

**Роутер** - основа веб-приложения. Он включает в себя хендлеры для обработки маршрутов.

Создание роутера происходит при помощи `gin.Default()` (встроенные `Logger` и `Recovery`) или `gin.New()` (чистый роутер).

**Пример создания экземпляра роутера:**

```Go
package main

import "github.com/gin-gonic/gin"


func main() {
    // gin.Default() возвращает роутер с встроенными Middleware (Logger и Recovery)
    router := gin.Default() 

    // Определение маршрута GET
    router.GET("/hello", func(c *gin.Context) {
        // c.JSON - это метод для отправки JSON-ответа
        c.JSON(200, gin.H{
            "message": "Hello, Gin!",
        })
    })

    // Запуск сервера по умолчанию на :8080 (или через переменную окружения PORT)
    router.Run() 
}
```

## Хендлеры

**Хендлер** - функция, которая обрабатывает маршрут. Она принимает один аргумент: `*gin.Context`.

Для обработки параметров пути их следует указать в маршруте `/users/:id` и достать из контекста `c.Param("id")`.

**Пример создания хендлера:**

```Go
router.GET("/users/:id", func(c *gin.Context) {
	id := c.Param("id")
	c.JSON(200, gin.H{"user_id": id})
})
```

Примечание: `gin.H` - псевдоним для типа `map[string]interface`