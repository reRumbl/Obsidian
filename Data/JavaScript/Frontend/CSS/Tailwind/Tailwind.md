**Tailwind CSS** - это современный утилитарный фреймворк для стилизации веб-проектов, который позволяет создавать дизайн прямо в [[HTML|HTML]] с помощью специальных классов.

## Синтаксис Tailwind

**Пример:**

```HTML
<!DOCTYPE html>
<html>
<head>
	<script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 min-h-screen p-8">
	<!-- Простая кнопка -->
	<button class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700 transition-colors">
		Нажми меня!
	</button>

	<!-- Карточка с информацией -->
	<div class="mt-8 bg-white rounded-lg shadow-md p-6 max-w-sm mx-auto">
		<h2 class="text-xl font-bold mb-2">Привет!</h2>
		<p class="text-gray-600">Это пример карточки с Tailwind.</p>
	</div>

	<!-- Адаптивный контейнер -->
	<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mt-8">
		<div class="bg-red-200 p-4 rounded">Колонка 1</div>
		<div class="bg-green-200 p-4 rounded">Колонка 2</div>
		<div class="bg-blue-200 p-4 rounded">Колонка 3</div>
	</div>
</body>
</html>
```

*Исходя из примера:*

- Каждый класс отвечает за одно CSS-свойство. Например, `bg-blue-500` устанавливает синий фон, а `px-4` добавляет отступ по горизонтали.

- Классы можно комбинировать для создания сложных стилей.

- Суффиксы `hover:` позволяют определять состояния при наведении.

- Префиксы `md:` и `lg:` делают стили адаптивными.

## Основные преимущества

