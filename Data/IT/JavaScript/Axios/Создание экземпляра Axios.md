Для удобной работы с API в [[Axios|Axios]] можно создавать экземпляры.

**Пример создания экземпляра:**

```TypeScript
const instance = axios.create({
	baseURL: 'https://some-domain.com/api/',
	timeout: 1000,
	headers: {'X-Custom-Header': 'foobar'}
});
```

