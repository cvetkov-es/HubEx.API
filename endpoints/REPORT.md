# REPORT — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса REPORT (API for REPORT in HubEx): сигнатуры, параметры, права. Типы — schemas/REPORT.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/REPORT.md`; грабли — `notes/REPORT.md` (если есть).
> **Источник:** swagger сервиса REPORT · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/REPORT`

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
