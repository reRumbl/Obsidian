`this` — это особая переменная, которая ссылается на объект, в контексте которого выполняется текущая функция. Контекст зависит от того, как была вызвана функция.

**В методах объекта**: `this` ссылается на сам объект.

```JavaScript
const person = {
    name: 'John',
    greet: function() {
        console.log(this.name);
    }
};
person.greet(); // John
```

**В обычных функциях**: `this` ссылается на глобальный объект (в браузере это `window`).

```JavaScript
function showThis() {
    console.log(this); // window (в браузере)
}
showThis();
```

**В стрелочных функциях**: `this` в стрелочной функции не привязан к контексту вызова, он захватывается из окружающей области, в которой эта функция была создана.

```JavaScript
const obj = {
    name: 'Alice',
    showThis: () => console.log(this.name)
};
obj.showThis(); // undefined, так как this ссылается на глобальный объект
```

**Использование `bind`, `call`, `apply`**: можно явно задать, какой объект будет ассоциирован с `this`.

```JavaScript
const person = {
    name: 'Alice',
    greet: function() {
        console.log(this.name);
    }
};
const anotherPerson = { name: 'Bob' };
person.greet.call(anotherPerson); // Bob
```