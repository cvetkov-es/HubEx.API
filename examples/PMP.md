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

### `POST /Schedules`

## Пример запроса:
```text
POST /Schedules
Authorization: Bearer <token>
Content-Type: application/json
            
[
  {
    "frequencyTypeID": 1,
    "id": null,
    "options": { "interval": 1, "timeOfDay": "10:00:00" }
  },
  {
    "frequencyTypeID": 2,
    "id": 5,
    "options": { "interval": 2, "daysOfWeek": [1, 3, 5] }
  }
]
```
            
## Пример успешного ответа (200):
```json
[1, 5]
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `DELETE /Schedules`

## Пример запроса:
```text
DELETE /Schedules
Authorization: Bearer <token>
Content-Type: application/json
            
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `POST /Schedules/appointments/assign`

## Пример запроса:
```text
POST /Schedules/appointments/assign
Authorization: Bearer <token>
Content-Type: application/json
            
[
  {
    "scheduleID": 1,
    "appointmentID": 100,
    "assetID": 501,
    "userID": 42
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "scheduleID": 1,
    "appointmentID": 100,
    "assetID": 501,
    "userID": 42
  }
]
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — назначения не были созданы.
- 409 — конфликт при назначении исполнителей.

### `DELETE /Schedules/appointments/assign`

## Пример запроса:
```text
DELETE /Schedules/appointments/assign
Authorization: Bearer <token>
Content-Type: application/json
            
[
  {
    "scheduleID": 1,
    "appointmentID": 100,
    "assetID": 501
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 409 — конфликт при удалении назначений.

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

### `DELETE /Schedules/{id}`

## Пример запроса:
```text
DELETE /Schedules/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `DELETE /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}`

## Пример запроса:
```text
DELETE /Schedules/1/appointments/100/asset/501
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 409 — конфликт при удалении назначений.

### `POST /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}/assign/{userID}`

## Пример запроса:
```text
POST /Schedules/1/appointments/100/asset/501/assign/42
Authorization: Bearer <token>
```
            
## Пример успешного ответа (201):
```json
[
  {
    "scheduleID": 1,
    "appointmentID": 100,
    "assetID": 501,
    "userID": 42
  }
]
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — назначение не было создано.
- 409 — конфликт при назначении исполнителя.
