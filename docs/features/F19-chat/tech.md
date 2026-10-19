# F19 — техническая документация
**Статус реализации:** не начато.
## Сущности
`conversations` (channel: site | max, client, order?, assignee, status), `messages` (author, body, attachments, read_at).
## Технически
Reverb WebSocket для сайта; MAX — вебхук бота + отправка через API (env `MAX_BOT_TOKEN`). Рабочие часы и автоответ — настройки.
## Где в коде
TBD (`app/Modules/Communications/Chat`).
