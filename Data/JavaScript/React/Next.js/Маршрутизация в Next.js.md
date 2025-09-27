В [[Next.js|Next.js]] маршрутизация работает на основе `App Router`. Все маршруты определяются с помощью папок внутри директории `app`.

- Каждая папка в `app` представляет собой сегмент маршрута.

- Внутри каждой папки должен быть файл `page.js` или `page.jsx` — это и есть страница, которая будет отображаться по соответствующему маршруту.

**Пример:**

- `app/page.js` -> `/` (домашняя страница)

- `app/about/page.js` -> `/about` (страница "О нас")

- `app/blog/page.js` -> `/blog` (страница блога)

## Динамические маршруты

В реальных приложениях часто нужны страницы, которые отображают контент в зависимости от параметра в URL. Например, `/products/123` или `/blog/nextjs-basics`. [[Next.js|Next.js]] решает эту задачу с помощью динамических сегментов маршрута. 

Чтобы создать динамический маршрут, используются квадратные скобки `[]` в имени папки. В компоненте страницы можно получить доступ к параметрам URL через объект `params`, который передаётся в компонент как свойство.

**Пример компонента с динамическим маршрутом:**

```TypeScript
// app/products/[id]/page.js (Server Component)

async function getProduct(id) {
	const res = await fetch(`https://api.example.com/products/${id}`);
	return res.json();
}


export default async function ProductPage({ params }) {
	const product = await getProduct(params.id);
	
	if (!product) {
		return <div>Продукт не найден</div>;
	}
	
	return (
		<div>
			<h1>{product.name}</h1>
			<p>{product.description}</p>
			<p>Цена: {product.price}</p>
		</div>
	);
}
```
