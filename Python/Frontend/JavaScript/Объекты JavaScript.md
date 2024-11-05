**Объект** — это коллекция свойств, где каждое свойство имеет имя и значение. Свойства объекта могут хранить значения любого типа, включая массивы и другие объекты.

```JavaScript
let person = {
  name: 'Alice',
  age: 25,
  subscribed: true
};

console.log(person.name); // "Alice"
console.log(person['age']); // 25
```

Чтобы добавить новое свойство или изменить существующее, можно обратиться к объекту с использованием точки или квадратных скобок.

```JavaScript
person.city = 'New York'; // Добавляем новое свойство
person.age = 26; // Изменяем существующее свойство
```

Объекты могут содержать функции в качестве свойств, которые называются методами.

```JavaScript
let person = {
  name: 'Bob',
  greet: function() {
    console.log('Hello, ' + this.name);
  }
};

person.greet(); // "Hello, Bob"
```

*Примечание: Ключевое слово `this` ссылается на сам объект, в котором находится.*

## Деструктуризация объектов

**Деструктуризация объектов:** позволяет извлекать свойства объекта в отдельные переменные.

```JavaScript
let user = { name: 'Alice', age: 25, city: 'New York' };
let { name, age, city } = user;

console.log(name); // 'Alice'
console.log(age);  // 25
console.log(city); // 'New York'
```

**Значения по умолчанию:** При деструктуризации можно задавать значения по умолчанию.

```JavaScript
let person = { name: 'Bob' };
let { name, age = 30 } = person;

console.log(age); // 30
```