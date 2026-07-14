# REPORT — схемы

> **Что здесь:** определения типов запросов/ответов сервиса REPORT. Ручки, ссылающиеся на них — `endpoints/REPORT.md`.
> **Источник:** `snapshots/REPORT.json` · файл генерируется пайплайном — руками не править.

```
type AssetResult { id?: int, name?: str, host?: IdNameDeletedResult<Int32>, deleted?: datetime, parentID?: int }
type CustomReportList { name?: str /* Название отчета */, reportID?: str /* Идентификатор отчета */, reportType?: IdNameResult<Byte> }
type DatePart enum(Year, Quarter, Month, Day, Week, Second, Minute, Hour)
type IdNameDeletedResult<Int32> { id?: int, name?: str, deleted?: datetime }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type PlannedMaintenanceResult { taskTemplateID?: str /* Идентификатор шаблона заявки */, appointment?: datetime /* Метка времени (UTC) события */, normalWorkingHours?: int /* Трудозатраты в нормочасах */, normalWorkingMinutes?: int /* Трудозатраты в нормоминутах */, workType?: IdNameResult<Int16>, taskType?: IdNameResult<Byte>, frequencyType?: IdNameResult<Byte>, assetClass?: IdNameResult<Byte>, assetType?: IdNameResult<Byte>, asset?: AssetResult }
type TaskListGroupByAssigneesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */, total?: int /* Общее количество заявок */, assignee?: UserResult }
type TaskListGroupByCompaniesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */, total?: int /* Общее количество заявок */, company?: IdNameResult<Int32> }
type TaskListGroupByStagesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */, total?: int /* Общее количество заявок */, taskStage?: TaskStageResult }
type TaskListGroupByWorkTypesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */, total?: int /* Общее количество заявок */, workType?: IdNameResult<Int32> }
type TaskStageResult { id?: int, name?: str, color?: str /* Цвет */ }
type UserResult { id?: int, firstName?: str, lastName?: str, middleName?: str, avatarUrl?: str, deleted?: datetime }
```
