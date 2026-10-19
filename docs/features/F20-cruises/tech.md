# F20 — техническая документация
**Статус реализации:** не начато.
## Сущности
`cruise_providers` (infoflot, mosturflot), `ships` (provider, external_id, название, фото, описание, палубы), `cabin_categories`, `cruises` (ship, маршрут, даты, порты), `cruise_prices` (cruise, cabin_category, price, available), `sync_runs` (лог).
## Технически
Ночная задача (cron 03:00 МСК) на каждого провайдера: загрузка → upsert по external_id → снятие с публикации исчезнувших → переиндексация. Ошибка синхронизации → алерт, витрина остаётся со вчерашними данными.
Env: `INFOFLOT_API_KEY`, `MOSTURFLOT_API_KEY` (имена уточню по документации API).
## Обязательные тесты
Upsert, исчезновение круиза, частичный сбой одного провайдера.
## Где в коде
TBD (`app/Modules/Products/Cruises`).
