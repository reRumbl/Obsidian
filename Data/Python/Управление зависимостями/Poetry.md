**Poetry** - это современный инструмент для управления зависимостями и упаковки проектов Python. Он предоставляет более продвинутый и удобный способ управления пакетами по сравнению с традиционным [[Pip|pip]], особенно в контексте современных [[Python|Python]]-проектов.

**Основные преимущества Poetry:**

- Автоматическое управление виртуальными средами.

- Улучшенный процесс разрешения зависимостей.

- Использование современного формата конфигурации pyproject.toml.

- Встроенная поддержка пакетирования проектов.

- Улучшенная производительность по сравнению с [[Pip|pip]].

![[Poetry.png]]

**Установка через pipx:**

```Shell
pipx install poetry
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
cd project-name
poetry init
```

### Конфигурация в pyproject.toml

```TOML
[tool.poetry]
name = "project-name"
version = "0.1.0"
description = ""

[tool.poetry.dependencies]
python = "^3.9"

[tool.poetry.dev-dependencies]
pytest = "^6.0"
```
