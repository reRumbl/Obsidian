В [[Textual|Textual]] все начинается с класса, который наследует от `textual.app.App`. Это главный компонент приложения. В нём определяется начальный layout, виджеты и логику. `App` содержит метод `compose`, он отвечает за сборку интерфейса из виджетов.

**Пример App:**

```Python
from textual.app import App, ComposeResult
from textual.widgets import Header, Footer, Static


class ExampleApp(App):
    def compose(self) -> ComposeResult:
        # Здесь определяются виджеты, которые будут в приложении
        yield Header()
        yield Static()
        yield Footer()


if __name__ == '__main__':
    app = ExampleApp()
    app.run()
```