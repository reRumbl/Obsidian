При помощи Node.js можно легко сгенерировать секретный ключ в конcоли.

**Генерация ключа:**

```Shell
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```