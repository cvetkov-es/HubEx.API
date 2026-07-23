# PA — схемы

> **Что здесь:** определения типов запросов/ответов сервиса PA. Ручки, ссылающиеся на них — `endpoints/PA.md`.

```
type ActionData<BaseData> { data: BaseData[], userID: int }
type ActionData<Int32> { data: int[], userID: int }
type ActionData<UpdateData> { data: UserSkillData.UpdateData[], userID: int }
type AppointmentResult { coordinate?: str /* Географическая координата Lat:Lng */, isContinuedOnTheNextDay?: bool /* Признак перехода заявки на следующий день */, period?: PeriodResult, task?: TaskResult, taskPeriod?: PeriodResult }
type AssetAssignments.ListResult { asset?: AssetResult, notes?: str /* Примечания */, user?: UserResult, validityPeriod?: PeriodResult }
type AssetResult { deleted?: datetime, host?: IdNameDeletedResult<Int32>, id?: int, name?: str, parentID?: int }
type BaseData { dateFrom: datetime, dateTill: datetime, skillID: int }
type ComplexActionData<AddData> { data?: EmploymentData.AddData[] /* Перечисление сущностей сложного типа. */, userID: int /* Идентификатор пользователя. */ }
type ComplexActionData<RemoveData> { data?: RemoveData[] /* Перечисление сущностей сложного типа. */, userID: int /* Идентификатор пользователя. */ }
type ComplexActionData<UpdateData> { data?: EmploymentData.UpdateData[] /* Перечисление сущностей сложного типа. */, userID: int /* Идентификатор пользователя. */ }
type Counters { assets?: int /* Количество оборудования с навыком */, tasks?: int /* Количество заявок с навыком */, users?: int /* Количество пользователей с навыком */ }
type CriticalityResult { color?: str /* Цвет критичности */, id?: int, name?: str }
type DailyScheduleDto { date: datetime /* День yyyy-mm-dd */, isDayOff?: bool /* Признак того, что этот день не будет рабочим */, workShifts?: WorkShiftDto[] }
type DeleteData { assetID?: int, dateTill?: datetime, userID?: int }
type EmploymentAddResult { id?: int /* Идентификатор записи о трудоустройстве */, userID?: int /* Идентификатор пользователя */ }
type EmploymentData.AddData { dateFrom: datetime, dateTill: datetime, dutyScheduleRuleID?: int, erpID?: str, orgUnitID?: int, personnelNumber?: str, position?: str, scheduleRuleID?: int, userGroupID?: int }
type EmploymentData.UpdateData { dateFrom: datetime, dateTill: datetime, dutyScheduleRuleID?: int, erpID?: str, id?: int, orgUnitID?: int, personnelNumber?: str, position?: str, scheduleRuleID?: int, userGroupID?: int }
type EmploymentGetResult { company?: IdNameResult<Int16>, dutyScheduleRule?: IdNameResult<Int32>, erpID?: str /* Идентификатор пользователя в ERP */, id?: int /* Идентификатор записи */, orgUnit?: IdNameResult<Int32>, personnelNumber?: str /* Табельный номер */, position?: str /* Должность */, scheduleRule?: IdNameResult<Int32>, userGroup?: IdNameResult<Byte>, validityPeriod?: PeriodResult }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type GeoTrackingModes.ListResult { name?: str /* Название режима геотрекинга */ }
type IdNameDeletedResult<Int16> { deleted?: datetime, id?: int, name?: str }
type IdNameDeletedResult<Int32> { deleted?: datetime, id?: int, name?: str }
type IdNameDescriptionResult<Int16> { description?: str, id?: int, name?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type LocationResult { address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, deleted?: datetime /* Метка времени (UTC), когда локация была удалена */, description?: str /* Описание локации */, id?: int }
type MergeData { assetID?: int, dateFrom?: datetime, dateTill?: datetime, notes?: str, userID?: int }
type Mobilities.ListResult { maxDistanceFromActualLocation?: int /* Максимальное удаление от текущего расположения */, maxDistanceFromDefaultLocation?: int /* Максимальное удаление от расположения по умолчанию */, name?: str /* Название мобильности */ }
type NameResult { name?: str /* Название */ }
type PeriodResult { from?: datetime, till?: datetime }
type RatingCriteria.AddData { isSystem?: bool, name: str, weight: float }
type RatingCriteria.GetResult { id?: int /* Идентификатор критерия рейтинга */, isSystem?: bool /* Является критерий рейтинга системным? */, name?: str /* Наименование критерия рейтинга */, weight?: float /* Весовой коэффициент критерия рейтинга */ }
type RatingCriteria.ListResult { isSystem?: bool /* Является критерий рейтинга системным? */, name?: str /* Наименование критерия рейтинга */, weight?: float /* Весовой коэффициент критерия рейтинга */ }
type RatingCriteria.UpdateData { id: int, isSystem?: bool, name: str, weight: float }
type RatingResult { rating?: float /* Рейтинг */, trend?: int }
type RemoveData { id?: int }
type ScheduleTaskResult { assignedTo?: UserResult, company?: IdNameDeletedResult<Int16>, description?: str /* Описания заявки в расписании */, listAssignedTo?: UserResult[] /* Список исполнителей */, location?: LocationResult, period?: PeriodResult, task?: TaskScheduleResult, taskAssignmentPeriod?: PeriodResult, taskPeriod?: PeriodResult }
type SkillBaseData { description?: str, isOptional: bool, name: str }
type SkillData.UpdateData { description?: str, id: int, isOptional: bool, name: str }
type Skills.AddResult { skillID?: int /* Идентификатор навыка */ }
type Skills.GetResult { deleted?: datetime /* Метка времени (UTC), когда навык был удален */, description?: str /* Описание навыка */, id?: int, isOptional?: bool /* Флаг необязательности */, name?: str }
type Skills.ListResult { counters?: Counters, id?: int, isOptional?: bool /* Флаг необязательности */, name?: str }
type TaskResult { asset?: AssetResult, criticality?: CriticalityResult, id?: int /* Ид заявки */, isClosed?: bool /* Заявка уже закрыта? */, isCompleted?: bool /* Заявка уже выполнена? */, notes?: str /* Примечания по заявки */, number?: str /* Номер заявки */ }
type TaskScheduleResult { asset?: AssetResult, criticality?: CriticalityResult, deadline?: datetime /* Дедлайн */, id?: int /* Ид заявки */, isClosed?: bool /* Заявка уже закрыта? */, isCompleted?: bool /* Заявка уже выполнена? */, notes?: str /* Примечания по заявки */, number?: str /* Номер заявки */, taskType?: IdNameResult<Byte>, workType?: IdNameResult<Int16> }
type TechnicianRatingResult { lastFiftyTasks?: RatingResult, lastFourMonths?: RatingResult, lastHundredTasks?: RatingResult, lastMonth?: RatingResult, lastTenTasks?: RatingResult, lastWeek?: RatingResult, lastYear?: RatingResult, timestamp?: datetime /* Метка времени последнего пересчета рейтинга */, total?: RatingResult }
type TenantSettings.GetResult { maxRatingMark?: int /* Максимальный рейтинг. */ }
type UserGroupResult { name?: str /* Имя. */ }
type UserResult { avatarUrl?: str, deleted?: datetime, firstName?: str, id?: int, lastName?: str, middleName?: str }
type UserSkillData.UpdateData { dateFrom: datetime, dateTill: datetime, skillID: int, sourceDateTill: datetime }
type UserSkills.AddResult { dateTill?: datetime /* Дата окончания периода действия навыка */, skillID?: int /* Идентификатор навыка */, userID?: int /* Идентификатор пользователя */ }
type WorkScheduleResult { isNightShift?: bool /* Признак ночной смены */, plannedWorkMinutes?: int /* Рабочее время в минутах */, taskWorkMinutes?: int /* Количество запланированного рабочего времени в минутах */, workPeriod?: PeriodResult }
type WorkShiftDto { timeFrom?: str /* Начало смены hh:mm (лучше использовать hh:mm:ss) */, timeTill?: str /* Конец смены hh:mm (лучше использовать hh:mm:ss) */ }
type WorkShiftFlatProjection { date?: datetime, id?: int, isDayOff?: bool, timeFrom?: str, timeTill?: str }
type WorkShiftScheduleDailyItemResult { dateWork?: datetime /* Дата работы */, id?: int /* Внутренний идентификатор рабочей смены */, isCustomSchedule?: bool /* Признак того, что график в этот день введен пользователем поверх основного */, isDayOff?: bool /* Является ли день выходным для пользователя */, isNightShift?: bool /* Признак ночной смены */, isPublicHoliday?: bool /* Официальный выходной день */, timeFrom?: datetime /* Время начала смены в таймзоне тенанта */, timeTill?: datetime /* Время окончание смены в таймзоне тенанта */ }
type WorkShiftScheduleUserStatusResult { onShift?: bool /* Признак того, что пользователь находится на смене */, timeFrom?: datetime /* Начало смены */, timeTill?: datetime /* Конец смены */, userID?: int /* Идентификатор пользователя */ }
type WorkShiftSimpleData { from?: datetime /* Дата и время начала смены Utc */, till?: datetime /* Дата и время окончания смены Utc */ }
type WorkTypesListResult { workClass?: IdNameResult<Int16>, workType?: IdNameDescriptionResult<Int16> }
```
