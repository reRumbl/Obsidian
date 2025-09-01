В [[Rust|Rust]], как и в других языках, существуют базовые управляющие конструкции.

## If / Else

**Пример использования if/else:**

```Rust
if x > 5 {
    println!("Больше 5");
} else {
    println!("Меньше или равно 5");
}
```

## Циклы

В [[Rust|Rust]] существует три типа циклов: `loop`, `while` и `for`. `Loop` - бесконечный цикл, из которого можно выйти только при помощи `break` или завершения программы. `While` - цикл с условием. `For` - цикл с итерацией по коллекциям или диапазонам.

**Пример использования loop:**

```Rust
let counter = 0;

loop {
	println!("Hello");
	println!("Rust");
	counter += 1;
	
	if counter >= 5 {
		break;
	}
}
```

**Пример использования loop с записью в переменную:**

```Rust
let mut counter = 0;

let result = loop {
	counter += 1;
	
	if counter == 10 {
		break counter * 2;
	}
}
println!(result);  // 20
```

**Пример использования while:**

```Rust
let mut number = 3;   

while number != 0 {        
	println!("{}", number);
	number -= 1;
}
```

**Пример использования for:**

```Rust
for i in 0..5 {
    println!("{}", i);
}
```