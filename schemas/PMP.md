# PMP — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса PMP. Ручки, ссылающиеся на них — `endpoints/PMP.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type AppointmentResult { appointment?: datetime /* Дата и время создания плановой заявки */, appointmentID?: int /* Идентификатор точки срабатывания */, assetAssigns?: RSAAAssetAssignResult[] /* Список оборудования для точки расписание с исполнителями */ }
type AppointmentResultOfAssetAssignResultV2 { appointment?: datetime /* Дата и время создания плановой заявки */, appointmentBy?: datetime /* Дата По */, appointmentID?: int /* Идентификатор точки срабатывания */, appointmentWith?: datetime /* Дата С */, assetAssigns?: AssetAssignResultV2[] /* Список оборудования для точки расписание с исполнителями */, scheduleID?: int /* Идентификатор расписания */ }
type AppointmentResultOfRSTAssetAssignResult { appointment?: datetime /* Дата и время создания плановой заявки */, appointmentBy?: datetime /* Дата По */, appointmentID?: int /* Идентификатор точки срабатывания */, appointmentWith?: datetime /* Дата С */, assetAssigns?: RSTAssetAssignResult[] /* Список оборудования для точки расписание с исполнителями */, scheduleID?: int /* Идентификатор расписания */ }
type AssetAssignResultV2 { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, assetName?: str /* Наименование оборудования, по которому будет создана заявка */, company?: IdNameDeletedResultOfShort, location?: LocationResult, sortOrder?: int /* Индекс сортировки */, users?: int[] }
type CountResult { countTasksForDay?: int /* Общее количество заявок на дату */, countTasksForUsers?: ListCountResult[] /* Количество заявок на дату по исполнителям */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type GetResult { frequencyType?: IdNameResultOfByte, id?: int /* Идентификатор расписания */, options?: str /* Настройки срабатывания расписания в формате JSON */ }
type IdCodeNameResultOfByte { code?: str, id?: int, name?: str }
type IdNameDeletedResultOfShort { deleted?: datetime, id?: int, name?: str }
type IdNameResultOfByte { id?: int, name?: str }
type ListCountResult { countWithAssign?: int /* Количество назначенных заявок на дату */, countWithoutAssign?: int /* Количество неназначенных заявок на дату */, userID?: int /* Идентификатор исполнителя назначенной заявки (0 — для неназначенных) */ }
type LocationResult { address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, deleted?: datetime /* Метка времени (UTC), когда локация была удалена */, description?: str /* Описание локации */, id?: int }
type ProblemDetails { detail?: str, instance?: str, status?: int, title?: str, type?: str }
type RSAAAssetAssignResult { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, userID?: int /* Идентификатор исполнителя по заявке в конкретной точке по этому оборудованию */ }
type RSAListResult { appointment?: datetime /* Дата и время точки расписания */, id?: int }
type RSRListResult { frequencyType?: IdNameResultOfByte }
type RSTAssetAssignResult { assetID?: int /* Идентификатор оборудования, по которому будет создана заявка */, assetName?: str /* Наименование оборудования, по которому будет создана заявка */, sortOrder?: int /* Индекс сортировки */, userID?: int /* Идентификатор исполнителя по заявке в конкретной точке по этому оборудованию */ }
type RSTListResult { description?: str /* Описание плановой заявки */, name?: str /* Наименование плановой заявки */, notes?: str /* Замечания к плановой заявки */, sortOrder?: int /* Индекс сортировки */, taskTemplateID?: str /* Идентификатор плановой заявки */ }
type ScheduleAppointmentAssignListResult { appointments?: AppointmentResult[] /* Список точек срабатывания с исполнителями */ }
```
