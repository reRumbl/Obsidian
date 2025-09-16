Реактивные переменные - это одна из самых мощных фишек [[Textual|Textual]]. Если нужно, чтобы при изменении переменной обновлялся и интерфейс, просто требуется пометить её как **реактивную**. Это избавляет от необходимости вручную обновлять виджеты.

```Python
from textual.app import App, ComposeResult
from textual.widgets import Header, Static
from textual import on
import psutil


class SystemMonitor(App):

    CPU_USAGE = 0.0 # Обычная переменная
    cpu_usage: float = 0.0 # Реактивная переменная

    def on_mount(self):
        self.set_interval(1, self.update_data)

    def update_data(self):
        self.cpu_usage = psutil.cpu_percent() # Обновляем реактивную переменную

    def compose(self) -> ComposeResult:
        yield Header()
        yield Static(f'Использование CPU: {self.cpu_usage:.2f}%')
```