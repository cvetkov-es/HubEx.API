# PMP — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса PMP (API for PMP in HubEx): сигнатуры, параметры, права. Типы — schemas/PMP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PMP.md`; грабли — `notes/PMP.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/PMP`
> Примеры ответов вынесены в [../examples/PMP.md](../examples/PMP.md).

**Оглавление**

- FrequencyTypes — строки 16–18
- ScheduledTasks — строки 20–37
- Schedules — строки 39–53

## FrequencyTypes
- `GET /FrequencyTypes` — Возвращает список типов повторений расписаний. · коды: 200, 204 · примеры
  → map<IdCodeNameResultOfByte>

## ScheduledTasks
- `GET /ScheduledTasks` — Возвращает список шаблонов плановых заявок. · paginated · коды: 200, 204, 206, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → map<RSTListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
- `HEAD /ScheduledTasks` — Возвращает заголовок с количеством шаблонов плановых заявок. · коды: 200, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool
- `GET /ScheduledTasks/appointments` — Возвращает список срабатываний шаблонов плановых заявок. · paginated · коды: 200, 204, 206, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → AppointmentResultOfRSTAssetAssignResult[]
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
- `HEAD /ScheduledTasks/appointments` — Возвращает заголовок с количеством срабатываний шаблонов заявок. · коды: 200, 204, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool
- `GET /ScheduledTasks/count` — Возвращает количество плановых заявок по дням с разбивкой по исполнителям. · коды: 200, 204, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → map<ListCountResult[]>
- `GET /ScheduledTasks/v2/appointments` — Возвращает список срабатываний шаблонов плановых заявок (версия 2). · paginated · коды: 200, 204, 206, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → AppointmentResultOfAssetAssignResultV2[]
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`. В отличие от v1, возвращает несколько исполнителей на объект, а также данные о компании и локации.
- `GET /ScheduledTasks/v2/count` — Возвращает агрегированное количество плановых заявок по дням (версия 2). · коды: 200, 204, 400 · примеры
  ← query: assetID?:int, taskTypeID?:int, workTypeID?:int, criticalityID?:int, userID?:int, scheduleID?:int, appointmentID?:int, dateRangeFrom?:datetime, dateRangeTill?:datetime, isAssigned?:bool → map<CountResult[]>

## Schedules
- `GET /Schedules` — Возвращает список расписаний текущего тенанта. · paginated · коды: 200, 204, 206 · примеры
  → map<RSRListResult>
  Поддерживает постраничную выборку через заголовок `Range`.
- `GET /Schedules/appointments/assign` — Возвращает список назначенных исполнителей для событий расписаний. · paginated · коды: 200, 204, 206, 400 · примеры
  ← query: assetID?:int, userID?:int, scheduleID?:int, appointmentID?:int, validTill?:datetime, validFrom?:datetime → map<ScheduleAppointmentAssignListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
- `GET /Schedules/{id}` — Возвращает информацию о расписании по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → GetResult
- `GET /Schedules/{scheduleID}/appointments` — Возвращает список событий (точек срабатывания) для расписания. · paginated · коды: 200, 204, 206 · примеры
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → RSAListResult[]
  Поддерживает постраничную выборку через заголовок `Range`.
- `GET /Schedules/{scheduleID}/appointments/assign` — Возвращает список назначенных исполнителей для событий конкретного расписания. · paginated · коды: 200, 204, 206, 400 · примеры
  ← path: scheduleID:int; query: assetID?:int, userID?:int, scheduleID?:int, appointmentID?:int, validTill?:datetime, validFrom?:datetime → map<ScheduleAppointmentAssignListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
