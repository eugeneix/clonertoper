# F06 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `price_rules`: scope (tour | departure | accommodation | boarding_point | extra_service), kind (base | surcharge | discount | child | single_supplement | markup), amount | percent, conditions (JSON: возраст, тип номера, даты), priority.
- `money`: integer minor units + currency (RUB по умолчанию).

## Сервис
`PriceCalculator::quote(departure, tourists[], accommodation, boarding, extras) → Quote` с построчной расшифровкой (line items). Quote сохраняется в заказ целиком (снимок).

## Правила
- Порядок применения: база → размещение → SGL → точка посадки → детские → скидки тура → доп. услуги → ручная корректировка.
- Округление до рубля по итогам строки.
- Ручная корректировка хранит было/стало/кто/причину.

## Обязательные тесты
Таблица кейсов: взрослый, ребёнок по возрастам, SGL, посадка с доплатой, скидка %, комбинации, партнёрская наценка.

## Где в коде
TBD (`app/Modules/Catalog/Pricing`).
