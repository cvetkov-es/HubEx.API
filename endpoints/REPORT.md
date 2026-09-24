# REPORT — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса REPORT (API for REPORT in HubEx): сигнатуры, параметры, права. Типы — schemas/REPORT.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/REPORT.md`; грабли — `notes/REPORT.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/REPORT`
> Примеры ответов вынесены в [../examples/REPORT.md](../examples/REPORT.md).

**Оглавление**

- AssetMaintenance — строки 23–25
- CompletionTime — строки 27–29
- PowerBICustomReports — строки 31–33
- ReactionTime — строки 35–37
- TasksByAssets — строки 39–41
- TasksByAssignees — строки 43–45
- TasksByCompanies — строки 47–49
- TasksByStages — строки 51–53
- TasksByWorkTypes — строки 55–57
- WorkingTime — строки 59–61

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
