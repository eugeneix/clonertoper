# F10 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `payment_schemes`: code, name, rules (JSON: [{percent, due: "on_booking"} , {rest, due_days_before_start, holiday_due_days}]).
- `payment_schedule_items`: order_id, amount, due_date, status (pending | paid | overdue | waived), manual (bool).
- `payments`: order_id, method (paykeeper | cash | bank_transfer | other), direction (in | refund), amount, status, external_id, receipt (54-ФЗ), created_by, paid_at.
- `penalties`: order_id, amount, reason, created_by.
- `holidays`: date, kind (holiday | shortened | manual), source.

## Правила
- График строится при брони по схеме тура и дате начала; holiday = departure.is_holiday OR start_date ∈ holidays.
- Если today > due_date доплаты → один платёж 100%.
- Оплата распределяется по графику по порядку дат.
- PayKeeper: создание счёта → ссылка; callback с проверкой подписи; идемпотентность по external_id; ночная сверка.
- Ручная оплата требует права `billing.payments.create_manual`, пишет в журнал.

## Интеграции
PayKeeper (env `PAYKEEPER_URL`, `PAYKEEPER_USER`, `PAYKEEPER_PASSWORD`, `PAYKEEPER_SECRET`); производственный календарь (загрузка раз в год + ручная правка).

## Обязательные тесты
Построение графика для А/Б/В, праздник → 21 день, поздняя бронь → 100%, повторный callback, частичная оплата, ручной возврат.

## Где в коде
TBD (`app/Modules/Billing`).
