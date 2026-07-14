# PMP — справочник ручек

> **Что здесь:** все ручки сервиса PMP (API for PMP in HubEx): сигнатуры, параметры, права. Типы — schemas/PMP.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PMP.md`; грабли — `notes/PMP.md` (если есть).
> **Источник:** `snapshots/PMP.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/PMP`

## FrequencyTypes
- `GET /FrequencyTypes` — Метод получения списка типов повторений расписаний · права: FrequencyTypeList
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → map<IdCodeNameResult<Byte>>[]

## ScheduledTasks
- `GET /ScheduledTasks` — Возвращает список шаблонов заявок · права: ScheduledTaskList · paginated
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → map<ScheduledTasks.ListResult>
- `HEAD /ScheduledTasks` — Возвращает заголовок список шаблонов заявок · права: ScheduledTaskList
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:enum(true, false), dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false)
- `GET /ScheduledTasks/appointments` — Возвращает список срабатываний шаблонов заявок · права: ScheduledTaskList · paginated
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → AppointmentResult<AssetAssignResult>[]
- `HEAD /ScheduledTasks/appointments` — Реализует поведение для Head запроса
В Ok-ответ добавляет заголовок Content-Range=0-0/RowCount
Где RowCount - число записей попавших под переданный фильтр · права: ScheduledTaskList · paginated
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false)
- `GET /ScheduledTasks/count` — Возвращает количество плановых заявок, которые будут созданы, по дням · права: ScheduledTaskList
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → map<ListCountResult[]>
- `GET /ScheduledTasks/v2/appointments` — Возвращает список срабатываний шаблонов заявок · права: ScheduledTaskList · paginated
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → AppointmentResult<AssetAssignResultV2>[]
- `GET /ScheduledTasks/v2/count` — Возвращает количество плановых заявок, которые будут созданы, по дням · права: ScheduledTaskList
  ← query: assetID?:any, taskTypeID?:any, workTypeID?:any, criticalityID?:any, userID?:any, scheduleID?:any, appointmentID?:any, dateRangeFrom?:any, dateRangeTill?:any, isAssigned?:enum(true, false) → map<CountResult[]>

## Schedules
- `GET /Schedules` — Метод получения списка расписаний · права: TaskScheduleList · paginated
  → map<GetResult>[]
- `POST /Schedules` — Метод обновления или создания расписаний для тенанта · права: TaskScheduleMerge
  ← body: ScheduleMergeData[]
- `DELETE /Schedules` — Удаление расписаний для тенанта по списку идентификаторов · права: TaskScheduleDelete
  ← body: int[]
- `GET /Schedules/appointments/assign` — Метод получения списка исполнителей для событий расписания · права: ScheduleAppointmentAssignList
  ← query: assetID?:any, userID?:any, scheduleID?:any, appointmentID?:any, validTill?:any, validFrom?:any → map<ScheduleAppointmentAssignListResult[]>
- `POST /Schedules/appointments/assign` — Добавляет исполнителей на заявки событий расписаний · права: ScheduleAppointmentAssignMerge
  ← body: ScheduleAppointmentAssignMergeData[] → ScheduleAppointmentAssignResult
- `DELETE /Schedules/appointments/assign` — Удаляет исполнителей на заявки событий расписаний · права: ScheduleAppointmentAssignDelete
  ← body: ScheduleAppointmentAssignDeleteData[]
- `GET /Schedules/{id}` — Метод получения информации о расписании по идентификатору · права: TaskScheduleGet
  ← path: ID:int → GetResult
- `DELETE /Schedules/{id}` — Удаление расписания для тенанта по идентификатору · права: TaskScheduleDelete
  ← path: ID:int
- `GET /Schedules/{scheduleID}/appointments` — Метод получения списка событий для расписаний · права: ScheduleAppointmentList · paginated
  ← path: scheduleID:int; query: dateFrom?:datetime, dateTill?:datetime → ScheduleAppointments.ListResult[]
- `GET /Schedules/{scheduleID}/appointments/assign` — Метод получения списка исполнителей для событий расписания для конкретного расписания · права: ScheduleAppointmentAssignList
  ← path: scheduleID:int; query: assetID?:any, userID?:any, scheduleID?:any, appointmentID?:any, validTill?:any, validFrom?:any → map<ScheduleAppointmentAssignListResult[]>
- `DELETE /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}` — Удаляет исполнителя из заявки событий расписаний · права: ScheduleAppointmentAssignDelete
  ← path: scheduleID:int, appointmentID:int, assetID:int
- `POST /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}/assign/{userID}` — Добавляет исполнителя на заявку событий расписаний · права: ScheduleAppointmentAssignMerge
  ← path: scheduleID:int, appointmentID:int, assetID:int, userID:int → ScheduleAppointmentAssignResult
