# EXPORT — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса EXPORT (API for data exporting in HubEx): сигнатуры, параметры, права. Типы — schemas/EXPORT.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/EXPORT.md`; грабли — `notes/EXPORT.md` (если есть).
> **Источник:** swagger сервиса EXPORT · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/EXPORT`

**Оглавление**

- Assets — строки 19–25
- Companies — строки 27–29
- MaterialConsumption — строки 31–33
- Materials — строки 35–39
- Tasks — строки 41–53
- Users — строки 55–57

## Assets
- `GET /Assets` — Экспортирует список объектов с учетом указанных фильтров · права: AssetsExport · коды: 200
  ← query: searchText?:str, parentID?:any, assetID?:any, responsiblePerson?:any, districtID?:any, workTypeID?:any, skillID?:any, companyID?:any, taskTypeID?:any, tag?:str, name?:str, isMobile?:enum(true, false), isAssigned?:any, isDeleted?:enum(true, false), isPublished?:enum(true, false), warrantyFrom?:any, warrantyTill?:any, checkListID?:any, startWithAssetID?:any, noData?:enum(true, false), erpID?:str
- `GET /Assets/extended` — Экспортирует список объектов с учетом указанных фильтров · права: AssetsExport · коды: 200
  ← query: include?:str[], searchText?:str, parentID?:any, assetID?:any, responsiblePerson?:any, districtID?:any, workTypeID?:any, skillID?:any, companyID?:any, taskTypeID?:any, tag?:str, name?:str, isMobile?:enum(true, false), isAssigned?:any, isDeleted?:enum(true, false), isPublished?:enum(true, false), warrantyFrom?:any, warrantyTill?:any, checkListID?:any, startWithAssetID?:any, noData?:enum(true, false), erpID?:str
- `GET /Assets/extended/includes` — Возвращает список данных, доступных для расширенного экспорта · права: AssetsExport · paginated · коды: 200, 206
  ← query: searchText?:str → FieldResult[]

## Companies
- `GET /Companies` — Экспортирует список компаний с учетом указанных фильтров · права: CompaniesExport · коды: 200
  ← query: searchText?:str, noData?:enum(true, false), erpID?:str

## MaterialConsumption
- `GET /MaterialConsumption` — Экспортирует список расходов материалов · права: MaterialConsumptionList · коды: 200
  ← query: searchText?:str, noData?:enum(true, false), assetID?:any, taskTypeID?:any, workTypeID?:any, warehouseID?:any, consumedByUserID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any

## Materials
- `GET /Materials` — Экспортирует список материалов · права: MaterialList · коды: 200
  ← query: searchText?:str, warehouseID?:any, inventoryDate?:any, warehouseAssignedTo?:any, noData?:enum(true, false)
- `GET /Materials/v2.0` — Экспортирует список материалов (версия 2.0 с постраничной загрузкой) · права: MaterialList · коды: 200
  ← query: searchText?:str, warehouseID?:any, inventoryDate?:any, warehouseAssignedTo?:any, noData?:enum(true, false)

## Tasks
- `GET /Tasks` — Экспортирует список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: searchText?:str, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, noData?:enum(true, false), erpID?:str
- `GET /Tasks/extended` — Экспортирует расширенный список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: include?:str[], searchText?:str, hideEmptyColumns?:bool, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, noData?:enum(true, false), erpID?:str, hideEmptyColumns?:enum(true, false)
- `GET /Tasks/extended/V2` — Экспортирует расширенный список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: include?:str[], searchText?:str, hideEmptyColumns?:bool, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, noData?:enum(true, false), erpID?:str, hideEmptyColumns?:enum(true, false)
- `GET /Tasks/extended/includes` — Возвращает список данных, доступных для расширенного экспорта · права: TasksExport · paginated · коды: 200, 206
  ← query: searchText?:str → FieldResult[]
- `GET /Tasks/noData` — Экспортирует пустой шаблон для импорта заявок · права: TasksExport · коды: 200
  ← query: searchText?:str
- `GET /Tasks/v2.0` — Экспортирует список заявок с учетом указанных фильтров · права: TasksExport · коды: 200
  ← query: searchText?:str, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, erpID?:str

## Users
- `GET /Users` — Экспортирует список пользователей с учетом указанных фильтров · права: UsersExport · коды: 200
  ← query: searchText?:str, orgUnitID?:any, districtID?:any, userID?:any, workTypeID?:any, skillID?:any, tag?:str, isDeleted?:enum(true, false), isCustomer?:enum(true, false), isTeam?:enum(true, false), isTechnician?:enum(true, false), firstName?:str, lastName?:str, middleName?:str, position?:str, noData?:enum(true, false), erpID?:str
