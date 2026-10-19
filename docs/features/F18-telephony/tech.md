# F18 — техническая документация
**Статус реализации:** не начато.

## Сущности
`calls`: external_id, direction, from, to, user_id (сотрудник), order_id?, client_id?, started_at, duration, recording_url, status.

## Интеграции
Манго Офис VPBX API: вебхуки событий звонка (подпись sha256(key+json+salt)), запрос записи, click-to-call. Env `MANGO_API_KEY`, `MANGO_API_SALT`.

## Обязательные тесты
Проверка подписи, дедупликация событий, создание заявки vs привязка к существующему заказу.

## Где в коде
TBD (`app/Modules/Communications/Telephony`).
