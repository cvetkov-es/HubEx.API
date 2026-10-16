# PMP — справочник ручек

> **Что здесь:** все ручки сервиса PMP (API for PMP in HubEx): сигнатуры, параметры, права. Типы — schemas/PMP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PMP.md`; грабли — `notes/PMP.md` (если есть).

Base: `{BASE_URL}/PMP`
> Примеры ответов вынесены в [../examples/PMP.md](../examples/PMP.md).

**Оглавление**

- FrequencyTypes — строки 15–17
- ScheduledTasks — строки 19–36
- Schedules — строки 38–66

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
- `POST /Schedules` — Создаёт или обновляет расписания для текущего тенанта. · коды: 200, 400 · примеры
  ← body: ScheduleMergeData[] → int[]
- `DELETE /Schedules` — Удаляет расписания по списку идентификаторов. · коды: 202, 400 · примеры
  ← body: int[]
- `GET /Schedules/appointments/assign` — Возвращает список назначенных исполнителей для событий расписаний. · paginated · коды: 200, 204, 206, 400 · примеры
  ← query: assetID?:int, userID?:int, scheduleID?:int, appointmentID?:int, validTill?:datetime, validFrom?:datetime → map<ScheduleAppointmentAssignListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
- `POST /Schedules/appointments/assign` — Назначает исполнителей на заявки событий расписаний. · коды: 201, 204, 409 · примеры
  ← body: ScheduleAppointmentAssignMergeData[] → ScheduleAppointmentAssignResult[]
- `DELETE /Schedules/appointments/assign` — Удаляет назначения исполнителей с заявок событий расписаний. · коды: 202, 409 · примеры
  ← body: ScheduleAppointmentAssignDeleteData[]
- `GET /Schedules/{id}` — Возвращает информацию о расписании по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → GetResult
- `DELETE /Schedules/{id}` — Удаляет расписание по идентификатору. · коды: 202, 400 · примеры
  ← path: id:int
- `GET /Schedules/{scheduleID}/appointments` — Возвращает список событий (точек срабатывания) для расписания. · paginated · коды: 200, 204, 206 · примеры
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → RSAListResult[]
  Поддерживает постраничную выборку через заголовок `Range`.
- `GET /Schedules/{scheduleID}/appointments/assign` — Возвращает список назначенных исполнителей для событий конкретного расписания. · paginated · коды: 200, 204, 206, 400 · примеры
  ← path: scheduleID:int; query: assetID?:int, userID?:int, scheduleID?:int, appointmentID?:int, validTill?:datetime, validFrom?:datetime → map<ScheduleAppointmentAssignListResult>
  Поддерживает фильтрацию по query-параметрам и постраничную выборку через заголовок `Range`.
- `DELETE /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}` — Удаляет все назначения исполнителей с заявки события расписания по объекту. · коды: 202, 409 · примеры
  ← path: scheduleID:int, appointmentID:int, assetID:int
- `POST /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}/assign/{userID}` — Назначает исполнителя на заявку события расписания. · коды: 201, 204, 409 · примеры
  ← path: scheduleID:int, appointmentID:int, assetID:int, userID:int → ScheduleAppointmentAssignResult[]
