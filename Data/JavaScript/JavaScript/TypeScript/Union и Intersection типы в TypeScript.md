Для объединения типов в [[TypeScript|TypeScript]] существуют **Union** и **Intersection**. Они позволяют задать несколько возможных типов для одной переменной.

## Union типы

**Особенности Union типов:**

- Позволяют объединить несколько типов в один.

- Используется вертикальная черта | для разделения типов.

- Описывает значение, которое может быть одним из нескольких типов.

```TypeScript
type StringOrNumber = string | number;

let bigNum: StringOrNumber = 1234567890;
bigNum = '14882281337093';
```

## Intersection типы

**Особенности Intersection типов:**

- Объединяют несколько [[Интерфейсы в TypeScript|интерфейсов]] в один более специфичный тип.

- Используется амперсанд & для объединения типов.

- Создает новый тип, который включает все свойства всех объединяемых типов.

```TypeScript
interface Animal {
	name: string;
}

interface Dog {
	breed: string;
}

type DogWithName = Animal & Dog; // { name: string; breed: string; }

let dog: DogWithName = {
	name: 'Шарик',
	breed: 'Немецкая овчарка'
}
```