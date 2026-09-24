# PMP — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса PMP (API for PMP in HubEx): сигнатуры, параметры, права. Типы — schemas/PMP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PMP.md`; грабли — `notes/PMP.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/PMP`
> Примеры ответов вынесены в [../examples/PMP.md](../examples/PMP.md).

**Оглавление**

- FrequencyTypes — строки 44–46
- ScheduledTasks — строки 48–51
- Пример запроса: — строки 53–58
- Пример успешного ответа (200): — строки 60–71
- Пример успешного ответа (206): — строки 73–74
- Негативные сценарии: — строки 76–84
- Пример запроса: — строки 86–91
- Пример успешного ответа (200): — строки 93–112
- Пример успешного ответа (206): — строки 114–115
- Негативные сценарии: — строки 117–128
- Пример запроса: — строки 130–135
- Пример успешного ответа (200): — строки 137–168
- Пример успешного ответа (206): — строки 170–171
- Негативные сценарии: — строки 173–178
- Schedules — строки 180–183
- Пример запроса: — строки 185–190
- Пример успешного ответа (200): — строки 192–208
- Пример успешного ответа (206): — строки 210–211
- Негативные сценарии: — строки 213–218
- Пример запроса: — строки 220–225
- Пример успешного ответа (200): — строки 227–245
- Пример успешного ответа (206): — строки 247–248
- Негативные сценарии: — строки 250–258
- Пример запроса: — строки 260–265
- Пример успешного ответа (200): — строки 267–279
- Пример успешного ответа (206): — строки 281–282
- Негативные сценарии: — строки 284–289
- Пример запроса: — строки 291–296
- Пример успешного ответа (200): — строки 298–316
- Пример успешного ответа (206): — строки 318–319
- Негативные сценарии: — строки 321–324

## FrequencyTypes
- `GET /FrequencyTypes` — Возвращает список типов повторений расписаний. · коды: 200, 204 · примеры
  → map<IdCodeNameResultOfByte>

## ScheduledTasks
- `GET /ScheduledTasks` — Возвращает список шаблонов плановых заявок. · коды: 200, 204, 206, 400
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → map<RSTListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
            
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
- `HEAD /ScheduledTasks` — Возвращает заголовок с количеством шаблонов плановых заявок. · коды: 200, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool
- `GET /ScheduledTasks/appointments` — Возвращает список срабатываний шаблонов плановых заявок. · коды: 200, 204, 206, 400
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → AppointmentResultOfRSTAssetAssignResult[]
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
            
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
- `HEAD /ScheduledTasks/appointments` — Возвращает заголовок с количеством срабатываний шаблонов заявок. · коды: 200, 204, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool
- `GET /ScheduledTasks/count` — Возвращает количество плановых заявок по дням с разбивкой по исполнителям. · коды: 200, 204, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → map<ListCountResult[]>
- `GET /ScheduledTasks/v2/appointments` — Возвращает список срабатываний шаблонов плановых заявок (версия 2). · коды: 200, 204, 206, 400
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → AppointmentResultOfAssetAssignResultV2[]
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
В отличие от v1, возвращает несколько исполнителей на объект, а также данные о компании и локации.
            
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
- `GET /ScheduledTasks/v2/count` — Возвращает агрегированное количество плановых заявок по дням (версия 2). · коды: 200, 204, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → map<CountResult[]>

## Schedules
- `GET /Schedules` — Возвращает список расписаний текущего тенанта. · коды: 200, 204, 206
  → map<RSRListResult>
  Поддерживает постраничную выборку через заголовок `Range`.
            
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
- `GET /Schedules/appointments/assign` — Возвращает список назначенных исполнителей для событий расписаний. · коды: 200, 204, 206, 400
  ← query: assetID?:int, userID?:int, scheduleID?:int, appointmentID?:int, validTill?:datetime, validFrom?:datetime → map<ScheduleAppointmentAssignListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
            
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
- `GET /Schedules/{id}` — Возвращает информацию о расписании по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → GetResult
- `GET /Schedules/{scheduleID}/appointments` — Возвращает список событий (точек срабатывания) для расписания. · коды: 200, 204, 206
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → RSAListResult[]
  Поддерживает постраничную выборку через заголовок `Range`.
            
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
- `GET /Schedules/{scheduleID}/appointments/assign` — Возвращает список назначенных исполнителей для событий конкретного расписания. · коды: 200, 204, 206, 400
  ← path: scheduleID:int; query: assetID?:int, userID?:int, scheduleID?:int, appointmentID?:int, validTill?:datetime, validFrom?:datetime → map<ScheduleAppointmentAssignListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
            
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
