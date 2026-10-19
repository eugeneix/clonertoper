# F12 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `client_travelers`: user_id, ФИО, дата рождения, документ (шифр.), телефон.
- Остальное — чтение из F09/F10/F11/F27.

## API
`GET /api/me/orders`, `GET /api/me/orders/{id}`, `POST /api/me/orders/{id}/pay` (ссылка PayKeeper), `GET /api/me/documents/{id}`, CRUD `/api/me/travelers`, `POST /api/me/reviews`.

## Правила
- Клиент видит только свои заказы (по user_id; гостевые привязываются при входе, F01).
- Документы отдаются по подписанной временной ссылке.

## Где в коде
Фронт `app/(cabinet)/lk`, бэк `app/Modules/Sales/ClientApi`.
