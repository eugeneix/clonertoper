# F17 — техническая документация
**Статус реализации:** не начато.

## Сущности
`notification_templates` (event, channel, текст с переменными, active), `notification_log` (кому, канал, статус, ошибка).

## Технически
Laravel Notifications + очередь; каналы: mail, smsru, database (в интерфейсе сотрудника), позже max. Повторы при ошибке, лог доставки.

## Где в коде
TBD (`app/Modules/Communications/Notifications`).
