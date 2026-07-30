# WH — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса WH (API for WH in HubEx): сигнатуры, параметры, права. Типы — schemas/WH.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WH.md`; грабли — `notes/WH.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/WH`
> Примеры ответов вынесены в [../examples/WH.md](../examples/WH.md).

**Оглавление**

- BarcodeTypes — строки 27–29
- DocumentStatuses — строки 31–33
- DocumentTypes — строки 35–37
- Documents — строки 39–41
- Inventories — строки 43–47
- Issues — строки 49–57
- MaterialConsumptions — строки 59–61
- Materials — строки 63–83
- NumberSequences — строки 85–89
- OperationTypes — строки 91–95
- Receipts — строки 97–105
- Transfers — строки 107–115
- UserWarehouses — строки 117–119
- Warehouses — строки 121–133

## BarcodeTypes
- `GET /BarcodeTypes` — Возвращает полный список типов штрихкодов · коды: 200
  → map<ResultsBarcodeTypesListResult>

## DocumentStatuses
- `GET /DocumentStatuses` — Возвращает полный список статусов складских документов · коды: 200
  → map<ResultsDocumentStatusesListResult>

## DocumentTypes
- `GET /DocumentTypes` — Возвращает полный список типов складских документов · коды: 200
  → map<ResultsDocumentTypesListResult>

## Documents
- `GET /Documents` — Получение списка складских документов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, isPosted?:bool, documentTypeID?:int, documentStatusID?:int, operationTypeID?:int, fromWarehouses?:int, toWarehouses?:int, responsiblePersonID?:int, creationFrom?:datetime, creationTill?:datetime, modifiedFrom?:datetime, modifiedTill?:datetime, documentDateFrom?:datetime, documentDateTill?:datetime, orderBy?:int, sortDirection?:int → ResultsDocumentsDocumentResult[]

## Inventories
- `GET /Inventories` — Возвращает список инвентаризаций · paginated · коды: 200, 206, 500
  ← query: validFrom?:datetime, validTill?:datetime → map<ResultsInventoriesListResult>
- `GET /Inventories/actual` — Возвращает информацию о последней инвентаризации · коды: 200
  → ResultsInventoriesListResult

## Issues
- `GET /Issues` — Получение списка списаний материалов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, responsiblePersonID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime → map<ResultsIssuesIssueResult>
- `HEAD /Issues` — Получение общего количества списаний материалов · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, responsiblePersonID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime
- `GET /Issues/{id}` — Получение детальной информации о списании материалов · коды: 200, 204 · примеры
  ← path: id:int → ResultsIssuesIssueResult
- `GET /Issues/{issueID}/items` — Возвращает список строк для документа списания материалов · коды: 200, 204 · примеры
  ← path: issueID:int → ResultsIssueItemsListResult[]

## MaterialConsumptions
- `GET /MaterialConsumptions` — Возвращает список израсходованных материалов. · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:int, sortDirection?:int, assetID?:int, taskTypeID?:int, workTypeID?:int, warehouseID?:int, consumedByUserID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime → map<ResultsMaterialConsumptionsMaterialInventoryResult>

## Materials
- `GET /Materials` — Возвращает список материалов · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:int, sortDirection?:int, warehouseID?:int, inventoryDate?:datetime, materialID?:int, warehouseAssignedTo?:int → ResultsMaterialsListResult[]
- `HEAD /Materials` — Методо получения общего количества материалов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool → map<ResultsMaterialsMaterialListResult>
- `GET /Materials/v2` — Метод получения списка материалов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool, isMarkable?:bool → map<ResultsMaterialsMaterialListResult>
- `GET /Materials/{id}` — Метод получения детальной информации о материале · коды: 200
  ← path: id:int → ResultsMaterialsMaterialResult
- `GET /Materials/{materialID}/attachment/{attachmentID}` — Метод получения прикрепленного к материалу файла вложения
<param name="materialID">Идентификатор материала</param><param name="attachmentID">Идентификатор прикрепленного файла к договору</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · коды: 200, 500
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int → ResultsMaterialAttachmentsMaterialAttachmentResult
- `GET /Materials/{materialID}/attachments` — Метод получения списка файлов вложений прикрепленных к материалу
<param name="materialID">Идентификатор материала</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · коды: 200, 500
  ← path: materialID:int; query: thumbnailSize?:int → map<ResultsMaterialAttachmentsMaterialAttachmentListResult>
