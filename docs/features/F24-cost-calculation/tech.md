# F24 — техническая документация
**Статус реализации:** не начато.
## Сущности
`cost_templates` (на тур), `departure_cost_items`: category (transport | hotel | guide | excursion | meals | other), basis (per_group | per_person | per_room), planned_amount, actual_amount, comment, currency.
## Расчёты
Плановая себестоимость при N туристах; break-even N = fixed / (avg_price − variable_per_person); маржа = выручка − себестоимость (план и факт).
## Где в коде
TBD (`app/Modules/Finance/Costing`).
