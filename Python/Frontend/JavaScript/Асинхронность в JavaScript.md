[[JavaScript|JavaScript]] может выполнять действия асинхронно, например, запросы на сервер или ожидание таймера. Для этого используют `setTimeout` или `Promise`.

```JavaScript
console.log("Начало");

setTimeout(function() {
	console.log("Прошло 2 секунды");
}, 2000);

console.log("Конец");

```