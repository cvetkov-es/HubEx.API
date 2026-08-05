# PA — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса PA (API for personnel administration in HubEx): сигнатуры, параметры, права. Типы — schemas/PA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PA.md`; грабли — `notes/PA.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/PA`

**Оглавление**

- AssetAssignments — строки 23–25
- Employment — строки 27–29
- GeoTrackingModes — строки 31–33
- Moblities — строки 35–37
- RatingCriteria — строки 39–43
- Sexes — строки 45–47
- Skills — строки 49–53
- Technicians — строки 55–65
- TenantSettings — строки 67–70
- UserGroups — строки 72–74
- Users — строки 76–82

## AssetAssignments
- `GET /AssetAssignments` — Возвращает Список назначенного оборудования для указанных пользователей или список пользователей, для которых назанчен указанный объект · права: AssetAssignmentList · paginated · коды: 200, 206
  ← query: userID?:int, assetID?:int, validOn?:datetime → AssetAssignments.ListResult[]

## Employment
- `GET /Employment/{userID}` — Возвращает полный список трудоустройств пользователя · права: EmploymentList · paginated · коды: 200, 206
  ← path: userID:int; query: validFrom?:datetime, validTill?:datetime → EmploymentGetResult[]

## GeoTrackingModes
- `GET /GeoTrackingModes` — Возвращает список режимов геотрекинга · права: GeoTrackingModesList · paginated · коды: 200, 206
  → map<GeoTrackingModes.ListResult>

## Moblities
- `GET /Moblities` — Возвращает список мобильностей для данного тенанта · права: MobilitiesList · paginated · коды: 200, 206
  → map<Mobilities.ListResult>

## RatingCriteria
- `GET /RatingCriteria` — Cписок критериев рейтинга. · права: RatingCriteriaList · коды: 200
  → map<RatingCriteria.ListResult>
- `GET /RatingCriteria/{id}` — Выбор критерия рейтинга по идентификатору. · права: RatingCriteriaGet · коды: 200
  ← path: id:int → RatingCriteria.GetResult

## Sexes
- `GET /Sexes` — Возвращает полный список трудоустройств пользователя · права: SexList · paginated · коды: 200, 206
  → map<NameResult>

## Skills
- `GET /Skills` — Возвращает список навыков для данного тенанта · права: SkillList · paginated · коды: 200, 206, 500
  ← query: isDeleted?:enum(true, false) → map<Skills.ListResult>
- `GET /Skills/{id}` — Возвращает навык · права: SkillGet · коды: 200
  ← path: id:int → Skills.GetResult

## Technicians
- `GET /Technicians/taskSchedules` — Расписание специалиста на дату с заявками для диаграммы Ганта · права: ScheduleTaskListForTenantMember · коды: 200
  ← query: validOn?:datetime, userID?:int, taskID?:int, validFrom?:datetime, validTill?:datetime, isCompleted?:enum(true, false) → ScheduleTaskResult[]
- `GET /Technicians/{userID}/rating` — Статистика по рейтингу мобильного инженера · права: TechnicianRatingGet · коды: 200
  ← path: userID:int → TechnicianRatingResult[]
- `GET /Technicians/{userID}/taskRatings` — Рейтинги инжененра по заявкам · права: TaskTechnicianRatingList · paginated · коды: 200, 206
  ← path: userID:int → TechnicianRatingResult[]
- `GET /Technicians/{userID}/workSchedules` — Расписание специалиста · права: TechnicianWorkScheduleListForTenantMember · коды: 200
  ← path: userID:int; query: validOn?:datetime, userID?:int, validFrom?:datetime, validTill?:datetime → WorkScheduleResult[]
- `GET /Technicians/{userID}/workSchedules/appointments` — Расписание специалиста на дату с заявками · права: ScheduleTaskListForTenantMember · коды: 200
  ← path: userID:int; query: showTransitionalAppointments?:bool, showWholeDayEvents?:bool, validOn?:datetime, userID?:int, taskID?:int, validFrom?:datetime, validTill?:datetime, isCompleted?:enum(true, false), showTransitionalAppointments?:enum(true, false), showWholeDayEvents?:enum(true, false) → AppointmentResult[]

## TenantSettings
- `GET /TenantSettings` — Возвращает список групп пользователей. · коды: 200
  → TenantSettings.GetResult
  Для выполнения данного метода пользователь должен быть **TenantMember**.

## UserGroups
- `GET /UserGroups` — Возвращает список групп пользователей. · права: UserGroupsList · paginated · коды: 200, 206
  → map<UserGroupResult>

## Users
- `GET /Users/onshift/schedules` — Структурированный список представляющий график рабочих смен пользователя · права: UserWorkShiftList · коды: 200
  ← query: userID?:int, validFrom?:datetime, validTill?:datetime → map<WorkShiftScheduleDailyItemResult[]>
- `GET /Users/onshift/status` — Проверка статусов пользователей "на смене" - на момент вызова · права: UserWorkShiftList · коды: 200
  ← query: userID?:int → WorkShiftScheduleUserStatusResult[]
- `GET /Users/{userID}/workTypes` — Список видов работ пользователя · права: UserWorkTypeList · paginated · коды: 200, 206
  ← path: userID:int → map<WorkTypesListResult>
