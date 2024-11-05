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

```
