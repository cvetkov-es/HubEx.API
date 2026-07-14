# PMP — схемы

> **Что здесь:** определения типов запросов/ответов сервиса PMP. Ручки, ссылающиеся на них — `endpoints/PMP.md`.
> **Источник:** `snapshots/PMP.json` · файл генерируется пайплайном — руками не править.

```
type AppointmentResult { appointmentID?: int /* Идентификатор точки срабатывания */, appointment?: datetime /* Дата и время создания плановой заявки */, assetAssigns?: ScheduleAppointmentAssign.AssetAssignResult[] /* Список оборудования для точки расписание с исполнителями */ }
type AppointmentResult<AssetAssignResult> { scheduleID?: int /* Идентификатор расписания */, appointmentID?: int /* Идентификатор точки срабатывания */, appointment?: datetime /* Дата и время создания плановой заявки */, appointmentWith?: datetime /* Дата С */, appointmentBy?: datetime /* Дата По */, assetAssigns?: ScheduledTasks.AssetAssignResult[] /* Список оборудования для точки расписание с исполнителями */ }
type AppointmentResult<AssetAssignResultV2> { scheduleID?: int /* Идентификатор расписания */, appointmentID?: int /* Идентификатор точки срабатывания */, appointment?: datetime /* Дата и время создания плановой заявки */, appointmentWith?: datetime /* Дата С */, appointmentBy?: datetime /* Дата По */, assetAssigns?: AssetAssignResultV2[] /* Список оборудования для точки расписание с исполнителями */ }
type AssetAssignResultV2 { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, assetName?: str /* Наименование оборудования, по которому будет создана заявка */, sortOrder?: int /* Индекс сортировки */, users?: int[], company?: IdNameDeletedResult<Int16>, location?: LocationResult }
type CountResult { countTasksForDay?: int /* Общее количество заявок на дату */, countTasksForUsers?: ListCountResult[] /* Количество заявок на дату по исполнителям */ }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type GetResult { frequencyType?: IdNameResult<Byte>, id?: int /* Идентификатор расписания */, options?: str /* Настройки срабатывания расписания в формате JSON */ }
type IdCodeNameResult<Byte> { id?: int, code?: str, name?: str }
type IdNameDeletedResult<Int16> { id?: int, name?: str, deleted?: datetime }
type IdNameResult<Byte> { id?: int, name?: str }
type ListCountResult { userID?: int /* Идентификатор исполнителя назначенной заявки (0 - для неназначненных_ */, countWithAssign?: int /* Количество назначенных заявок на дату */, countWithoutAssign?: int /* Количество неназначенных заявок на дату */ }
type LocationResult { id?: int, address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, description?: str /* Описание локации */, deleted?: datetime /* Метка времени (UTC), когда локация была удалена */ }
type ScheduleAppointmentAssign.AssetAssignResult { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, userID?: int /* Идентификатор исполнителя по заявке в конкретной точке по этому оборудованию */ }
type ScheduleAppointmentAssignDeleteData { scheduleID?: int, appointmentID?: int, assetID?: int }
type ScheduleAppointmentAssignListResult { appointments?: AppointmentResult[] /* Список точек срабатывания с исполнителями */ }
type ScheduleAppointmentAssignMergeData { scheduleID?: int, appointmentID?: int, assetID?: int, userID?: int }
type ScheduleAppointmentAssignResult { scheduleID?: int /* Идентификатор расписания */, appointmentID?: int /* Идентификатор точки срабатывания */, assetID?: int /* Идентификатор объекта точки срабатывания */, userID?: int /* Идентификатор назначенного исполнителя */ }
type ScheduleAppointments.ListResult { id?: int, appointment?: datetime /* Дата и время точки расписания */ }
type ScheduledTasks.AssetAssignResult { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, assetName?: str /* Наименование оборудования, по которому будет создана заявка */, sortOrder?: int /* Индекс сортировки */, userID?: int /* Идентификатор исполнителя по заявке в конкретной точке по этому оборудованию */ }
type ScheduledTasks.ListResult { taskTemplateID?: str /* Идентификатор плановой заявки */, name?: str /* Наименование плановой заявки */, description?: str /* Описание плановой заявки */, notes?: str /* Замечания к плановой заявки */, sortOrder?: int /* Индекс сортировки */ }
type ScheduleMergeData { frequencyTypeID?: int /* Идентификатор частоты повторения */, id?: int /* Идентификатор расписания */, options?: str /* Информация о расписании в формате JSON */ }
```
