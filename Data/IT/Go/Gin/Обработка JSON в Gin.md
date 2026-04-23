[[Gin|Gin]] использует процесс **binding** для автоматического парсинга и валидации тела запроса (JSON, XML и т. д.) в [[Go|Go]]-структуру.

```Go
type NewUser struct {
    Username string `json:"username" binding:"required"`
    Email    string `json:"email" binding:"required,email"`
}

router.POST("/users", func(c *gin.Context) {
    var newUser NewUser
    if err := c.ShouldBindJSON(&newUser); err != nil {
        c.JSON(400, gin.H{"error": err.Error()})
        return
    }
    c.JSON(200, newUser)
})
```
