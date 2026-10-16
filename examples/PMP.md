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

### `GET /ScheduledTasks`

## Пример запроса:
```text
GET /ScheduledTasks?assetID=501&scheduleID=1&dateRangeFrom=2026-08-01T00:00:00Z&dateRangeTill=2026-08-31T23:59:59Z&isAssigned=false
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "taskTemplateID": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Плановое ТО насоса",
    "description": "Ежемесячное техническое обслуживание",
    "notes": "Проверить давление",
    "sortOrder": 0
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — плановые заявки по указанным фильтрам не найдены.
- 400 — некорректные параметры фильтрации.

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

### `GET /ScheduledTasks/appointments`

## Пример запроса:
```text
GET /ScheduledTasks/appointments?assetID=501&scheduleID=1&dateRangeFrom=2026-08-01T00:00:00Z&dateRangeTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
[
  {
    "scheduleID": 1,
    "appointmentID": 100,
    "appointment": "2026-08-20T10:00:00Z",
    "appointmentWith": "2026-08-20T08:00:00Z",
    "appointmentBy": "2026-08-20T18:00:00Z",
    "assetAssigns": [
      {
        "assetID": 501,
        "assetName": "Насос №1",
        "sortOrder": 0,
        "userID": 42
      }
    ]
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — срабатывания по указанным фильтрам не найдены.
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

### `GET /ScheduledTasks/v2/appointments`

## Пример запроса:
```text
GET /ScheduledTasks/v2/appointments?assetID=501&scheduleID=1&dateRangeFrom=2026-08-01T00:00:00Z&dateRangeTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
[
  {
    "scheduleID": 1,
    "appointmentID": 100,
    "appointment": "2026-08-20T10:00:00Z",
    "appointmentWith": "2026-08-20T08:00:00Z",
    "appointmentBy": "2026-08-20T18:00:00Z",
    "assetAssigns": [
      {
        "assetID": 501,
        "assetName": "Насос №1",
        "sortOrder": 0,
        "users": [42, 43],
        "company": {
          "id": 5,
          "name": "ООО Ремонт",
          "deleted": null
        },
        "location": {
          "id": 10,
          "address": "ул. Примерная, 1",
          "coordinate": "55.7558:37.6173",
          "description": "Цех №1",
          "deleted": null
        }
      }
    ]
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — срабатывания по указанным фильтрам не найдены.
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

### `GET /Schedules`

## Пример запроса:
```text
GET /Schedules
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "frequencyType": {
      "id": 1,
      "name": "Ежедневно"
    }
  },
  "2": {
    "frequencyType": {
      "id": 2,
      "name": "Еженедельно"
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — расписания не найдены.

### `GET /Schedules/appointments/assign`

## Пример запроса:
```text
GET /Schedules/appointments/assign?assetID=501&userID=42&validFrom=2026-08-01T00:00:00Z&validTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "appointments": [
      {
        "appointmentID": 100,
        "appointment": "2026-08-20T10:00:00Z",
        "assetAssigns": [
          {
            "assetID": 501,
            "userID": 42
          }
        ]
      }
    ]
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — назначения по указанным фильтрам не найдены.
- 400 — некорректные параметры фильтрации.

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

### `GET /Schedules/{scheduleID}/appointments`

## Пример запроса:
```text
GET /Schedules/1/appointments?dateFrom=2026-08-01T00:00:00Z&dateTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 100,
    "appointment": "2026-08-20T10:00:00Z"
  },
  {
    "id": 101,
    "appointment": "2026-08-21T10:00:00Z"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — события расписания по указанным параметрам не найдены.

### `GET /Schedules/{scheduleID}/appointments/assign`

## Пример запроса:
```text
GET /Schedules/1/appointments/assign?assetID=501&userID=42&validFrom=2026-08-01T00:00:00Z&validTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "appointments": [
      {
        "appointmentID": 100,
        "appointment": "2026-08-20T10:00:00Z",
        "assetAssigns": [
          {
            "assetID": 501,
            "userID": 42
          }
        ]
      }
    ]
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — назначения по указанным фильтрам не найдены.
- 400 — некорректные параметры фильтрации.
