# PA — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса PA (API for personnel administration in HubEx): сигнатуры, параметры, права. Типы — schemas/PA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PA.md`; грабли — `notes/PA.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/PA`
> Примеры ответов вынесены в [../examples/PA.md](../examples/PA.md).

**Оглавление**

- AssetAssignments — строки 25–27
- Employment — строки 29–31
- GeoTrackingModes — строки 33–35
- Mobilities — строки 37–39
- Moblities — строки 41–43
- RatingCriteria — строки 45–49
- Sexes — строки 51–53
- Skills — строки 55–59
- Technicians — строки 61–71
- TenantSettings — строки 73–75
- UserGroups — строки 77–79
- Users — строки 81–87

## AssetAssignments
- `GET /AssetAssignments` — Возвращает список назначений объектов. · коды: 200, 204, 206 · примеры
  ← query: userID?:int, assetID?:int, validOn?:datetime → RAAListResult[]

## Employment
- `GET /Employment/{userID}` — Возвращает полный список трудоустройств пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: validFrom?:datetime, validTill?:datetime → EmploymentGetResult[]

## GeoTrackingModes
- `GET /GeoTrackingModes` — Возвращает список режимов геотрекинга. · коды: 200, 204, 206 · примеры
  → map<RGTMListResult>

## Mobilities
- `GET /Mobilities` — Возвращает список мобильностей тенанта. · коды: 200, 204, 206 · примеры
  → map<RMListResult>

## Moblities
- `GET /Moblities` — Возвращает список мобильностей тенанта. · коды: 200, 204, 206 · примеры
  → map<RMListResult>

## RatingCriteria
- `GET /RatingCriteria` — Возвращает список критериев рейтинга. · коды: 200 · примеры
  → map<RRCListResult>
- `GET /RatingCriteria/{id}` — Возвращает критерий рейтинга по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RRCGetResult

## Sexes
- `GET /Sexes` — Возвращает список полов. · коды: 200, 204, 206 · примеры
  → map<NameResult>

## Skills
- `GET /Skills` — Возвращает список навыков тенанта. · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool → map<RSListResult>
- `GET /Skills/{id}` — Возвращает навык по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RSGetResult

## Technicians
- `GET /Technicians/taskSchedules` — Возвращает расписание заявок для диаграммы Ганта. · коды: 200, 204 · примеры
  ← query: validOn?:datetime, userID?:int, taskID?:int, validFrom?:datetime, validTill?:datetime, isCompleted?:bool → ScheduleTaskResult[]
- `GET /Technicians/{userID}/rating` — Возвращает статистику рейтинга мобильного инженера. · коды: 200, 204 · примеры
  ← path: userID:int → TechnicianRatingResult
- `GET /Technicians/{userID}/taskRatings` — Возвращает оценки инженера по заявкам. · коды: 200, 204 · примеры
  ← path: userID:int → TaskRatingResult[]
- `GET /Technicians/{userID}/workSchedules` — Возвращает рабочее расписание специалиста. · коды: 200, 204 · примеры
  ← path: userID:int; query: validOn?:datetime, userID?:int, validFrom?:datetime, validTill?:datetime → map<WorkScheduleResult>
- `GET /Technicians/{userID}/workSchedules/appointments` — Возвращает расписание специалиста на дату вместе с назначенными заявками. · коды: 200, 204 · примеры
  ← path: userID:int; query: showTransitionalAppointments?:bool, showWholeDayEvents?:bool, validOn?:datetime, userID?:int, taskID?:int, validFrom?:datetime, validTill?:datetime, isCompleted?:bool → AppointmentResult[]

## TenantSettings
- `GET /TenantSettings` — Возвращает настройки тенанта для модуля PA. · коды: 200 · примеры
  → RTSGetResult

## UserGroups
- `GET /UserGroups` — Возвращает список групп пользователей. · коды: 200 · примеры
  → map<UserGroupResult>

## Users
- `GET /Users/onshift/schedules` — Возвращает структурированный график рабочих смен пользователей. · коды: 200, 204, 400 · примеры
  ← query: userID?:int, validFrom?:datetime, validTill?:datetime → map<WorkShiftScheduleDailyItemResult[]>
- `GET /Users/onshift/status` — Возвращает текущие статусы пользователей "на смене". · коды: 200, 204 · примеры
  ← query: userID?:int → WorkShiftScheduleUserStatusResult[]
- `GET /Users/{userID}/workTypes` — Возвращает список видов работ пользователя. · коды: 200, 204, 206 · примеры
  ← path: userID:int → map<WorkTypesListResult[]>
