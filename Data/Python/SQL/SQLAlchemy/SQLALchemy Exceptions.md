Исключения, возникающие при работе с [[SQLAlchemy|SQLAlchemy]].

## Сессия

### A transaction is already begun on this Session

Возникает, когда встречается лишний `.begun()` или `.commit()`.

### Instance is not persistent within this Session

Возникает, когда вызывается `.refresh()` до `.commit()` или второй вовсе не вызывается.


