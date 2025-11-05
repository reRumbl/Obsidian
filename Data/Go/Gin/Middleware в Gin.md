[[Gin|Gin]] имеет мощную систему middleware.

**Пример middleware:**

```Go
func AuthMiddleware() gin.HandlerFunc {
    return func(c *gin.Context) {
        token := c.GetHeader("Authorization")
        if token != "valid-token" {
            c.AbortWithStatusJSON(401, gin.H{"error": "Unauthorized"}) // Прерывает выполнение
            return
        }
        c.Next() // Переходит к следующему хендлеру/middleware
    }
}

// Применение middleware
router.GET("/protected", AuthMiddleware(), func(c *gin.Context) {
    c.JSON(200, gin.H{"message": "Access granted"})
})
```