# PMP — справочник ручек

> **Что здесь:** все ручки сервиса PMP (API for PMP in HubEx): сигнатуры, параметры, права. Типы — schemas/PMP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PMP.md`; грабли — `notes/PMP.md` (если есть).

Base: `{BASE_URL}/PMP`
> Примеры ответов вынесены в [../examples/PMP.md](../examples/PMP.md).

**Оглавление**

- FrequencyTypes — строки 43–45
- ScheduledTasks — строки 47–50
- Пример запроса: — строки 52–57
- Пример успешного ответа (200): — строки 59–70
- Пример успешного ответа (206): — строки 72–73
- Негативные сценарии: — строки 75–83
- Пример запроса: — строки 85–90
- Пример успешного ответа (200): — строки 92–111
- Пример успешного ответа (206): — строки 113–114
- Негативные сценарии: — строки 116–127
- Пример запроса: — строки 129–134
- Пример успешного ответа (200): — строки 136–167
- Пример успешного ответа (206): — строки 169–170
- Негативные сценарии: — строки 172–177
- Schedules — строки 179–182
- Пример запроса: — строки 184–189
- Пример успешного ответа (200): — строки 191–207
- Пример успешного ответа (206): — строки 209–210
- Негативные сценарии: — строки 212–221
- Пример запроса: — строки 223–228
- Пример успешного ответа (200): — строки 230–248
- Пример успешного ответа (206): — строки 250–251
- Негативные сценарии: — строки 253–267
- Пример запроса: — строки 269–274
- Пример успешного ответа (200): — строки 276–288
- Пример успешного ответа (206): — строки 290–291
- Негативные сценарии: — строки 293–298
- Пример запроса: — строки 300–305
- Пример успешного ответа (200): — строки 307–325
- Пример успешного ответа (206): — строки 327–328
- Негативные сценарии: — строки 330–337

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
- `POST /Schedules` — Создаёт или обновляет расписания для текущего тенанта. · коды: 200, 400 · примеры
  ← body: ScheduleMergeData[] → int[]
- `DELETE /Schedules` — Удаляет расписания по списку идентификаторов. · коды: 202, 400 · примеры
  ← body: int[]
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
- `POST /Schedules/appointments/assign` — Назначает исполнителей на заявки событий расписаний. · коды: 201, 204, 409 · примеры
  ← body: ScheduleAppointmentAssignMergeData[] → ScheduleAppointmentAssignResult[]
- `DELETE /Schedules/appointments/assign` — Удаляет назначения исполнителей с заявок событий расписаний. · коды: 202, 409 · примеры
  ← body: ScheduleAppointmentAssignDeleteData[]
- `GET /Schedules/{id}` — Возвращает информацию о расписании по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → GetResult
- `DELETE /Schedules/{id}` — Удаляет расписание по идентификатору. · коды: 202, 400 · примеры
  ← path: id:int
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
- `DELETE /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}` — Удаляет все назначения исполнителей с заявки события расписания по объекту. · коды: 202, 409 · примеры
  ← path: scheduleID:int, appointmentID:int, assetID:int
- `POST /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}/assign/{userID}` — Назначает исполнителя на заявку события расписания. · коды: 201, 204, 409 · примеры
  ← path: scheduleID:int, appointmentID:int, assetID:int, userID:int → ScheduleAppointmentAssignResult[]
