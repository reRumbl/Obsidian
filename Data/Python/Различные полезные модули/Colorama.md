**Colorama** - это библиотека для [[Python|Python]], упрощающая раскрашивание и стилизацию строк в консольном выводе. По сути библиотека просто заменяет трудно читаемые последовательности, которые уже существуют в [[Python|Python]]. **Colorama** использует несколько классов для разных типов стилей:

- `Fore` - покраска самого текста.

- `Back` - покраска заднего фона текста.

- `Style` - стилизация текста.

**Пример покраски и стилизации выводимого текста:**

```Python
from colorama import Fore, Back, Style

print(Fore.RED + 'some red text')
print(Back.GREEN + 'and with a green background')
print(Style.DIM + 'and in dim text')
print(Style.RESET_ALL)
print('back to normal now')
```