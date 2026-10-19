# F08 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `redirects`: from_path (уникальный), to_path, code (301), source (legacy | slug_change | manual), hits.
- SEO-поля у туров, категорий, подборок, страниц: title, description, h1, canonical, noindex.

## Правила
- Middleware Next.js: перед 404 проверяет `redirects`.
- Смена slug автоматически создаёт редирект, цепочки схлопываются (A→B→C ⇒ A→C).
- sitemap.xml генерируется по опубликованным сущностям; robots.txt; Schema.org `TouristTrip`/`Product`, `BreadcrumbList`.
- Trailing slash — как на старом сайте.

## Обязательные тесты
Все legacy URL из выгрузки отдают 200 или 301 (интеграционный тест по списку), отсутствие цепочек.

## Где в коде
TBD (`app/Modules/Content/Seo`, фронт `middleware.ts`).
