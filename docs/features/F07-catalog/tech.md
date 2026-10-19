# F07 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `categories` (дерево): slug, title, seo-поля, порядок.
- `collections` (подборки): type (manual | rule), правило (теги, период дат, категория), slug, seo.
- Индекс Meilisearch `tours`: id, title, categories, tags, duration, departure_city, has_transport, next_dates, price_from, weight, seats_left.

## Правила
- Сортировка по умолчанию: weight desc, затем ближайшая дата.
- Индекс обновляется событиями (`TourPublished`, `DepartureChanged`, места/цены) через очередь.
- Страницы рендерятся на сервере (Next.js SSR/ISR) для SEO.

## API
`GET /api/catalog/tours?filters`, `GET /api/catalog/tours/{slug}`, `GET /api/catalog/categories/{slug}`, `GET /api/catalog/collections/{slug}`.

## Обязательные тесты
Фильтры, сортировка по весу, скрытие неопубликованных, переиндексация при изменении мест.

## Где в коде
TBD (`app/Modules/Catalog/Storefront`, фронт `app/(storefront)`).
