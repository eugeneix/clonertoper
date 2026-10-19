# F03 — техническая документация
**Статус реализации:** не начато.

## Сущности (черновик)
- `tours`: title, slug, legacy_id, type, duration_days, has_transport, description/program (блоки), gallery, categories, tags, weight, status (draft|published|archived), payment_scheme_id, min_group_size, is_partner, partner_id.
- `tour_program_days`: день, заголовок, текст.
- `departures`: tour_id, start_date, end_date, status (open|closed|cancelled|completed), seat_quota (если без транспорта), is_holiday (ручная отметка, A-03).
- `boarding_points` (справочник) + `departure_boarding_points`: время, доплата/скидка.
- `tour_extra_services`: название, цена, обязательная/опциональная, за человека/за заказ.

## Правила
- Свободные места выезда = сумма свободных мест его рейсов (F05) или quota − занятые (без транспорта).
- Нельзя удалить выезд с заказами — только закрыть/отменить.
- Смена slug создаёт редирект (F08).
- Копирование тура/выезда — со всеми правилами, без заказов.

## События
`DepartureCreated`, `DepartureCancelled`, `TourPublished`, `TourSlugChanged`.

## Обязательные тесты
Подсчёт свободных мест, копирование, запрет удаления с заказами, редирект при смене slug.

## Где в коде
TBD (`app/Modules/Catalog/Tours`).