- `GET /Materials/{materialID}/attachments/{attachmentID}` — Метод получения TemporaryRedirect на временную ссылку для скачки файла · коды: 303
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Materials/{materialID}/barcodes` — Возвращает список штрихкодов для материалов · коды: 200, 400
  ← path: materialID:int → map<ResultsMaterialBarcodesListResult[]>
- `GET /Materials/{required}` — Возвращает список материалов · paginated · коды: 200, 206
  ← path: required:str; query: searchText?:str, orderBy?:int, sortDirection?:int, warehouseID?:int, warehouseAssignedTo?:int, inventoryDate?:datetime → ResultsMaterialsListRequiredResult[]

## NumberSequences
- `GET /NumberSequences` — Возвращает список масок номеров складских документов · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:int → ResultsNumberSequencesNumberSequenceResult[]
- `GET /NumberSequences/{documentTypeId}` — Возвращает информацию о маске номера складского документа · коды: 200
  ← path: documentTypeId:int → ResultsNumberSequencesNumberSequenceResult

## OperationTypes
- `GET /OperationTypes` — Возвращает список типов операций · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:int, isDeleted?:bool → map<ResultsOperationTypesOperationTypeResult>
- `GET /OperationTypes/{id}` — Возвращает информацию о типе операции · коды: 200
  ← path: id:int → ResultsOperationTypesOperationTypeResult

## Receipts
- `GET /Receipts` — Получение списка оприходываний материалов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime, responsiblePersonID?:int → map<ResultsReceiptsReceiptResult>
- `HEAD /Receipts` — Получение общего количества оприходываний материалов · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime
- `GET /Receipts/{id}` — Получение детальной информации об оприходывании материалов · коды: 200, 204 · примеры
  ← path: id:int → ResultsReceiptsReceiptResult
- `GET /Receipts/{receiptID}/items` — Возвращает список строк для документа оприходывания материалов · коды: 200, 204 · примеры
  ← path: receiptID:int → ResultsReceiptItemsListResult[]

## Transfers
- `GET /Transfers` — Получение списка перемещений материалов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, fromWarehouses?:int, toWarehouses?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime, responsiblePersonID?:int → map<ResultsTransfersTransferResult>
- `HEAD /Transfers` — Получение общего количества перемещений материалов · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, fromWarehouses?:int, toWarehouses?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime
- `GET /Transfers/{id}` — Получение детальной информации о перемещении материалов · коды: 200, 204 · примеры
  ← path: id:int → ResultsTransfersTransferResult
- `GET /Transfers/{transferID}/items` — Возвращает список данных для документа перемещения материалов · коды: 200, 204 · примеры
  ← path: transferID:int → ResultsTransferItemsListResult[]

## UserWarehouses
- `GET /UserWarehouses/{id}` — Возвращает полный список складов пользователя · коды: 200
  ← path: id:int; query: searchText?:str → ResultsWarehouseUsersUserWarehouseListResult[]

## Warehouses
- `GET /Warehouses` — Метод получения списка складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDefault?:bool, warehouseAssignedTo?:int → map<ResultsWarehousesListShortResult>
- `HEAD /Warehouses` — Методо получения общего количества складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool → map<ResultsWarehousesListResult>
- `GET /Warehouses/V2` — Метод получения списка складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool, isDefault?:bool, warehouseAssignedTo?:int → map<ResultsWarehousesListResult>
- `GET /Warehouses/short` — Метод получения списка складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool, isDefault?:bool, warehouseAssignedTo?:int → map<ResultsWarehousesListShortResult>
- `GET /Warehouses/{id}` — Метод получения детальной информации о складе · коды: 200
  ← path: id:int → ResultsWarehousesGetResult
- `GET /Warehouses/{id}/users` — Список пользователей склада · paginated · коды: 200, 206
  ← path: id:int; query: searchText?:str → ResultsWarehouseUsersWarehouseUserListResult[]
