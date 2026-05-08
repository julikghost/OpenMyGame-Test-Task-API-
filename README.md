# OpenMyGame API Full Checks

Полный набор API-проверок в Postman для проекта OpenMyGame.

## Цель

- Проверить стабильность и контракт ключевых API.
- Подтвердить корректность поиска, фильтрации и синхронности данных.
- Проверить экспорт и базовые негативные HTTP-сценарии.

## Структура проверок

- `A. Smoke API Core`
  - `GET /api/kpis`
  - `GET /api/orders`
  - `GET /api/revenue-chart`
- `B. SMK-05 Search Cases (API)`
  - `GET /api/orders` с параметром `search`
- `C. SMK-08 Filters/Sync Cases (API)`
  - `GET /api/orders` с фильтрами `status`, `start_date`, `end_date`
  - SYNC-проверка согласованности `GET /api/orders` и `GET /api/kpis`
- `D. SMK-10 Export Cases (API)`
  - `GET /api/export` (формат, структура, фильтрация, стабильность)
- `E. Negative Contract / HTTP Basics`
  - `GET /api/orders` (некорректные параметры -> `422`)
  - `GET /api/unknown` -> `404`

## Покрытые endpoint'ы

- `GET /api/kpis`
- `GET /api/orders`
- `GET /api/revenue-chart`
- `GET /api/export`
- `GET /api/unknown`

## Known issues

- `GET /api/orders` (baseline): в ответе нет поля `data`, тест ожидает наличие `data`.
- `GET /api/export?status=completed`: экспорт содержит записи с другими статусами, не только `completed`.
- `GET /api/export?search=zzzz_not_found`: API возвращает данные вместо CSV только с header.
- `GET /api/orders?status=invalid_status_123`: API возвращает `200`, хотя негативный тест ожидает `422`.
