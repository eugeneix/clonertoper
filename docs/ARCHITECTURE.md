# Архитектура (черновик, кода ещё нет)

## Стек (D-02)
| Слой | Технология | Комментарий |
|---|---|---|
| Бэкенд | Laravel (PHP 8.4) | Команда компании знает PHP |
| БД | PostgreSQL | Деньги и места — только транзакции и блокировки строк |
| Кэш/очереди | Redis + Laravel Horizon | Синхронизация круизов, SMS, документы, уведомления |
| Кабинеты сотрудников и агентов | Filament (2 панели: `/staff`, `/agent`) | Сложные экраны (схема салона, распределение) — свои компоненты |
| Права | spatie/laravel-permission | Права → роли → пользователи (D-07) |
| Витрина и ЛК | Next.js (React), SSR | Фронтендеры компании знают React; SEO |
| Реалтайм | Laravel Reverb (WebSocket) | Чат, живые места в салоне |
| Поиск | Meilisearch | Фильтры по датам, направлениям, ценам |
| Файлы | S3-совместимое хранилище (РФ) | Фото, отзывы, документы |
| Документы | Word-шаблоны → PDF через Gotenberg | Версии шаблонов, неизменяемые PDF (D-08) |
| Хостинг | Российское облако (Yandex Cloud / Selectel — Q-12) | 152-ФЗ |
| Инфраструктура | Terraform + Docker + GitHub Actions | Нет SSH из среды разработки (D-24) |

## Модули бэкенда (модульный монолит)
`Identity` (F01,F02) · `Catalog` (F03,F04,F05,F06,F07) · `Content` (F08,F28,F29,F30) · `Sales` (F09,F13,F14,F15,F16) ·
`Billing` (F10,F25) · `Documents` (F11) · `Communications` (F17,F18,F19) · `Products` (F20,F21,F22,F23) ·
`Finance` (F24,F26) · `Reviews` (F27) · `Loyalty` (F31) · `Platform` (F32,F33,F34).
Модули общаются через доменные события (например `OrderPaid`, `SeatReleased`), а не напрямую через таблицы друг друга.

## Ядро данных (черновик)
```
Tour ─< Departure ─< DepartureTrip >─ Trip(bus run) ── BusLayout ─< Seat
  │         │                                  └─< SeatAssignment >─ OrderTourist
  │         ├─< DepartureBoardingPoint ── BoardingPoint
  │         ├─< DepartureAccommodation ── Hotel / RoomType (квота)
  │         ├─< DepartureCostItem (план/факт)
  │         └─ PaymentScheme
  ├─< TourExtraService
  └─< TourPriceRule (дети, доплаты, скидки)

Order ─< OrderItem (type: own_tour | partner_tour | cruise | bus_rental | corporate | extra)
  ├─< OrderTourist
  ├─< PaymentScheduleItem
  ├─< Payment (online | cash | bank | refund | penalty)
  ├─< Document (version, immutable pdf + snapshot)
  ├─ channel, product_line, assignee (User), agency?
  └─< AuditLog
User (staff | agent | client) ─< roles/permissions
```
Деньги — целые копейки + код валюты (A-01). Все даты — в часовом поясе Europe/Moscow, хранение в UTC.

## Интеграции
| Сервис | Для чего | Функционал |
|---|---|---|
| sms.ru | Код по SMS и звонку | F01, F17 |
| SMTP / почтовый сервис | Код на почту, уведомления | F01, F17 |
| PayKeeper | Онлайн-оплата, чеки 54-ФЗ, возвраты | F10 |
| Инфофлот API | Круизы | F20 |
| Мостурфлот API | Круизы | F20 |
| Манго Офис API | Звонки → заявки, записи | F18 |
| MAX (бот-API) | Чат с клиентами | F19 |
| Производственный календарь | Праздники для схем оплаты | F10 |
| 1С | Бэклог | F25 |
| API партнёров | Бэклог | F23 |

## Окружения
- `local` — разработка в контейнере Claude (Docker Compose).
- `staging` — тестовый стенд для пользователя (домен — Q-13).
- `production` — боевой.
Деплой: push в `main` → тесты → деплой на staging; prod — по тегу/ручному запуску workflow.

## План на месяц (D-28) — подробно в PLAN.md
| Неделя | Что |
|---|---|
| 1 | Каркас, инфраструктура, F02, F01, F03, F04, F05 (конструктор схем), F06 |
| 2 | Выбор мест, F09, F10 (PayKeeper, схемы, график), F12, F11 |
| 3 | F13, F14 (ручное → авто), F20, F21, F22, F28, F29, F07, F08 |
| 4 | F24, F25, F27, F19, F18, F15, стабилизация, F32 перенос |
