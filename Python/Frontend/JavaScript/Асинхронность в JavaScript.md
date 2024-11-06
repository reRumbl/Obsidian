[[JavaScript|JavaScript]] может выполнять действия асинхронно, например, запросы на сервер или ожидание таймера. Для этого используют `setTimeout` или `Promise`.

```JavaScript
console.log('Начало');

setTimeout(function() {
	console.log('Прошло 2 секунды');
}, 2000);

console.log('Конец');
```

*Примечание: Программа не блокируется ожиданием `setTimeout`, и сразу после запуска выводится "Конец".*

## Promise

**Promise** — это объект, представляющий результат асинхронной операции. **Promise** может быть выполнен успешно (resolved) или завершиться с ошибкой (rejected).

```JavaScript
let promise = new Promise(function(resolve, reject) {
	let success = true;
	if (success) {
		resolve('Операция выполнена успешно!');
	} else {
		reject('Ошибка операции.');
	}
});

promise
	.then(function(result) {
		console.log(result); // "Операция выполнена успешно!"
	})
	.catch(function(error) {
		console.log(error); // Если ошибка
	});

```

**Пример асинхронной операции проверки подписки пользователя на основе Promise:**

```JavaScript
let user = {  
    name: 'John',  
    age: 18,  
    subscribed: true,  
    getInfo: function() {  
        let result = ''  
        for (let key in this) {  
            result += key + ': '' + this[key] + ' ';  
        }  
        return result;  
    }  
}  
  
user.city = 'New York'  
  
function checkSubscription(user) {  
    return new Promise((resolve, reject) => {  
        if (user.subscribed === true) {  
            resolve('Подписка активна');  
        } else {  
            reject('Подписка неактивна');  
        }  
    });  
}  
  
checkSubscription(user)  
    .then(function(result) {  
        console.log(result);  
    })  
    .catch(function(error) {  
        console.log(error);  
    });
```

## Работа с несколькими Promise

**Promise.all** — позволяет запускать несколько **Promise** одновременно и ждать их завершения. Возвращает массив с результатами всех **Promise**, если они завершились успешно. Если хотя бы один завершился с ошибкой, весь `Promise.all` завершится с `reject`.

```JavaScript
let promise1 = Promise.resolve('Результат 1');
let promise2 = Promise.resolve('Результат 2');
let promise3 = Promise.resolve('Результат 3');

Promise.all([promise1, promise2, promise3])
    .then((results) => console.log(results)) // ['Результат 1', 'Результат 2', 'Результат 3']
    .catch((error) => console.error(error));
```

**Promise.race** — возвращает результат самого быстрого из **Promise**, будь то успешное завершение или ошибка.

```JavaScript
Promise.race([promise1, promise2, promise3])
    .then((result) => console.log(result)) // Выведет результат самого быстрого
    .catch((error) => console.error(error));
```

**Promise.allSettled** — возвращает результаты всех **Promise**, вне зависимости от того, завершились они успешно или с ошибкой. Полезно, если нужно обработать результат каждого **Promise**, даже если некоторые из них завершились с ошибкой.

```JavaScript
Promise.allSettled([promise1, promise2, promise3])
    .then((results) => console.log(results)); // Все результаты в любом случае
```

**Promise.any** — ждет первый успешно завершенный **Promise**. Если все **Promise** завершаются с ошибкой, тогда возвращает `reject` с `AggregateError`.

```JavaScript
Promise.any([promise1, promise2, promise3])
    .then((results) => console.log(results)); // Результат самого быстрого успешного
```

## Async / Await

**Асинхронные функции (`async`):** Ключевое слово `async` перед функцией делает её асинхронной, позволяя использовать внутри неё `await` для ожидания выполнения `Promise`. Асинхронная функция всегда возвращает `Promise`.

```JavaScript
async function fetchData() {
	return 'Данные получены!';
}

fetchData().then(result => console.log(result)); // 'Данные получены!'
```

**Асинхронное ожидание (`await`):** Ключевое слово `await` заставляет функцию ждать выполнения `Promise`, прежде чем перейти к следующей строке. Это позволяет писать асинхронный код в линейном стиле, что улучшает читаемость.

```JavaScript
async function fetchData() {
	let data = await new Promise((resolve) => {
		setTimeout(() => resolve('Данные получены!'), 2000);
	});
	console.log(data); // 'Данные получены!' через 2 секунды
}

fetchData();
```

**Обработка ошибок:** Ошибки в `async`-функциях можно перехватывать с помощью `try...catch`.

```JavaScript
async function fetchData() {
	try {
		let result = await somePromiseFunction();
		console.log(result);
	} catch (error) {
		console.log('Ошибка:', error);
	}
}
```



