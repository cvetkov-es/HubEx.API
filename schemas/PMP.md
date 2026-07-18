# PMP — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса PMP. Ручки, ссылающиеся на них — `endpoints/PMP.md`.
> **Источник:** swagger сервиса PMP · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type AppointmentResult { appointment?: datetime /* Дата и время создания плановой заявки */, appointmentID?: int /* Идентификатор точки срабатывания */, assetAssigns?: ScheduleAppointmentAssign.AssetAssignResult[] /* Список оборудования для точки расписание с исполнителями */ }
type AppointmentResult<AssetAssignResult> { appointment?: datetime /* Дата и время создания плановой заявки */, appointmentBy?: datetime /* Дата По */, appointmentID?: int /* Идентификатор точки срабатывания */, appointmentWith?: datetime /* Дата С */, assetAssigns?: ScheduledTasks.AssetAssignResult[] /* Список оборудования для точки расписание с исполнителями */, scheduleID?: int /* Идентификатор расписания */ }
type AppointmentResult<AssetAssignResultV2> { appointment?: datetime /* Дата и время создания плановой заявки */, appointmentBy?: datetime /* Дата По */, appointmentID?: int /* Идентификатор точки срабатывания */, appointmentWith?: datetime /* Дата С */, assetAssigns?: AssetAssignResultV2[] /* Список оборудования для точки расписание с исполнителями */, scheduleID?: int /* Идентификатор расписания */ }
type AssetAssignResultV2 { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, assetName?: str /* Наименование оборудования, по которому будет создана заявка */, company?: IdNameDeletedResult<Int16>, location?: LocationResult, sortOrder?: int /* Индекс сортировки */, users?: int[] }
type CountResult { countTasksForDay?: int /* Общее количество заявок на дату */, countTasksForUsers?: ListCountResult[] /* Количество заявок на дату по исполнителям */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type GetResult { frequencyType?: IdNameResult<Byte>, id?: int /* Идентификатор расписания */, options?: str /* Настройки срабатывания расписания в формате JSON */ }
type IdCodeNameResult<Byte> { code?: str, id?: int, name?: str }
type IdNameDeletedResult<Int16> { deleted?: datetime, id?: int, name?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type ListCountResult { countWithAssign?: int /* Количество назначенных заявок на дату */, countWithoutAssign?: int /* Количество неназначенных заявок на дату */, userID?: int /* Идентификатор исполнителя назначенной заявки (0 - для неназначненных_ */ }
type LocationResult { address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, deleted?: datetime /* Метка времени (UTC), когда локация была удалена */, description?: str /* Описание локации */, id?: int }
type ScheduleAppointmentAssign.AssetAssignResult { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, userID?: int /* Идентификатор исполнителя по заявке в конкретной точке по этому оборудованию */ }
type ScheduleAppointmentAssignListResult { appointments?: AppointmentResult[] /* Список точек срабатывания с исполнителями */ }
type ScheduleAppointments.ListResult { appointment?: datetime /* Дата и время точки расписания */, id?: int }
type ScheduledTasks.AssetAssignResult { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, assetName?: str /* Наименование оборудования, по которому будет создана заявка */, sortOrder?: int /* Индекс сортировки */, userID?: int /* Идентификатор исполнителя по заявке в конкретной точке по этому оборудованию */ }
type ScheduledTasks.ListResult { description?: str /* Описание плановой заявки */, name?: str /* Наименование плановой заявки */, notes?: str /* Замечания к плановой заявки */, sortOrder?: int /* Индекс сортировки */, taskTemplateID?: str /* Идентификатор плановой заявки */ }
```
