**Linux:**

- `/var/log/auth.log` (или `/var/log/secure`) — Попытки входа.

- `/var/log/syslog` — Общие системные события.

- `/var/log/apache2/access.log` — Запросы к сайту (SQL-инъекции).

- `/var/log/suricata/eve.json` — Основной вывод алертов **Suricata**.

**Windows:**

- `C:\Windows\System32\winevt\Logs\Security.evtx` — Журнал безопасности.

- Логи **Sysmon** (в просмотре событий: _Applications and Services -> Microsoft -> Windows -> Sysmon_).