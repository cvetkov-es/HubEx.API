# PA — схемы

> **Что здесь:** определения типов запросов/ответов сервиса PA. Ручки, ссылающиеся на них — `endpoints/PA.md`.
> **Источник:** `snapshots/PA.json` · файл генерируется пайплайном — руками не править.

```
type ActionData<BaseData> { data: BaseData[], userID: int }
type ActionData<Int32> { data: int[], userID: int }
type ActionData<UpdateData> { data: UserSkillData.UpdateData[], userID: int }
type AppointmentResult { period?: PeriodResult, taskPeriod?: PeriodResult, isContinuedOnTheNextDay?: bool /* Признак перехода заявки на следующий день */, task?: TaskResult, coordinate?: str /* Географическая координата Lat:Lng */ }
type AssetAssignments.ListResult { user?: UserResult, asset?: AssetResult, validityPeriod?: PeriodResult, notes?: str /* Примечания */ }
type AssetResult { id?: int, name?: str, host?: IdNameDeletedResult<Int32>, deleted?: datetime, parentID?: int }
type BaseData { skillID: int, dateFrom: datetime, dateTill: datetime }
type ComplexActionData<AddData> { userID: int /* Идентификатор пользователя. */, data?: EmploymentData.AddData[] /* Перечисление сущностей сложного типа. */ }
type ComplexActionData<RemoveData> { userID: int /* Идентификатор пользователя. */, data?: RemoveData[] /* Перечисление сущностей сложного типа. */ }
type ComplexActionData<UpdateData> { userID: int /* Идентификатор пользователя. */, data?: EmploymentData.UpdateData[] /* Перечисление сущностей сложного типа. */ }
type Counters { tasks?: int /* Количество заявок с навыком */, assets?: int /* Количество оборудования с навыком */, users?: int /* Количество пользователей с навыком */ }
type CriticalityResult { id?: int, name?: str, color?: str /* Цвет критичности */ }
type DailyScheduleDto { date: datetime /* День yyyy-mm-dd */, isDayOff?: bool /* Признак того, что этот день не будет рабочим */, workShifts?: WorkShiftDto[] }
type DeleteData { assetID?: int, userID?: int, dateTill?: datetime }
type EmploymentAddResult { userID?: int /* Идентификатор пользователя */, id?: int /* Идентификатор записи о трудоустройстве */ }
type EmploymentData.AddData { dateTill: datetime, personnelNumber?: str, erpID?: str, userGroupID?: int, position?: str, orgUnitID?: int, scheduleRuleID?: int, dutyScheduleRuleID?: int, dateFrom: datetime }
type EmploymentData.UpdateData { dateTill: datetime, personnelNumber?: str, erpID?: str, userGroupID?: int, position?: str, orgUnitID?: int, scheduleRuleID?: int, dutyScheduleRuleID?: int, dateFrom: datetime, id?: int }
type EmploymentGetResult { validityPeriod?: PeriodResult, id?: int /* Идентификатор записи */, personnelNumber?: str /* Табельный номер */, erpID?: str /* Идентификатор пользователя в ERP */, position?: str /* Должность */, userGroup?: IdNameResult<Byte>, orgUnit?: IdNameResult<Int32>, company?: IdNameResult<Int16>, scheduleRule?: IdNameResult<Int32>, dutyScheduleRule?: IdNameResult<Int32> }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type GeoTrackingModes.ListResult { name?: str /* Название режима геотрекинга */ }
type IdNameDeletedResult<Int16> { id?: int, name?: str, deleted?: datetime }
type IdNameDeletedResult<Int32> { id?: int, name?: str, deleted?: datetime }
type IdNameDescriptionResult<Int16> { id?: int, name?: str, description?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type LocationResult { id?: int, address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, description?: str /* Описание локации */, deleted?: datetime /* Метка времени (UTC), когда локация была удалена */ }
type MergeData { assetID?: int, userID?: int, dateTill?: datetime, notes?: str, dateFrom?: datetime }
type Mobilities.ListResult { name?: str /* Название мобильности */, maxDistanceFromDefaultLocation?: int /* Максимальное удаление от расположения по умолчанию */, maxDistanceFromActualLocation?: int /* Максимальное удаление от текущего расположения */ }
type NameResult { name?: str /* Название */ }
type PeriodResult { from?: datetime, till?: datetime }
type RatingCriteria.AddData { name: str, weight: float, isSystem?: bool }
type RatingCriteria.GetResult { name?: str /* Наименование критерия рейтинга */, weight?: float /* Весовой коэффициент критерия рейтинга */, isSystem?: bool /* Является критерий рейтинга системным? */, id?: int /* Идентификатор критерия рейтинга */ }
type RatingCriteria.ListResult { name?: str /* Наименование критерия рейтинга */, weight?: float /* Весовой коэффициент критерия рейтинга */, isSystem?: bool /* Является критерий рейтинга системным? */ }
type RatingCriteria.UpdateData { name: str, weight: float, isSystem?: bool, id: int }
type RatingResult { rating?: float /* Рейтинг */, trend?: int }
type RemoveData { id?: int }
type ScheduleTaskResult { period?: PeriodResult, taskPeriod?: PeriodResult, taskAssignmentPeriod?: PeriodResult, description?: str /* Описания заявки в расписании */, assignedTo?: UserResult, listAssignedTo?: UserResult[] /* Список исполнителей */, task?: TaskScheduleResult, company?: IdNameDeletedResult<Int16>, location?: LocationResult }
type SkillBaseData { name: str, description?: str, isOptional: bool }
type SkillData.UpdateData { name: str, description?: str, isOptional: bool, id: int }
type Skills.AddResult { skillID?: int /* Идентификатор навыка */ }
type Skills.GetResult { id?: int, name?: str, isOptional?: bool /* Флаг необязательности */, description?: str /* Описание навыка */, deleted?: datetime /* Метка времени (UTC), когда навык был удален */ }
type Skills.ListResult { id?: int, name?: str, isOptional?: bool /* Флаг необязательности */, counters?: Counters }
type TaskResult { id?: int /* Ид заявки */, number?: str /* Номер заявки */, notes?: str /* Примечания по заявки */, asset?: AssetResult, criticality?: CriticalityResult, isClosed?: bool /* Заявка уже закрыта? */, isCompleted?: bool /* Заявка уже выполнена? */ }
type TaskScheduleResult { id?: int /* Ид заявки */, number?: str /* Номер заявки */, notes?: str /* Примечания по заявки */, asset?: AssetResult, criticality?: CriticalityResult, isClosed?: bool /* Заявка уже закрыта? */, isCompleted?: bool /* Заявка уже выполнена? */, deadline?: datetime /* Дедлайн */, workType?: IdNameResult<Int16>, taskType?: IdNameResult<Byte> }
type TechnicianRatingResult { total?: RatingResult, lastYear?: RatingResult, lastFourMonths?: RatingResult, lastMonth?: RatingResult, lastWeek?: RatingResult, lastTenTasks?: RatingResult, lastFiftyTasks?: RatingResult, lastHundredTasks?: RatingResult, timestamp?: datetime /* Метка времени последнего пересчета рейтинга */ }
type TenantSettings.GetResult { maxRatingMark?: int /* Максимальный рейтинг. */ }
type UserGroupResult { name?: str /* Имя. */ }
type UserResult { id?: int, firstName?: str, lastName?: str, middleName?: str, avatarUrl?: str, deleted?: datetime }
type UserSkillData.UpdateData { skillID: int, dateFrom: datetime, dateTill: datetime, sourceDateTill: datetime }
type UserSkills.AddResult { skillID?: int /* Идентификатор навыка */, userID?: int /* Идентификатор пользователя */, dateTill?: datetime /* Дата окончания периода действия навыка */ }
type WorkScheduleResult { workPeriod?: PeriodResult, plannedWorkMinutes?: int /* Рабочее время в минутах */, taskWorkMinutes?: int /* Количество запланированного рабочего времени в минутах */, isNightShift?: bool /* Признак ночной смены */ }
type WorkShiftDto { timeFrom?: str /* Начало смены hh:mm (лучше использовать hh:mm:ss) */, timeTill?: str /* Конец смены hh:mm (лучше использовать hh:mm:ss) */ }
type WorkShiftFlatProjection { date?: datetime, timeFrom?: str, timeTill?: str, id?: int, isDayOff?: bool }
type WorkShiftScheduleDailyItemResult { isDayOff?: bool /* Является ли день выходным для пользователя */, isCustomSchedule?: bool /* Признак того, что график в этот день введен пользователем поверх основного */, isPublicHoliday?: bool /* Официальный выходной день */, id?: int /* Внутренний идентификатор рабочей смены */, isNightShift?: bool /* Признак ночной смены */, dateWork?: datetime /* Дата работы */, timeFrom?: datetime /* Время начала смены в таймзоне тенанта */, timeTill?: datetime /* Время окончание смены в таймзоне тенанта */ }
type WorkShiftScheduleUserStatusResult { userID?: int /* Идентификатор пользователя */, onShift?: bool /* Признак того, что пользователь находится на смене */, timeFrom?: datetime /* Начало смены */, timeTill?: datetime /* Конец смены */ }
type WorkShiftSimpleData { from?: datetime /* Дата и время начала смены Utc */, till?: datetime /* Дата и время окончания смены Utc */ }
type WorkTypesListResult { workType?: IdNameDescriptionResult<Int16>, workClass?: IdNameResult<Int16> }
```
