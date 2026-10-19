# F15 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `agencies`: название, ИНН/КПП, реквизиты, договор (номер, дата, файл), commission_default, status (requested | active | blocked).
- `agency_requests`: заявка на регистрацию с сайта.
- `commission_rules`: agency_id?, tour_id?, product_line?, percent (приоритет: агентство+тур > агентство > по умолчанию) — модель зависит от Q-03.

## Где в коде
TBD (`app/Modules/Sales/Agents`).
