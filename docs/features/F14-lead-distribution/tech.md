# F14 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `sales_queues`: product_line, mode (manual | round_robin | weighted).
- `queue_members`: queue_id, user_id, active, base_weight.
- `manager_stats` (ежедневный пересчёт): user_id, period, leads, paid_orders, conversion, revenue, avg_first_response.
- `assignments`: order_id, user_id, assigned_at, reason (auto | manual | reassign), first_response_at.

## Правила
- На `OrderCreated` → выбор менеджера в очереди product_line по весу (с учётом активности; рабочие часы — Q-04).
- Конверсия = paid_orders / leads за период (определение «paid» — Q-05).
- Ручное переназначение — право `sales.assign`.

## Обязательные тесты
Распределение пропорционально весам (статистически), неактивные не получают, переназначение при блокировке.

## Где в коде
TBD (`app/Modules/Sales/Distribution`).
