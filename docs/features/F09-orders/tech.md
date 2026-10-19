# F09 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `orders`: number (человекочитаемый), status, channel (site | phone | chat | max | agent | corporate | manual), product_line (tours | cruises | bus_rental | corporate), client_user_id, contact (имя, телефон, почта), assignee_id, agency_id, total (снимок), currency, payment_scheme_id, notes, source_meta (UTM, звонок, чат).
- `order_items`: type (own_tour | partner_tour | cruise | bus_rental | corporate | extra), ref (departure_id / cruise_offer_id / …), price_snapshot (JSON Quote), qty.
- `order_tourists`: ФИО, дата рождения, документ (шифруется), телефон, категория (adult | child), seat (F05), room (F04).
- `order_status_history`.

## Статусная модель (черновик)
`new` → `in_progress` → `booked` → `partially_paid` → `paid` → `completed`
любое → `cancelled` (вручную, с причиной); `booked` → `transferred` (перенос, создаёт связь со новым выездом).

## Правила
- Создание брони — одна транзакция: места + номера + заказ.
- Цены — снимок (F06), не пересчитываются при изменении тура; пересчёт — только явным действием менеджера.
- Паспортные данные шифруются на уровне приложения (152-ФЗ).

## События
`OrderCreated`, `OrderAssigned`, `OrderBooked`, `OrderPaid`, `OrderCancelled`, `OrderTransferred`.

## Обязательные тесты
Создание с гонкой за места, перенос с оплатами, аннуляция освобождает места/номера, снимок цены.

## Где в коде
TBD (`app/Modules/Sales/Orders`).
