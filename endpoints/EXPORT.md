# EXPORT — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса EXPORT (API for data exporting in HubEx): сигнатуры, параметры, права. Типы — schemas/EXPORT.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/EXPORT.md`; грабли — `notes/EXPORT.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/EXPORT`
> Примеры ответов вынесены в [../examples/EXPORT.md](../examples/EXPORT.md).

**Оглавление**

- Assets — строки 19–25
- Companies — строки 27–29
- MaterialConsumption — строки 31–33
- Materials — строки 35–39
- Tasks — строки 41–53
- Users — строки 55–57

## Assets
- `GET /Assets` — Экспортирует список объектов с учетом указанных фильтров · коды: 200 · примеры
  ← query: searchText?:str, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, checkListID?:int, startWithAssetID?:int, noData?:bool, erpID?:str
- `GET /Assets/extended` — Экспортирует расширенный список объектов с учетом указанных фильтров · коды: 200, 500 · примеры
  ← query: include?:str[], searchText?:str, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, checkListID?:int, startWithAssetID?:int, noData?:bool, erpID?:str
- `GET /Assets/extended/includes` — Возвращает список данных, доступных для расширенного экспорта · коды: 200, 204, 206 · примеры
  ← query: searchText?:str → FieldResult[]

## Companies
- `GET /Companies` — Экспортирует список компаний с учетом указанных фильтров · коды: 200 · примеры
  ← query: searchText?:str, noData?:bool, erpID?:str

## MaterialConsumption
- `GET /MaterialConsumption` — Экспортирует список расходов материалов · коды: 200 · примеры
  ← query: searchText?:str, noData?:bool, assetID?:int, taskTypeID?:int, workTypeID?:int, warehouseID?:int, consumedByUserID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime

## Materials
- `GET /Materials` — Экспортирует список материалов · коды: 200 · примеры
  ← query: searchText?:str, warehouseID?:int, inventoryDate?:datetime, warehouseAssignedTo?:int, noData?:bool
- `GET /Materials/v2.0` — Экспортирует список материалов (версия 2.0 с постраничной загрузкой) · коды: 200 · примеры
  ← query: searchText?:str, warehouseID?:int, inventoryDate?:datetime, warehouseAssignedTo?:int, noData?:bool

## Tasks
- `GET /Tasks` — Экспортирует список заявок с учетом указанных фильтров · коды: 200 · примеры
  ← query: searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, isOutdated?:bool, companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:str, pointSouthWest?:str, pointCenter?:str, radius?:float, geoHash?:str, noData?:bool, erpID?:str
- `GET /Tasks/extended` — Экспортирует расширенный список заявок с учетом указанных фильтров · коды: 200, 500 · примеры
  ← query: include?:str[], searchText?:str, hideEmptyColumns?:bool, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, isOutdated?:bool, companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:str, pointSouthWest?:str, pointCenter?:str, radius?:float, geoHash?:str, noData?:bool, erpID?:str
- `GET /Tasks/extended/V2` — Экспортирует расширенный список заявок с учетом указанных фильтров (версия 2.0 с постраничной загрузкой) · коды: 200, 500 · примеры
  ← query: include?:str[], searchText?:str, hideEmptyColumns?:bool, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, isOutdated?:bool, companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:str, pointSouthWest?:str, pointCenter?:str, radius?:float, geoHash?:str, noData?:bool, erpID?:str
- `GET /Tasks/extended/includes` — Возвращает список данных, доступных для расширенного экспорта · коды: 200, 204, 206 · примеры
  ← query: searchText?:str → FieldResult[]
- `GET /Tasks/noData` — Экспортирует пустой шаблон для импорта заявок · коды: 200 · примеры
  ← query: searchText?:str
- `GET /Tasks/v2.0` — Экспортирует список заявок с учетом указанных фильтров (версия 2.0 с постраничной загрузкой) · коды: 200 · примеры
  ← query: searchText?:str, requestedBy?:int, assignedTo?:int, approvalWith?:int, escalatedTo?:int, assetID?:int, startWithAssetID?:int, taskID?:int, taskNumber?:str, taskTypeID?:int, workTypeID?:int, taskStageID?:int, taskStatusID?:int, creationFrom?:datetime, creationTill?:datetime, assignationFrom?:datetime, assignationTill?:datetime, completionFrom?:datetime, completionTill?:datetime, closingFrom?:datetime, closingTill?:datetime, deadlineFrom?:datetime, deadlineTill?:datetime, isClosed?:bool, isFavourite?:bool, isCompleted?:bool, isAssigned?:bool, isDeleted?:bool, isOutdated?:bool, companyID?:int, contractID?:int, criticalityID?:int, orderBy?:int, sortDirection?:int, pointNorthEast?:str, pointSouthWest?:str, pointCenter?:str, radius?:float, geoHash?:str, erpID?:str

## Users
- `GET /Users` — Экспортирует список пользователей с учетом указанных фильтров · коды: 200 · примеры
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, noData?:bool, erpID?:str
