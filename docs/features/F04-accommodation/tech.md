# F04 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `hotels` (справочник): название, город, звёзды, описание, фото.
- `room_types`: code (SGL, DBL, TWIN, TRPL…), capacity, allows_extra_bed.
- `departure_accommodations`: departure_id, hotel_id, room_type_id, rooms_quota, price rules (через F06).
- `order_rooms`: order_id, departure_accommodation_id, extra_bed, sharing_wanted (подселение), paired_order_room_id.
- Туристы заказа ссылаются на `order_rooms`.

## Правила
- Резерв номера — транзакция с блокировкой строки квоты; занятые = count(order_rooms активных заказов).
- Туристов в номере ≤ capacity (+1 при доп. месте).
- Аннуляция/перенос освобождает номер.

## Обязательные тесты
Гонка двух заказов на последний номер; переполнение номера; освобождение при аннуляции.

## Где в коде
TBD (`app/Modules/Catalog/Accommodation`).
