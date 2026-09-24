# PMP — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса PMP, вынесенные из `endpoints/PMP.md`. Сигнатуры и типы — там же и в `schemas/PMP.md`.

## FrequencyTypes

### `GET /FrequencyTypes`

## Пример запроса:
```text
GET /FrequencyTypes
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "code": "DAILY",
    "name": "Ежедневно"
  },
  "2": {
    "id": 2,
    "code": "WEEKLY",
    "name": "Еженедельно"
  }
}
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — типы повторений не найдены.

## ScheduledTasks

### `HEAD /ScheduledTasks`

## Пример запроса:
```text
HEAD /ScheduledTasks?assetID=501&dateRangeFrom=2026-08-01T00:00:00Z&dateRangeTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
Тело ответа отсутствует. В заголовке `Content-Range` возвращается общее количество записей в формате `items 0-0/{totalRowsCount}`.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные параметры фильтрации.

### `HEAD /ScheduledTasks/appointments`

## Пример запроса:
```text
HEAD /ScheduledTasks/appointments?assetID=501&dateRangeFrom=2026-08-01T00:00:00Z&dateRangeTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
Тело ответа отсутствует. В заголовке `Content-Range` возвращается общее количество записей в формате `items 0-0/{totalRowsCount}`.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — срабатывания по указанным фильтрам не найдены.
- 400 — некорректные параметры фильтрации.

### `GET /ScheduledTasks/count`

## Пример запроса:
```text
GET /ScheduledTasks/count?assetID=501&dateRangeFrom=2026-08-01T00:00:00Z&dateRangeTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "2026-08-20T00:00:00Z": [
    {
      "userID": 42,
      "countWithAssign": 3,
      "countWithoutAssign": 1
    },
    {
      "userID": 0,
      "countWithAssign": 0,
      "countWithoutAssign": 2
    }
  ]
}
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — данные по указанным фильтрам не найдены.
- 400 — некорректные параметры фильтрации.

### `GET /ScheduledTasks/v2/count`

## Пример запроса:
```text
GET /ScheduledTasks/v2/count?assetID=501&dateRangeFrom=2026-08-01T00:00:00Z&dateRangeTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "2026-08-20T00:00:00Z": [
    {
      "countTasksForDay": 5,
      "countTasksForUsers": [
        {
          "userID": 42,
          "countWithAssign": 3,
          "countWithoutAssign": 0
        },
        {
          "userID": 0,
          "countWithAssign": 0,
          "countWithoutAssign": 2
        }
      ]
    }
  ]
}
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — данные по указанным фильтрам не найдены.
- 400 — некорректные параметры фильтрации.

## Schedules

### `GET /Schedules/{id}`

## Пример запроса:
```text
GET /Schedules/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "frequencyType": {
    "id": 1,
    "name": "Ежедневно"
  },
  "options": {
    "interval": 1,
    "timeOfDay": "10:00:00"
  }
}
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — расписание с указанным идентификатором не найдено.
