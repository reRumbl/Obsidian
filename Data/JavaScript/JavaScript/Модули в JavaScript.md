Модули позволяют структурировать код и делать его более организованным и читаемым, разделяя его на отдельные файлы с определёнными функциональными частями. В современном [[JavaScript|JavaScript]] модули можно подключать и экспортировать с помощью `export` и `import`.

**Экспортирование**: Чтобы сделать функцию, класс или переменную доступными для других файлов, нужно их экспортировать.

```JavaScript
// В файле user.js
export class User {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}

export function greet(user) {
    console.log(`Привет, ${user.name}!`);
}
```

**Импортирование**: Импорт позволяет получить экспортированные сущности из других файлов. Синтаксис `import { ... } from` указывает, какие объекты или функции импортировать и откуда.

```JavaScript
// В другом файле main.js
import { User, greet } from './user.js';

let user = new User('Alice', 25);
greet(user); // 'Привет, Alice!'
```

**Экспорт по умолчанию**: Можно использовать `export default`, чтобы экспортировать один основной объект, класс или функцию из модуля, который затем можно импортировать под любым именем.

```JavaScript
// В файле logger.js
export default function log(message) {
    console.log('Log:', message);
}
```

```JavaScript
// В main.js
import log from './logger.js';

log('Это сообщение'); // "Log: Это сообщение"
```