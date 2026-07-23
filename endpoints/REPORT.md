# REPORT — справочник ручек

> **Что здесь:** все ручки сервиса REPORT (API for REPORT in HubEx): сигнатуры, параметры, права. Типы — schemas/REPORT.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/REPORT.md`; грабли — `notes/REPORT.md` (если есть).

Base: `{BASE_URL}/REPORT`

**Оглавление**

- AssetMaintenance — строки 21–23
- CompletionTime — строки 25–27
- PowerBICustomReports — строки 29–31
- ReactionTime — строки 33–35
- TasksByAssets — строки 37–39
- TasksByAssignees — строки 41–43
- TasksByCompanies — строки 45–47
- TasksByStages — строки 49–51
- TasksByWorkTypes — строки 53–55
- WorkingTime — строки 57–59

## AssetMaintenance
- `GET /AssetMaintenance/planned` — Возвращае запланированные заявки на обслуживание объектов, доступных пользователю · права: PreventiveAssetMaintenanceList · коды: 200
  ← query: validFrom?:any, validTill?:any → PlannedMaintenanceResult[]

## CompletionTime
- `GET /CompletionTime` — Возвращает список суммарного и среднего времени выполнения заявок, сгруппированных по периоду · права: TaskListCompletionTime · paginated · коды: 200, 206
  ← query: groupByPeriod?:DatePart, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByAssigneesResult[]

## PowerBICustomReports
- `GET /PowerBICustomReports` — Возвращает список кастомных отчетов тенанта · права: PowerBICustomReportList · paginated · коды: 200, 206
  → map<CustomReportList>

## ReactionTime
- `GET /ReactionTime` — Возвращает список суммарного и среднего времени реакции по заявкам, сгруппированным по периоду · права: TaskListReactionTime · paginated · коды: 200, 206
  ← query: groupByPeriod?:DatePart, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByAssigneesResult[]

## TasksByAssets
- `GET /TasksByAssets` — Возвращает список заявок, сгруппированных по оборудованию · права: TaskListGroupByAssets · paginated · коды: 200, 206
  ← query: searchText?:str, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByAssigneesResult[]

## TasksByAssignees
- `GET /TasksByAssignees` — Возвращает список заявок, сгруппированных по исполнителям · права: TaskListGroupByAssignees · paginated · коды: 200, 206
  ← query: searchText?:str, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByAssigneesResult[]

## TasksByCompanies
- `GET /TasksByCompanies` — Возвращает список заявок, сгруппированный по компаниям. · права: TaskListGroupByCompanies · paginated · коды: 200, 206
  ← query: searchText?:str, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByCompaniesResult[]

## TasksByStages
- `GET /TasksByStages` — Возвращает список заявок, сгруппированных по стадиям · права: TaskListGroupByStages · paginated · коды: 200, 206
  ← query: searchText?:str, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByStagesResult[]

## TasksByWorkTypes
- `GET /TasksByWorkTypes` — Возвращает список заявок, сгруппированных по видам работ · права: TaskListGroupByWorkTypes · paginated · коды: 200, 206
  ← query: searchText?:str, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByWorkTypesResult[]

## WorkingTime
- `GET /WorkingTime` — Возвращает список суммарного и среднего отработанного времени по заявокам, сгруппированным по периоду · права: TaskListWorkingTime · paginated · коды: 200, 206
  ← query: groupByPeriod?:DatePart, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any → TaskListGroupByAssigneesResult[]
