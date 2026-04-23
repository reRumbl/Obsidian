[[Rust|Rust]] поддерживает встроенные тесты.

**Пример теста:**

```Rust
#[cfg(test)]

mod tests {
    use main::is_even;

    #[test]
    fn test_is_even() {
        assert!(is_even(2));
        assert!(!is_even(3));
    }
}
```

**Запуск встроенных тестов:**

```Shell
cargo test
```