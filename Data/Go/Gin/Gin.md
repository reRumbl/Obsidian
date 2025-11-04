**Gin** — это высокопроизводительный, минималистичный веб-фреймворк для [[Go|Go]], разработанный для создания RESTful API и микросервисов.

Установка:

```Shell
go get github.com/gin-gonic/gin
```

## Основные концепции

**Пример создания экзмепляра роутера:**

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