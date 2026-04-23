
## Timer 

Для использования таймера в [[Slint|Slint]] существует структура `Timer`. Также нужно использовать перечисление `TimerMode`, чтобы указать режим таймера и `Duration` из `std::time`, чтобы указать интервал таймера. После всего этого указывается `callback` функция.

```Rust
use slint::{Timer, TimerMode};
use std::time::Duration;

let timer = Timer::default();
timer.start(TimerMode::Repeated, Duration::from_secs(1), some_callback_fn)
```