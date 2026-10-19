# F11 — техническая документация
**Статус реализации:** не начато.

## Сущности
- `document_types`: code (contract, voucher, booking_sheet, memo, invoice, act, offer, boarding_list…), name, applies_to (order | departure | corporate).
- `document_templates`: type_id, version, file (docx), status (draft | active | archived), created_by. Активна одна версия на тип (+ опционально на тур/продукт).
- `documents`: owner (order | departure), type_id, template_version_id?, version, pdf_path, data_snapshot (JSON), source (generated | uploaded), created_by, created_at. Записи не обновляются — только новые.

## Правила
- Генерация: снимок данных → docxtemplater-совместимый движок (PHP: PhpWord TemplateProcessor или docx-сервис) → Gotenberg → PDF в S3.
- Хеш PDF сохраняется, файл в хранилище неизменяем (write-once путь).
- Предпросмотр шаблона на тестовом заказе перед активацией.

## Обязательные тесты
Изменение шаблона не меняет старый документ; загрузка PDF создаёт новую версию; все поля шаблона заполняются.

## Где в коде
TBD (`app/Modules/Documents`).
