**Poetry** - это современный инструмент для управления зависимостями и упаковки проектов Python. Он предоставляет более продвинутый и удобный способ управления пакетами по сравнению с традиционным [[Pip|pip]], особенно в контексте современных [[Python|Python]]-проектов.

**Основные преимущества Poetry:**

- Автоматическое управление виртуальными средами.

- Улучшенный процесс разрешения зависимостей.

- Использование современного формата конфигурации pyproject.toml.

- Встроенная поддержка пакетирования проектов.

- Улучшенная производительность по сравнению с [[Pip|pip]].

![[Poetry.png]]

**Установка через pip:**

```Shell
pip install poetry
```

**Установка через скрипт:**

```Shell
curl -sSL https://install.python-poetry.org | python3 -
```

## Основные возможности Poetry

### Создание проекта

**Создание нового проекта:**

```Shell
poetry new project-name
```

*При создании проекта автоматически будет выстроена следующая структура:*

```plaintext
project-name/
├── src/
│   └── project-name/
│       └── __init__.py
├── tests/
│   └── __init__.py
├── pyproject.toml
└── README.md
```

**Инициализация в существующем проекте:**

```Shell
poetry init
```

### Конфигурация в pyproject.toml

**Poetry** использует современный формат конфигурации pyproject.toml. 

**Пример pyproject.toml:**

```TOML
[tool.poetry]
name = "project-name"
version = "0.1.0"
description = "Very cool project with poetry"

[tool.poetry.dependencies]
python = "^3.12"

[tool.poetry.dev-dependencies]
pytest = "^6.0"
```

### Управление зависимостями

**Добавление зависимости:**

```Shell
poetry add packet-name
```

**Установка зависимостей из pyproject.toml:**

```Shell
poetry install
```

**Обновление всех зависимостей:**

```Shell
poetry update
```

Удаление зависимости:

```Shell
poetry remove packet-name
```

### Работа с виртуальным окружением

**Активация виртуального окружения:**

```Shell
poetry shell
```

**Запуск команд внутри окружения:**

```Shell
poetry run command-example
```

**Запуск [[Python|Python]]:**

```Shell
poetry run python
```

### Управление версиями в poetry.lock

**Poetry** автоматически создает файл poetry.lock для обеспечения повторяемости установки:

- При первом запуске `poetry install` создает poetry.lock.

- Файл содержит точные версии всех установленных пакетов.

- Рекомендуется коммитить poetry.lock в репозиторий.

- Для обновления версий используется `poetry update`.

## Лучшие практики

- Всегда использовать `poetry shell` для активации окружения.

- Коммитить poetry.lock в репозиторий.

- Использовать `poetry run` для запуска команд.

- Регулярно обновлять зависимости через `poetry update`.

- Следить за совместимостью версий [[Python|Python]] в проекте.

