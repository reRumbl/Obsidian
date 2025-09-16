В [[Textual|Textual]] все начинается с класса, который наследует от `textual.app.App`. Это главный компонент приложения. В нём определяется начальный layout, виджеты и логику.

Пример App:

```Python
from textual.app import App, ComposeResult
from textual.widgets import Header, Footer, Static


class ExampleApp(App):
    def compose(self) -> ComposeResult:
        # Здесь определяются виджеты, которые будут в приложении
        yield Header()
        yield Static('Здесь будет информация о системе')
        yield Footer()


if __name__ == '__main__':
    app = MyMonitorApp()
    app.run()
```