# PA — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса PA. Ручки, ссылающиеся на них — `endpoints/PA.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type AppointmentResult { coordinate?: str /* Географическая координата Lat:Lng */, isContinuedOnTheNextDay?: bool /* Признак перехода заявки на следующий день */, period?: PeriodResult, task?: TaskResult, taskPeriod?: PeriodResult }
type AssetResult { deleted?: datetime, host?: IdNameDeletedResultOfInt, id?: int, name?: str, parentID?: int }
type Counters { assets?: int /* Количество оборудования с навыком */, tasks?: int /* Количество заявок с навыком */, users?: int /* Количество пользователей с навыком */ }
type CriticalityResult { color?: str /* Цвет критичности */, id?: int, name?: str }
type EmploymentGetResult { company?: IdNameResultOfShort, dutyScheduleRule?: IdNameResultOfInt, erpID?: str /* Идентификатор пользователя в ERP */, id?: int /* Идентификатор записи */, orgUnit?: IdNameResultOfInt, personnelNumber?: str /* Табельный номер */, position?: str /* Должность */, scheduleRule?: IdNameResultOfInt, userGroup?: IdNameResultOfByte, validityPeriod?: PeriodResult }
type IdNameDeletedResultOfInt { deleted?: datetime, id?: int, name?: str }
type IdNameDeletedResultOfShort { deleted?: datetime, id?: int, name?: str }
type IdNameDescriptionResultOfShort { description?: str, id?: int, name?: str }
type IdNameResultOfByte { id?: int, name?: str }
type IdNameResultOfInt { id?: int, name?: str }
type IdNameResultOfShort { id?: int, name?: str }
type LocationResult { address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, deleted?: datetime /* Метка времени (UTC), когда локация была удалена */, description?: str /* Описание локации */, id?: int }
type NameResult { name?: str /* Название */ }
type PeriodResult { from?: datetime, till?: datetime }
type RAAListResult { asset?: AssetResult, notes?: str /* Примечания */, user?: UserResult, validityPeriod?: PeriodResult }
type RatingResult { rating?: float /* Рейтинг */, trend?: int }
type RGTMListResult { name?: str /* Название режима геотрекинга */ }
type RMListResult { maxDistanceFromActualLocation?: int /* Максимальное удаление от текущего расположения */, maxDistanceFromDefaultLocation?: int /* Максимальное удаление от расположения по умолчанию */, name?: str /* Название мобильности */ }
type RRCGetResult { id?: int /* Идентификатор критерия рейтинга */, isSystem?: bool /* Является критерий рейтинга системным? */, name?: str /* Наименование критерия рейтинга */, weight?: float /* Весовой коэффициент критерия рейтинга */ }
type RRCListResult { isSystem?: bool /* Является критерий рейтинга системным? */, name?: str /* Наименование критерия рейтинга */, weight?: float /* Весовой коэффициент критерия рейтинга */ }
type RSGetResult { deleted?: datetime /* Метка времени (UTC), когда навык был удален */, description?: str /* Описание навыка */, id?: int, isOptional?: bool /* Флаг необязательности */, name?: str }
type RSListResult { counters?: Counters, id?: int, isOptional?: bool /* Флаг необязательности */, name?: str }
type RTSGetResult { maxRatingMark?: int /* Максимальный рейтинг. */ }
type ScheduleTaskResult { assignedTo?: UserResult, company?: IdNameDeletedResultOfShort, description?: str /* Описания заявки в расписании */, listAssignedTo?: UserResult[] /* Список исполнителей */, location?: LocationResult, period?: PeriodResult, task?: TaskScheduleResult, taskAssignmentPeriod?: PeriodResult, taskPeriod?: PeriodResult }
type TaskRatingResult { comment?: str /* Комментарий */, ignoreReason?: str /* ПРичина, по которой необходимо игнорировать оценку */, isIgnore?: bool /* Признак игнорирования оценки */, rating?: int /* Оценка */, ratingCriteria?: IdNameResultOfByte, taskCompleted?: datetime /* Дата выполнения заявки, по которой была выставлена оценка */, taskID?: int /* Идентификатор заявки, по которой была выставлена оценка */, taskNumber?: str /* Номер заявки, по которой была выставлена оценка */ }
type TaskResult { asset?: AssetResult, criticality?: CriticalityResult, id?: int /* Ид заявки */, isClosed?: bool /* Заявка уже закрыта? */, isCompleted?: bool /* Заявка уже выполнена? */, notes?: str /* Примечания по заявки */, number?: str /* Номер заявки */ }
type TaskScheduleResult { asset?: AssetResult, criticality?: CriticalityResult, deadline?: datetime /* Дедлайн */, id?: int /* Ид заявки */, isClosed?: bool /* Заявка уже закрыта? */, isCompleted?: bool /* Заявка уже выполнена? */, notes?: str /* Примечания по заявки */, number?: str /* Номер заявки */, taskType?: IdNameResultOfByte, workType?: IdNameResultOfShort }
type TechnicianRatingResult { lastFiftyTasks?: RatingResult, lastFourMonths?: RatingResult, lastHundredTasks?: RatingResult, lastMonth?: RatingResult, lastTenTasks?: RatingResult, lastWeek?: RatingResult, lastYear?: RatingResult, timestamp?: datetime /* Метка времени последнего пересчета рейтинга */, total?: RatingResult }
type UserGroupResult { name?: str /* Имя. */ }
type UserResult { avatarUrl?: str, deleted?: datetime, firstName?: str, id?: int, lastName?: str, middleName?: str }
type WorkScheduleResult { isNightShift?: bool /* Признак ночной смены */, plannedWorkMinutes?: int /* Рабочее время в минутах */, taskWorkMinutes?: int /* Количество запланированного рабочего времени в минутах */, workPeriod?: PeriodResult }
type WorkShiftScheduleDailyItemResult { dateWork?: datetime /* Дата работы */, id?: int /* Внутренний идентификатор рабочей смены */, isCustomSchedule?: bool /* Признак того, что график в этот день введен пользователем поверх основного */, isDayOff?: bool /* Является ли день выходным для пользователя */, isNightShift?: bool /* Признак ночной смены */, isPublicHoliday?: bool /* Официальный выходной день */, timeFrom?: datetime /* Время начала смены в таймзоне тенанта */, timeTill?: datetime /* Время окончание смены в таймзоне тенанта */ }
type WorkShiftScheduleUserStatusResult { onShift?: bool /* Признак того, что пользователь находится на смене */, timeFrom?: datetime /* Начало смены */, timeTill?: datetime /* Конец смены */, userID?: int /* Идентификатор пользователя */ }
type WorkTypesListResult { workClass?: IdNameResultOfShort, workType?: IdNameDescriptionResultOfShort }
```
