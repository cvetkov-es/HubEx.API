# REPORT — схемы

> **Что здесь:** определения типов запросов/ответов сервиса REPORT. Ручки, ссылающиеся на них — `endpoints/REPORT.md`.

```
type ApiEnumsDatePart enum(Year, Quarter, Month, Day, Week, Second, Minute, Hour)
type AspNetCoreResultsAssetResult { deleted?: datetime, host?: IdNameDeletedResultOfInt, id?: int, name?: str, parentID?: int }
type AspNetCoreResultsUserResult { avatarUrl?: str, deleted?: datetime, firstName?: str, id?: int, lastName?: str, middleName?: str }
type CommonResultsPeriodResult { from?: datetime, till?: datetime }
type IdNameDeletedResultOfInt { deleted?: datetime, id?: int, name?: str }
type IdNameResultOfByte { id?: int, name?: str }
type IdNameResultOfInt { id?: int, name?: str }
type IdNameResultOfShort { id?: int, name?: str }
type ResultsAssetMaintenancePlannedMaintenanceResult { appointment?: datetime /* Метка времени (UTC) события */, asset?: AspNetCoreResultsAssetResult, assetClass?: IdNameResultOfByte, assetType?: IdNameResultOfByte, frequencyType?: IdNameResultOfByte, normalWorkingHours?: int /* Трудозатраты в нормочасах */, normalWorkingMinutes?: int /* Трудозатраты в нормоминутах */, taskTemplateID?: str /* Идентификатор шаблона заявки */, taskType?: IdNameResultOfByte, workType?: IdNameResultOfShort }
type ResultsBaseBaseListTimeResult { averageMinutes?: float /* Среднее количество минут */, totalMinutes?: int /* общее количество минут */ }
type ResultsCompletionTimeCompletionTimeResult { completionTime?: ResultsBaseBaseListTimeResult, period?: CommonResultsPeriodResult }
type ResultsPowerBICustomReportsCustomReportList { name?: str /* Название отчета */, reportID?: str /* Идентификатор отчета */, reportType?: IdNameResultOfByte }
type ResultsReactionTimeReactionTimeResult { period?: CommonResultsPeriodResult, reactionTime?: ResultsBaseBaseListTimeResult }
type ResultsTaskListGroupByAssetsTasksListGroupByAssetsResult { activeTasksCount?: int /* Количество активных заявок */, asset?: IdNameResultOfInt, outdatedTasksCount?: int /* Количество просроченных заявок */, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */ }
type ResultsTaskListGroupByAssigneesTaskListGroupByAssigneesResult { activeTasksCount?: int /* Количество активных заявок */, assignee?: AspNetCoreResultsUserResult, outdatedTasksCount?: int /* Количество просроченных заявок */, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */ }
type ResultsTaskListGroupByCompaniesTaskListGroupByCompaniesResult { activeTasksCount?: int /* Количество активных заявок */, company?: IdNameResultOfInt, outdatedTasksCount?: int /* Количество просроченных заявок */, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */ }
type ResultsTaskListGroupByStagesTaskListGroupByStagesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, taskStage?: ResultsTaskListGroupByStagesTaskStageResult, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */ }
type ResultsTaskListGroupByStagesTaskStageResult { color?: str /* Цвет */, id?: int, name?: str }
type ResultsTaskListGroupByWorkTypesTaskListGroupByWorkTypesResult { activeTasksCount?: int /* Количество активных заявок */, outdatedTasksCount?: int /* Количество просроченных заявок */, total?: int /* Общее количество заявок */, undefinedTasksCount?: int /* Количество неопределенных заявок */, workType?: IdNameResultOfInt }
type ResultsWorkingTimeWorkingTimeResult { period?: CommonResultsPeriodResult, workingTime?: ResultsBaseBaseListTimeResult }
```
