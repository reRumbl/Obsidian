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


