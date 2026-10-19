# F21 — техническая документация
**Статус реализации:** не начато.
## Сущности
`rental_buses`: название, вместимость, фото, характеристики, published, порядок. Заявка — `orders` (product_line=bus_rental) + `order_items.type=bus_rental` с полями формы (даты, маршрут, кол-во человек, комментарий).
## Где в коде
TBD (`app/Modules/Products/BusRental`).
