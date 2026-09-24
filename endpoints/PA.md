# PA — справочник ручек

> **Что здесь:** все ручки сервиса PA (API for personnel administration in HubEx): сигнатуры, параметры, права. Типы — schemas/PA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PA.md`; грабли — `notes/PA.md` (если есть).

Base: `{BASE_URL}/PA`
> Примеры ответов вынесены в [../examples/PA.md](../examples/PA.md).

**Оглавление**

- AssetAssignments — строки 25–31
- Employment — строки 33–41
- GeoTrackingModes — строки 43–45
- Mobilities — строки 47–49
- Moblities — строки 51–53
- RatingCriteria — строки 55–67
- Sexes — строки 69–71
- Skills — строки 73–85
- Technicians — строки 87–97
- TenantSettings — строки 99–101
- UserGroups — строки 103–105
- UserSkills — строки 107–113
- Users — строки 115–133

## AssetAssignments
- `GET /AssetAssignments` — Возвращает список назначений объектов. · коды: 200, 204, 206 · примеры
  ← query: userID?:int, assetID?:int, validOn?:datetime → RAAListResult[]
- `POST /AssetAssignments` — Добавляет или изменяет назначение объекта для пользователя. · коды: 201, 202 · примеры
  ← body: PAAAMergeData[]
- `DELETE /AssetAssignments` — Удаляет назначение объекта для пользователя. · коды: 202 · примеры
  ← body: PAAADeleteData[]

## Employment
- `POST /Employment` — Добавляет набор записей о трудоустройстве пользователя · коды: 201, 400 · примеры
  ← body: ComplexActionDataOfPAEDAddData → EmploymentAddResult[]
- `PUT /Employment` — Обновляет набор записей о трудоустройстве пользователя · коды: 202, 400 · примеры
  ← body: ComplexActionDataOfPAEDUpdateData
- `DELETE /Employment` — Удаляет набор записей о трудоустройстве пользователя · коды: 202, 400 · примеры
  ← body: ComplexActionDataOfPAEDRemoveData
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
- `POST /RatingCriteria` — Создаёт новые критерии рейтинга. · коды: 201, 409 · примеры
  ← body: PARCAddData[] → int[]
- `PUT /RatingCriteria` — Обновляет критерии рейтинга. · коды: 202, 409 · примеры
  ← body: PARCUpdateData[]
- `DELETE /RatingCriteria` — Помечает критерии рейтинга как удалённые. · коды: 202, 409 · примеры
  ← body: int[]
- `GET /RatingCriteria/{id}` — Возвращает критерий рейтинга по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RRCGetResult
- `DELETE /RatingCriteria/{id}` — Помечает критерий рейтинга как удалённый. · коды: 202, 409 · примеры
  ← path: id:int

## Sexes
- `GET /Sexes` — Возвращает список полов. · коды: 200, 204, 206 · примеры
  → map<NameResult>

## Skills
- `GET /Skills` — Возвращает список навыков тенанта. · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool → map<RSListResult>
- `POST /Skills` — Добавляет навыки тенанту. · коды: 201, 204 · примеры
  ← body: SkillBaseData[] → RSAddResult[]
- `PUT /Skills` — Обновляет навыки тенанта. · коды: 202 · примеры
  ← body: PASDUpdateData[]
- `DELETE /Skills` — Помечает навыки как удалённые. · коды: 202 · примеры
  ← body: int[]
- `GET /Skills/{id}` — Возвращает навык по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RSGetResult
- `DELETE /Skills/{id}` — Помечает навык как удалённый. · коды: 202, 409 · примеры
  ← path: id:int

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

## UserSkills
- `POST /UserSkills` — Добавляет навыки пользователям. · коды: 201, 204 · примеры
  ← body: USDCActionDataOfUSDBBaseData[] → RUSAddResult[]
- `PUT /UserSkills` — Обновляет навыки пользователей. · коды: 202 · примеры
  ← body: USDCActionDataOfPAUSDUpdateData[]
- `DELETE /UserSkills` — Удаляет навыки пользователей. · коды: 202 · примеры
  ← body: USDCActionDataOfInt[]

## Users
- `PUT /Users/onshift/end/{userID}` — Досрочно завершает смену пользователя. · коды: 202, 409 · примеры
  ← path: userID:int; body: datetime → WorkShiftFlatProjection
- `GET /Users/onshift/schedules` — Возвращает структурированный график рабочих смен пользователей. · коды: 200, 204, 400 · примеры
  ← query: userID?:int, validFrom?:datetime, validTill?:datetime → map<WorkShiftScheduleDailyItemResult[]>
- `PUT /Users/onshift/start/{userID}` — Запускает новую смену пользователя. · коды: 202, 400, 409 · примеры
  ← path: userID:int; body: WorkShiftSimpleData → WorkShiftFlatProjection[]
- `GET /Users/onshift/status` — Возвращает текущие статусы пользователей "на смене". · коды: 200, 204 · примеры
  ← query: userID?:int → WorkShiftScheduleUserStatusResult[]
- `POST /Users/onshift/{userID}` — Создает произвольный график рабочих смен пользователя. · коды: 201, 400, 409 · примеры
  ← path: userID:int; body: DailyScheduleDto[] → WorkShiftFlatProjection[]
- `DELETE /Users/onshift/{userID}` — Удаляет пользовательский график рабочих смен для списка дат. · коды: 202, 409 · примеры
  ← path: userID:int; body: datetime[]
- `GET /Users/{userID}/workTypes` — Возвращает список видов работ пользователя. · коды: 200, 204, 206 · примеры
  ← path: userID:int → map<WorkTypesListResult[]>
- `POST /Users/{userID}/workTypes` — Добавляет пользователю виды работ. · коды: 201, 400 · примеры
  ← path: userID:int; body: int[] → map<int[]>
- `DELETE /Users/{userID}/workTypes` — Удаляет у пользователя виды работ. · коды: 202, 400 · примеры
  ← path: userID:int; body: int[]
