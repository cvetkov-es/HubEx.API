# PMP — справочник ручек

> **Что здесь:** все ручки сервиса PMP (API for PMP in HubEx): сигнатуры, параметры, права. Типы — schemas/PMP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PMP.md`; грабли — `notes/PMP.md` (если есть).

Base: `{BASE_URL}/PMP`

**Оглавление**

- FrequencyTypes — строки 14–16
- ScheduledTasks — строки 18–34
- Schedules — строки 36–60

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
- `POST /Schedules` — Метод обновления или создания расписаний для тенанта · права: TaskScheduleMerge · коды: 202
  ← body: ScheduleMergeData[]
- `DELETE /Schedules` — Удаление расписаний для тенанта по списку идентификаторов · права: TaskScheduleDelete · коды: 202
  ← body: int[]
- `GET /Schedules/appointments/assign` — Метод получения списка исполнителей для событий расписания · права: ScheduleAppointmentAssignList · коды: 200, 400
  ← query: assetID?:any, userID?:any, scheduleID?:any, appointmentID?:any, validTill?:any, validFrom?:any → map<ScheduleAppointmentAssignListResult[]>
- `POST /Schedules/appointments/assign` — Добавляет исполнителей на заявки событий расписаний · права: ScheduleAppointmentAssignMerge · коды: 201, 409
  ← body: ScheduleAppointmentAssignMergeData[] → ScheduleAppointmentAssignResult
- `DELETE /Schedules/appointments/assign` — Удаляет исполнителей на заявки событий расписаний · права: ScheduleAppointmentAssignDelete · коды: 202, 409
  ← body: ScheduleAppointmentAssignDeleteData[]
- `GET /Schedules/{id}` — Метод получения информации о расписании по идентификатору · права: TaskScheduleGet · коды: 200
  ← path: ID:int → GetResult
- `DELETE /Schedules/{id}` — Удаление расписания для тенанта по идентификатору · права: TaskScheduleDelete · коды: 202
  ← path: ID:int
- `GET /Schedules/{scheduleID}/appointments` — Метод получения списка событий для расписаний · права: ScheduleAppointmentList · paginated · коды: 200, 206
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → ScheduleAppointments.ListResult[]
- `GET /Schedules/{scheduleID}/appointments/assign` — Метод получения списка исполнителей для событий расписания для конкретного расписания · права: ScheduleAppointmentAssignList · коды: 200, 400
  ← path: scheduleID:int; query: assetID?:any, userID?:any, scheduleID?:any, appointmentID?:any, validTill?:any, validFrom?:any → map<ScheduleAppointmentAssignListResult[]>
- `DELETE /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}` — Удаляет исполнителя из заявки событий расписаний · права: ScheduleAppointmentAssignDelete · коды: 202, 409
  ← path: scheduleID:int, appointmentID:int, assetID:int
- `POST /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}/assign/{userID}` — Добавляет исполнителя на заявку событий расписаний · права: ScheduleAppointmentAssignMerge · коды: 201, 409
  ← path: scheduleID:int, appointmentID:int, assetID:int, userID:int → ScheduleAppointmentAssignResult
