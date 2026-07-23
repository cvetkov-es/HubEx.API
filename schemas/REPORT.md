# REPORT — схемы

> **Что здесь:** определения типов запросов/ответов сервиса REPORT. Ручки, ссылающиеся на них — `endpoints/REPORT.md`.

```
type AssetResult { deleted?: datetime, host?: IdNameDeletedResult<Int32>, id?: int, name?: str, parentID?: int }
type CustomReportList { name?: str /* Название отчета */, reportID?: str /* Идентификатор отчета */, reportType?: IdNameResult<Byte> }
type DatePart enum(Year, Quarter, Month, Day, Week, Second, Minute, Hour)
type IdNameDeletedResult<Int32> { deleted?: datetime, id?: int, name?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type PlannedMaintenanceResult { appointment?: datetime /* Метка времени (UTC) события */, asset?: AssetResult, assetClass?: IdNameResult<Byte>, assetType?: IdNameResult<Byte>, frequencyType?: IdNameResult<Byte>, normalWorkingHours?: int /* Трудозатраты в нормочасах */, normalWorkingMinutes?: int /* Трудозатраты в нормоминутах */, taskTemplateID?: str /* Идентификатор шаблона заявки */, taskType?: IdNameResult<Byte>, workType?: IdNameResult<Int16> }
type TaskListGroupByAssigneesResult { activeTasksCount?: int /* Количество активных заявок */, assignee?: UserResult, outdatedTasksCount?: int /* Количество просроченных заявок */, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */ }
type TaskListGroupByCompaniesResult { activeTasksCount?: int /* Количество активных заявок */, company?: IdNameResult<Int32>, outdatedTasksCount?: int /* Количество просроченных заявок */, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */ }
type TaskListGroupByStagesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, taskStage?: TaskStageResult, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */ }
type TaskListGroupByWorkTypesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */, workType?: IdNameResult<Int32> }
type TaskStageResult { color?: str /* Цвет */, id?: int, name?: str }
type UserResult { avatarUrl?: str, deleted?: datetime, firstName?: str, id?: int, lastName?: str, middleName?: str }
```
