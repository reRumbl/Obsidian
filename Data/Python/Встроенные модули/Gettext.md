**Gettext** - это встроенный модуль [[Python|Python]] для упрощения интернационализации и локализации приложений.

**Подключение в проект:**

```Python
import gettext
```

## Работа с gettext

**Для работы с gettext требуется:**

- Определиться со списком языков.

- Создать словарь с ключами из выбранных языков.

- Определить функцию, которая будет транслировать текст, переданный ей, на соответствующий язык.

**Стандартный код для работы с gettext:**

```Python
import gettext

LANGUAGES = ['ru', 'en']

translations = {
	lang: gettext.translation(
		'messages', localedir='translations', languages=[lang]
	)
	for lang in LANGUAGES
}


def get_translator(lang: str):
	return translations.get(lang, translations.get('en'))



```
