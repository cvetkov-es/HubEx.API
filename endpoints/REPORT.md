# REPORT — справочник ручек

> **Что здесь:** все ручки сервиса REPORT (API for REPORT in HubEx): сигнатуры, параметры, права. Типы — schemas/REPORT.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/REPORT.md`; грабли — `notes/REPORT.md` (если есть).

Base: `{BASE_URL}/REPORT`
> Примеры ответов вынесены в [../examples/REPORT.md](../examples/REPORT.md).

**Оглавление**

- AssetMaintenance — строки 22–24
- CompletionTime — строки 26–28
- PowerBICustomReports — строки 30–32
- ReactionTime — строки 34–36
- TasksByAssets — строки 38–40
- TasksByAssignees — строки 42–44
- TasksByCompanies — строки 46–48
- TasksByStages — строки 50–52
- TasksByWorkTypes — строки 54–56
- WorkingTime — строки 58–60

## AssetMaintenance
- `GET /AssetMaintenance/planned` — Получение запланированных заявок на обслуживание объектов · коды: 200, 204 · примеры
  ← query: validFrom?:datetime, validTill?:datetime → ResultsAssetMaintenancePlannedMaintenanceResult[]

## CompletionTime
- `GET /CompletionTime` — Получение отчета по времени выполнения заявок · коды: 200, 204, 206, 400 · примеры
  ← query: groupByPeriod?:ApiEnumsDatePart, groupByPeriod:enum(Year, Quarter, Month, Day, Week, Second, Minute, Hour), requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsCompletionTimeCompletionTimeResult[]

## PowerBICustomReports
- `GET /PowerBICustomReports` — Получение списка кастомных отчетов PowerBI · коды: 200, 204, 206 · примеры
  → map<ResultsPowerBICustomReportsCustomReportList>

## ReactionTime
- `GET /ReactionTime` — Получение отчета по времени реакции на заявки · коды: 200, 204, 206, 400 · примеры
  ← query: groupByPeriod?:ApiEnumsDatePart, groupByPeriod:enum(Year, Quarter, Month, Day, Week, Second, Minute, Hour), requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsReactionTimeReactionTimeResult[]

## TasksByAssets
- `GET /TasksByAssets` — Получение отчета по заявкам, сгруппированным по оборудованию · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsTaskListGroupByAssetsTasksListGroupByAssetsResult[]

## TasksByAssignees
- `GET /TasksByAssignees` — Получение отчета по заявкам, сгруппированным по исполнителям · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsTaskListGroupByAssigneesTaskListGroupByAssigneesResult[]

## TasksByCompanies
- `GET /TasksByCompanies` — Получение отчета по заявкам, сгруппированным по компаниям · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsTaskListGroupByCompaniesTaskListGroupByCompaniesResult[]

## TasksByStages
- `GET /TasksByStages` — Получение отчета по заявкам, сгруппированным по стадиям · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsTaskListGroupByStagesTaskListGroupByStagesResult[]

## TasksByWorkTypes
- `GET /TasksByWorkTypes` — Получение отчета по заявкам, сгруппированным по видам работ · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsTaskListGroupByWorkTypesTaskListGroupByWorkTypesResult[]

## WorkingTime
- `GET /WorkingTime` — Получение отчета по отработанному времени по заявкам · коды: 200, 204, 206, 400 · примеры
  ← query: groupByPeriod?:ApiEnumsDatePart, groupByPeriod:enum(Year, Quarter, Month, Day, Week, Second, Minute, Hour), requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, companyID?:int, contractID?:int, criticalityID?:int → ResultsWorkingTimeWorkingTimeResult[]
