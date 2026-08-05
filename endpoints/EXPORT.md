# EXPORT — справочник ручек

> **Что здесь:** все ручки сервиса EXPORT (API for data exporting in HubEx): сигнатуры, параметры, права. Типы — schemas/EXPORT.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/EXPORT.md`; грабли — `notes/EXPORT.md` (если есть).

Base: `{BASE_URL}/EXPORT`

**Оглавление**

- Assets — строки 17–23
- Companies — строки 25–27
- MaterialConsumption — строки 29–31
- Materials — строки 33–37
- Tasks — строки 39–51
- Users — строки 53–55

## Assets
- `GET /Assets` — Экспортирует список объектов с учетом указанных фильтров · права: AssetsExport · коды: 200
  ← query: searchText?:str, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:enum(true, false), isAssigned?:any, isDeleted?:enum(true, false), isPublished?:enum(true, false), warrantyFrom?:datetime, warrantyTill?:datetime, checkListID?:int, startWithAssetID?:int, noData?:enum(true, false), erpID?:str
- `GET /Assets/extended` — Экспортирует список объектов с учетом указанных фильтров · права: AssetsExport · коды: 200
  ← query: include?:str[], searchText?:str, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:enum(true, false), isAssigned?:any, isDeleted?:enum(true, false), isPublished?:enum(true, false), warrantyFrom?:datetime, warrantyTill?:datetime, checkListID?:int, startWithAssetID?:int, noData?:enum(true, false), erpID?:str
- `GET /Assets/extended/includes` — Возвращает список данных, доступных для расширенного экспорта · права: AssetsExport · paginated · коды: 200, 206
  ← query: searchText?:str → FieldResult[]

## Companies
- `GET /Companies` — Экспортирует список компаний с учетом указанных фильтров · права: CompaniesExport · коды: 200
  ← query: searchText?:str, noData?:enum(true, false), erpID?:str

## MaterialConsumption
- `GET /MaterialConsumption` — Экспортирует список расходов материалов · права: MaterialConsumptionList · коды: 200
  ← query: searchText?:str, noData?:enum(true, false), assetID?:int, taskTypeID?:int, workTypeID?:int, warehouseID?:int, consumedByUserID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime

## Materials
- `GET /Materials` — Экспортирует список материалов · права: MaterialList · коды: 200
  ← query: searchText?:str, warehouseID?:int, inventoryDate?:datetime, warehouseAssignedTo?:int, noData?:enum(true, false)
- `GET /Materials/v2.0` — Экспортирует список материалов (версия 2.0 с постраничной загрузкой) · права: MaterialList · коды: 200
  ← query: searchText?:str, warehouseID?:int, inventoryDate?:datetime, warehouseAssignedTo?:int, noData?:enum(true, false)

## Tasks
- `GET /Tasks` — Экспортирует список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:coordinate, pointSouthWest?:coordinate, pointCenter?:coordinate, radius?:float, geoHash?:str, noData?:enum(true, false), erpID?:str
- `GET /Tasks/extended` — Экспортирует расширенный список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: include?:str[], searchText?:str, hideEmptyColumns?:bool, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:coordinate, pointSouthWest?:coordinate, pointCenter?:coordinate, radius?:float, geoHash?:str, noData?:enum(true, false), erpID?:str, hideEmptyColumns?:enum(true, false)
- `GET /Tasks/extended/V2` — Экспортирует расширенный список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: include?:str[], searchText?:str, hideEmptyColumns?:bool, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:coordinate, pointSouthWest?:coordinate, pointCenter?:coordinate, radius?:float, geoHash?:str, noData?:enum(true, false), erpID?:str, hideEmptyColumns?:enum(true, false)
- `GET /Tasks/extended/includes` — Возвращает список данных, доступных для расширенного экспорта · права: TasksExport · paginated · коды: 200, 206
  ← query: searchText?:str → FieldResult[]
- `GET /Tasks/noData` — Экспортирует пустой шаблон для импорта заявок · права: TasksExport · коды: 200
  ← query: searchText?:str
- `GET /Tasks/v2.0` — Экспортирует список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:coordinate, pointSouthWest?:coordinate, pointCenter?:coordinate, radius?:float, geoHash?:str, erpID?:str

## Users
- `GET /Users` — Экспортирует список пользователей с учетом указанных фильтров · права: UsersExport · коды: 200
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:enum(true, false), isCustomer?:enum(true, false), isTeam?:enum(true, false), isTechnician?:enum(true, false), firstName?:str, lastName?:str, middleName?:str, position?:str, noData?:enum(true, false), erpID?:str
