# PMP — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса PMP (API for PMP in HubEx): сигнатуры, параметры, права. Типы — schemas/PMP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PMP.md`; грабли — `notes/PMP.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/PMP`

**Оглавление**

- FrequencyTypes — строки 15–17
- ScheduledTasks — строки 19–35
- Schedules — строки 37–47

## FrequencyTypes
- `GET /FrequencyTypes` — Метод получения списка типов повторений расписаний · права: FrequencyTypeList · коды: 200
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → map<IdCodeNameResult<Byte>>[]

## ScheduledTasks
- `GET /ScheduledTasks` — Возвращает список шаблонов заявок · права: ScheduledTaskList · paginated · коды: 200, 206
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → map<ScheduledTasks.ListResult>
- `HEAD /ScheduledTasks` — Возвращает заголовок список шаблонов заявок · права: ScheduledTaskList · коды: 200
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:enum(true, false), dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false)
- `GET /ScheduledTasks/appointments` — Возвращает список срабатываний шаблонов заявок · права: ScheduledTaskList · paginated · коды: 200, 206
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → AppointmentResult<AssetAssignResult>[]
- `HEAD /ScheduledTasks/appointments` — Реализует поведение для Head запроса
В Ok-ответ добавляет заголовок Content-Range=0-0/RowCount
Где RowCount - число записей попавших под переданный фильтр · права: ScheduledTaskList · paginated · коды: 200, 206
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false)
- `GET /ScheduledTasks/count` — Возвращает количество плановых заявок, которые будут созданы, по дням · права: ScheduledTaskList · коды: 200
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → map<ListCountResult[]>
- `GET /ScheduledTasks/v2/appointments` — Возвращает список срабатываний шаблонов заявок · права: ScheduledTaskList · paginated · коды: 200, 206
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → AppointmentResult<AssetAssignResultV2>[]
- `GET /ScheduledTasks/v2/count` — Возвращает количество плановых заявок, которые будут созданы, по дням · права: ScheduledTaskList · коды: 200
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → map<CountResult[]>

## Schedules
- `GET /Schedules` — Метод получения списка расписаний · права: TaskScheduleList · paginated · коды: 200, 206
  → map<GetResult>[]
- `GET /Schedules/appointments/assign` — Метод получения списка исполнителей для событий расписания · права: ScheduleAppointmentAssignList · коды: 200, 400
  ← query: assetID?:any, userID?:any, scheduleID?:any, appointmentID?:any, validTill?:any, validFrom?:any → map<ScheduleAppointmentAssignListResult[]>
- `GET /Schedules/{id}` — Метод получения информации о расписании по идентификатору · права: TaskScheduleGet · коды: 200
  ← path: ID:int → GetResult
- `GET /Schedules/{scheduleID}/appointments` — Метод получения списка событий для расписаний · права: ScheduleAppointmentList · paginated · коды: 200, 206
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → ScheduleAppointments.ListResult[]
- `GET /Schedules/{scheduleID}/appointments/assign` — Метод получения списка исполнителей для событий расписания для конкретного расписания · права: ScheduleAppointmentAssignList · коды: 200, 400
  ← path: scheduleID:int; query: assetID?:any, userID?:any, scheduleID?:any, appointmentID?:any, validTill?:any, validFrom?:any → map<ScheduleAppointmentAssignListResult[]>
