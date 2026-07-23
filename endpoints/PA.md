# PA — справочник ручек

> **Что здесь:** все ручки сервиса PA (API for personnel administration in HubEx): сигнатуры, параметры, права. Типы — schemas/PA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PA.md`; грабли — `notes/PA.md` (если есть).

Base: `{BASE_URL}/PA`

**Оглавление**

- AssetAssignments — строки 23–29
- Employment — строки 31–39
- GeoTrackingModes — строки 41–43
- Moblities — строки 45–47
- RatingCriteria — строки 49–61
- Sexes — строки 63–65
- Skills — строки 67–79
- Technicians — строки 81–91
- TenantSettings — строки 93–96
- UserGroups — строки 98–100
- UserSkills — строки 102–108
- Users — строки 110–131

## AssetAssignments
- `GET /AssetAssignments` — Возвращает Список назначенного оборудования для указанных пользователей или список пользователей, для которых назанчен указанный объект · права: AssetAssignmentList · paginated · коды: 200, 206
  ← query: userID?:any, assetID?:any, validOn?:any → AssetAssignments.ListResult[]
- `POST /AssetAssignments` — Добавляет или изменяет назначение объекта для пользователя · права: AssetAssignmentMerge · коды: 201, 202
  ← body: MergeData[]
- `DELETE /AssetAssignments` — Удаляет назначение объекта для пользователя · права: AssetAssignmentDelete · коды: 202
  ← body: DeleteData[]

## Employment
- `POST /Employment` — Добавляет набор записей о трудоустройстве пользователя · права: EmploymentAdd · коды: 201
  ← body: ComplexActionData<AddData> → EmploymentAddResult[]
- `PUT /Employment` — Обновляет набор записей о трудоустройстве пользователя · права: EmploymentUpdate · коды: 202
  ← body: ComplexActionData<UpdateData>
- `DELETE /Employment` — Удаляет набор записей о трудоустройстве пользователя · права: EmploymentRemove · коды: 202
  ← body: ComplexActionData<RemoveData>
- `GET /Employment/{userID}` — Возвращает полный список трудоустройств пользователя · права: EmploymentList · paginated · коды: 200, 206
  ← path: userID:int; query: validFrom?:any, validTill?:any → EmploymentGetResult[]

## GeoTrackingModes
- `GET /GeoTrackingModes` — Возвращает список режимов геотрекинга · права: GeoTrackingModesList · paginated · коды: 200, 206
  → map<GeoTrackingModes.ListResult>

## Moblities
- `GET /Moblities` — Возвращает список мобильностей для данного тенанта · права: MobilitiesList · paginated · коды: 200, 206
  → map<Mobilities.ListResult>

## RatingCriteria
- `GET /RatingCriteria` — Cписок критериев рейтинга. · права: RatingCriteriaList · коды: 200
  → map<RatingCriteria.ListResult>
- `POST /RatingCriteria` — Создание нового критерия рейтинга · права: RatingCriteriaAdd · коды: 201, 409
  ← body: RatingCriteria.AddData[] → int[]
- `PUT /RatingCriteria` — Изменение критерия рейтинга · права: RatingCriteriaUpdate · коды: 202, 409
  ← body: RatingCriteria.UpdateData[]
- `DELETE /RatingCriteria` — Пометить критерии рейтинга, как удаленные · права: RatingCriteriaDelete · коды: 202, 409
  ← body: int[]
- `GET /RatingCriteria/{id}` — Выбор критерия рейтинга по идентификатору. · права: RatingCriteriaGet · коды: 200
  ← path: id:int → RatingCriteria.GetResult
- `DELETE /RatingCriteria/{id}` — Пометить критерий рейтинга, как удаленный · права: RatingCriteriaDelete · коды: 202, 409
  ← path: id:int

## Sexes
- `GET /Sexes` — Возвращает полный список трудоустройств пользователя · права: SexList · paginated · коды: 200, 206
  → map<NameResult>

## Skills
- `GET /Skills` — Возвращает список навыков для данного тенанта · права: SkillList · paginated · коды: 200, 206, 500
  ← query: isDeleted?:enum(true, false) → map<Skills.ListResult>
- `POST /Skills` — Добавляет навыки данному тенанту · права: SkillAdd · коды: 201
  ← body: SkillBaseData[] → Skills.AddResult[]
- `PUT /Skills` — Обновляет навыки данного тенанта · права: SkillUpdate · коды: 202
  ← body: SkillData.UpdateData[]
- `DELETE /Skills` — Помечает навыки, как удаленные · права: SkillDelete · коды: 202
  ← body: int[]
- `GET /Skills/{id}` — Возвращает навык · права: SkillGet · коды: 200
  ← path: id:int → Skills.GetResult
- `DELETE /Skills/{id}` — Помечает навык, как удаленный · права: SkillDelete · коды: 202, 409
  ← path: id:int

## Technicians
- `GET /Technicians/taskSchedules` — Расписание специалиста на дату с заявками для диаграммы Ганта · права: ScheduleTaskListForTenantMember · коды: 200
  ← query: validOn?:any, userID?:any, taskID?:any, validFrom?:any, validTill?:any, isCompleted?:enum(true, false) → ScheduleTaskResult[]
- `GET /Technicians/{userID}/rating` — Статистика по рейтингу мобильного инженера · права: TechnicianRatingGet · коды: 200
  ← path: userID:int → TechnicianRatingResult[]
- `GET /Technicians/{userID}/taskRatings` — Рейтинги инжененра по заявкам · права: TaskTechnicianRatingList · paginated · коды: 200, 206
  ← path: userID:int → TechnicianRatingResult[]
- `GET /Technicians/{userID}/workSchedules` — Расписание специалиста · права: TechnicianWorkScheduleListForTenantMember · коды: 200
  ← path: userID:int; query: validOn?:any, userID?:any, validFrom?:any, validTill?:any → WorkScheduleResult[]
- `GET /Technicians/{userID}/workSchedules/appointments` — Расписание специалиста на дату с заявками · права: ScheduleTaskListForTenantMember · коды: 200
  ← path: userID:int; query: showTransitionalAppointments?:bool, showWholeDayEvents?:bool, validOn?:any, userID?:any, taskID?:any, validFrom?:any, validTill?:any, isCompleted?:enum(true, false), showTransitionalAppointments?:enum(true, false), showWholeDayEvents?:enum(true, false) → AppointmentResult[]

## TenantSettings
- `GET /TenantSettings` — Возвращает список групп пользователей. · коды: 200
  → TenantSettings.GetResult
  Для выполнения данного метода пользователь должен быть **TenantMember**.

## UserGroups
- `GET /UserGroups` — Возвращает список групп пользователей. · права: UserGroupsList · paginated · коды: 200, 206
  → map<UserGroupResult>

## UserSkills
- `POST /UserSkills` — Добавляет навыки пользователям · права: UserSkillAdd · коды: 201
  ← body: ActionData<BaseData>[] → UserSkills.AddResult[]
- `PUT /UserSkills` — Обновляет навыки пользователей · права: UserSkillUpdate · коды: 202
  ← body: ActionData<UpdateData>[]
- `DELETE /UserSkills` — Удаляет навыки пользователей · права: UserSkillDelete · коды: 202
  ← body: ActionData<Int32>[]

## Users
- `PUT /Users/onshift/end/{userID}` — Метод позволяющий пользователю досрочно завершить смену · права: UserWorkShiftOnShift · коды: 202, 409
  ← path: userID:int; body: datetime → WorkShiftFlatProjection
- `GET /Users/onshift/schedules` — Структурированный список представляющий график рабочих смен пользователя · права: UserWorkShiftList · коды: 200
  ← query: userID?:any, validFrom?:any, validTill?:any → map<WorkShiftScheduleDailyItemResult[]>
- `PUT /Users/onshift/start/{userID}` — Метод "На Смене" позволяет начать (создать новую смену) · права: UserWorkShiftOnShift · коды: 202, 409
  ← path: userID:int; body: WorkShiftSimpleData → WorkShiftFlatProjection[]
- `GET /Users/onshift/status` — Проверка статусов пользователей "на смене" - на момент вызова · права: UserWorkShiftList · коды: 200
  ← query: userID?:any → WorkShiftScheduleUserStatusResult[]
- `POST /Users/onshift/{userID}` — Сформировать произвольный график рабочих смен
Смены, переданные в качестве параметра, будут перезаписывать существующие
Обновления не предусмотрено · права: UserWorkShiftAdd · коды: 201, 409
  ← path: userID:int; body: DailyScheduleDto[] → WorkShiftFlatProjection[]
- `DELETE /Users/onshift/{userID}` — Метод позволяет сбросить/удалить пользовательский график рабочих смен для списка дат
Если для пользователя было установлено штатное расписание, то в эти дни будет произведён возврат к нему · права: UserWorkShiftDelete · коды: 202, 409
  ← path: userID:int; body: datetime[]
- `GET /Users/{userID}/workTypes` — Список видов работ пользователя · права: UserWorkTypeList · paginated · коды: 200, 206
  ← path: userID:int → map<WorkTypesListResult>
- `POST /Users/{userID}/workTypes` — Добавляет виды работ пользователю · права: UserWorkTypeAdd · коды: 201
  ← path: userID:int; body: int[] → map<int[][]>
- `DELETE /Users/{userID}/workTypes` — Удаляет виды работ у пользователя · права: UserWorkTypeDelete · коды: 202
  ← path: userID:int; body: int[]
