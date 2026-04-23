**Babel** - это библиотека для [[Python|Python]] предоставляющая удобные готовые инструменты для локализации и интернационализации. Она также предоставляет набор команд для генерации файлов перевода.

**Установка через cmd или terminal:**

```Shell
pip install babel
```

**Подключение в проект:**

```Python
import babel
```

## CLI команды

**Сбор всех переводимых сообщений из указанных файлов в `messages.pot`:**

```Shell
pybabel extract -o translations/messages.pot src/*
```

**Создание папок с переводами для указанного языка на основе `messages.pot`:**

```Python
pybabel init -i translations/messages.pot -d translations -l en
```

**Компиляция файлов `.po` в `.mo`:**

```Python
pybabel compile -d translations
```
