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

**Promise** — это объект, представляющий результат асинхронной операции. Промис может быть выполнен успешно (resolved) или завершиться с ошибкой (rejected).

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

**Пример асинхронной операции проверки подписки пользователя:**

```Python
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
