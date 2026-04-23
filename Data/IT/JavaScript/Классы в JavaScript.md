**Создание класса:** Классы определяются с помощью ключевого слова `class`, а метод `constructor` отвечает за инициализацию свойств при создании экземпляра.

```JavaScript
class Person {
    constructor(name, age, city) {
        this.name = name;
        this.age = age;
        this.city = city;
    }
    
    introduce() {
        return `Привет! Меня зовут ${this.name}, мне ${this.age} лет и я из города ${this.city}.`;
    }
}

let person1 = new Person('Alice', 25, 'London');
console.log(person1.introduce());
```

**Наследование:** С помощью ключевого слова `extends` можно создавать дочерние классы. Метод `super` позволяет вызывать конструктор родительского класса.

```JavaScript
class Student extends Person {
    constructor(name, age, city, course) {
        super(name, age, city);
        this.course = course;
    }

    introduce() {
        return `${super.introduce()} Я учусь на курсе ${this.course}.`;
    }
}

let student1 = new Student('Bob', 20, 'Paris', 'Computer Science');
console.log(student1.introduce());
```