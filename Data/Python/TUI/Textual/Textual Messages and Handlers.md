Когда в [[Textual|Textual]] приложении что-то происходит (нажатие кнопки, изменение поля ввода), генерируется **сообщение**. Можно определить **обработчик**, который будет реагировать на эти сообщения. Это похоже на систему событий.

**Пример обработки нажатия кнопки:**

```Python
from textual.app import App, ComposeResult
from textual.widgets import Button
from textual import on


class MyButtonApp(App):
    def compose(self) -> ComposeResult:
        yield Button('Нажми меня!', id='my_button')

    @on(Button.Pressed, '#my_button')
    def on_button_pressed(self, event: Button.Pressed):
        self.log('Кнопка была нажата!')
```