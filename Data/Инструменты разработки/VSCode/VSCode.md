**VSCode** - это редактор исходного кода, разработанный Microsoft для Windows, [[Linux|Linux]] и macOS. Позиционируется как «лёгкий» редактор кода для кроссплатформенной разработки веб- и облачных приложений.

**Стандартный `settings.json` для [[Python|Python]] проекта:**

```JSON
{
    "python.envFile": "${workspaceFolder}/.env",
    "python.analysis.extraPaths": [
        "./"
    ],
    "python.testing.pytestArgs": [
        "tests"
    ],
    "python.testing.unittestEnabled": false,
    "python.testing.pytestEnabled": true
}
```
