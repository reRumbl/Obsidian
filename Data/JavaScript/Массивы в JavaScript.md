**Массив** - тип данных, позволяющий хранить несколько объектов любого типа внутри одной переменной.

Массивы позволяют хранить несколько элементов в одной переменной.

```JavaScript
let fruits = ['apple', 'banana', 'orange'];

console.log(fruits[0]); // 'apple'
console.log(fruits.length); // 3
```

Добавить элемент в массив можно с помощью метода `push()`:

```JavaScript
fruits.push('grape'); // Добавит 'grape' в конец массива
```

Пройтись по элементам массива можно с помощью цикла `for`:

```JavaScript
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

Массивы можно деструктуризировать:

```JavaScript
let colors = ['red', 'green', 'blue'];
let [firstColor, secondColor] = colors;

console.log(firstColor); // 'red'
console.log(secondColor); // 'green'
```

## Методы массивов

**Метод `map`** — создаёт новый массив, преобразуя каждый элемент исходного массива с помощью переданной функции.

```JavaScript
let numbers = [1, 2, 3];
let squares = numbers.map(x => x * x);
console.log(squares); // [1, 4, 9]
```

**Метод `filter`** — создаёт новый массив только из тех элементов, которые соответствуют условию.

```JavaScript
let numbers = [1, 2, 3, 4];
let evens = numbers.filter(x => x % 2 === 0);
console.log(evens); // [2, 4]
```

**Метод `find`** — возвращает первый элемент массива, который соответствует условию. Если элемент не найден, возвращает `undefined`.

```JavaScript
let users = [{ name: 'Alice' }, { name: 'Bob' }];
let user = users.find(user => user.name === 'Bob');
console.log(user); // { name: 'Bob' }
```

**Метод `reduce`** — применяет функцию к каждому элементу массива, сохраняя промежуточный результат (аккумулятор) и возвращая итоговое значение.

```JavaScript
let numbers = [1, 2, 3, 4];
let sum = numbers.reduce((acc, x) => acc + x, 0);
console.log(sum); // 10
```
