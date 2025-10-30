[[Next.js|Next.js]] позволяет создавать собственный бэкенд прямо в приложении. Можно обрабатывать [[Cеть/Сетевые протоколы/HTTP/HTTP|HTTP]]-запросы (GET, POST, PUT, DELETE) и возвращать JSON-данные. Это очень удобно для создания API для фронтенда, поскольку можно использовать те же технологии.

Для построения API маршрута нужно сделать папку `api` в директории `app`, а внутри неё — папки для самих маршрутов. Например, `app/api/products`. Внутри папки создается файл `route.js` или `route.ts`. Этот файл будет содержать функции-обработчики для каждого [[Cеть/Сетевые протоколы/HTTP/HTTP|HTTP]]-метода.

**Пример API-маршрута:**

```TypeScript
// app/api/products/route.ts

export async function GET(request) {
	const products = [
		{ id: 1, name: 'Ноутбук' },
		{ id: 2, name: 'Мышь' },
		{ id: 3, name: 'Клавиатура' },
	];
	
	return new Response(JSON.stringify(products), {
		headers: { 'Content-Type': 'application/json' },
	});
}
```

