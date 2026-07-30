# WH — справочник ручек

> **Что здесь:** все ручки сервиса WH (API for WH in HubEx): сигнатуры, параметры, права. Типы — schemas/WH.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WH.md`; грабли — `notes/WH.md` (если есть).

Base: `{BASE_URL}/WH`
> Примеры ответов вынесены в [../examples/WH.md](../examples/WH.md).

**Оглавление**

- BarcodeTypes — строки 26–28
- DocumentStatuses — строки 30–32
- DocumentTypes — строки 34–36
- Documents — строки 38–40
- Inventories — строки 42–54
- Issues — строки 56–90
- MaterialConsumptions — строки 92–94
- Materials — строки 96–146
- NumberSequences — строки 148–156
- OperationTypes — строки 158–170
- Receipts — строки 172–206
- Transfers — строки 208–242
- UserWarehouses — строки 244–254
- Warehouses — строки 256–288

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
- `POST /Inventories` — Добавляет точку инвентаризации · коды: 201, 409
  ← body: WHInventoryAddData[] → ResultsInventoriesPostResult[]
- `PUT /Inventories` — Изменяет точку инвентаризации · коды: 202, 409
  ← body: WHInventoryUpdateData[]
- `DELETE /Inventories` — Удаляет точки инвентаризации · коды: 202
  ← body: int[]
- `GET /Inventories/actual` — Возвращает информацию о последней инвентаризации · коды: 200
  → ResultsInventoriesListResult
- `DELETE /Inventories/{id}` — Удаляет точку инвентаризации · коды: 202
  ← path: id:int

## Issues
- `GET /Issues` — Получение списка списаний материалов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, responsiblePersonID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime → map<ResultsIssuesIssueResult>
- `POST /Issues` — Создание списаний материалов · коды: 201, 409 · примеры
  ← body: WHIssueAddData[] → int[]
- `PUT /Issues` — Изменение списаний материалов · коды: 202, 409 · примеры
  ← body: WHIssueUpdateData[]
- `DELETE /Issues` — Удаление списаний материалов · коды: 202 · примеры
  ← body: int[]
- `HEAD /Issues` — Получение общего количества списаний материалов · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, responsiblePersonID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime
- `POST /Issues/items` — Добавляет строки к документам списания материалов · коды: 202, 409 · примеры
  ← body: WHIssueIssueItemMergeData[]
- `DELETE /Issues/items` — Удаляет строки у документов списания материалов · коды: 202, 409 · примеры
  ← body: WHIssueIssueItemDeleteData[]
- `PUT /Issues/post` — Проведение списаний материалов · коды: 202 · примеры
  ← body: int[]
- `PUT /Issues/restore` — Восстановление списаний материалов из удаленных · коды: 202 · примеры
  ← body: int[]
- `PUT /Issues/unpost` — Отмена проведения списаний материалов · коды: 202 · примеры
  ← body: int[]
- `GET /Issues/{id}` — Получение детальной информации о списании материалов · коды: 200, 204 · примеры
  ← path: id:int → ResultsIssuesIssueResult
- `DELETE /Issues/{id}` — Удаление списания материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Issues/{id}/post` — Проведение списания материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Issues/{id}/restore` — Восстановление списания материалов из удаленных по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Issues/{id}/unpost` — Отмена проведения списания материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `GET /Issues/{issueID}/items` — Возвращает список строк для документа списания материалов · коды: 200, 204 · примеры
  ← path: issueID:int → ResultsIssueItemsListResult[]
- `DELETE /Issues/{issueID}/items/{materialID}` — Удаляет строки у документа списания материалов · коды: 202, 409 · примеры
  ← path: issueID:int, materialID:int

## MaterialConsumptions
- `GET /MaterialConsumptions` — Возвращает список израсходованных материалов. · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:int, sortDirection?:int, assetID?:int, taskTypeID?:int, workTypeID?:int, warehouseID?:int, consumedByUserID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime → map<ResultsMaterialConsumptionsMaterialInventoryResult>

## Materials
- `GET /Materials` — Возвращает список материалов · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:int, sortDirection?:int, warehouseID?:int, inventoryDate?:datetime, materialID?:int, warehouseAssignedTo?:int → ResultsMaterialsListResult[]
- `POST /Materials` — Метод для создания материалов · коды: 201
  ← body: WHMaterialAddData[] → int[]
- `PUT /Materials` — Метод изменения материалов · коды: 202
  ← body: WHMaterialUpdateData[]
- `DELETE /Materials` — Метод для удаления материалов · коды: 202
  ← body: int[]
- `HEAD /Materials` — Методо получения общего количества материалов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool → map<ResultsMaterialsMaterialListResult>
- `POST /Materials/barcodes` — Добавляет штрихкоды к материалам · коды: 201, 409
  ← body: WHMaterialBarcodeAddData[] → ResultsMaterialBarcodesPostResult
- `PUT /Materials/barcodes` — Изменяет штрихкоды у материалов · коды: 202, 409
  ← body: WHMaterialBarcodeUpdateData[]
- `DELETE /Materials/barcodes` — Удаляет штрихкоды у материалов · коды: 202, 409
  ← body: MaterialActionDataOfShort[]
- `PUT /Materials/restore` — Метод для восстановления материалов из удаленных · коды: 202
  ← body: int[]
- `GET /Materials/v2` — Метод получения списка материалов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool, isMarkable?:bool → map<ResultsMaterialsMaterialListResult>
- `GET /Materials/{id}` — Метод получения детальной информации о материале · коды: 200
  ← path: id:int → ResultsMaterialsMaterialResult
- `DELETE /Materials/{id}` — Метод для удаления материала · коды: 202, 409
  ← path: id:int
- `PUT /Materials/{id}/restore` — Метод для восстановления материала из удаленных · paginated · коды: 202, 206, 409
  ← path: id:int
- `GET /Materials/{materialID}/attachment/{attachmentID}` — Метод получения прикрепленного к материалу файла вложения
<param name="materialID">Идентификатор материала</param><param name="attachmentID">Идентификатор прикрепленного файла к договору</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · коды: 200, 500
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int → ResultsMaterialAttachmentsMaterialAttachmentResult
- `DELETE /Materials/{materialID}/attachment/{attachmentID}` — Метод помечает связку материла и вложения как удаленную · коды: 202, 500
  ← path: materialID:int, attachmentID:int
- `GET /Materials/{materialID}/attachments` — Метод получения списка файлов вложений прикрепленных к материалу
<param name="materialID">Идентификатор материала</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · коды: 200, 500
  ← path: materialID:int; query: thumbnailSize?:int → map<ResultsMaterialAttachmentsMaterialAttachmentListResult>
- `POST /Materials/{materialID}/attachments` — Метод связывающий материал и вложение · коды: 201, 500
  ← path: materialID:int; body: int[] → ResultsMaterialAttachmentsMaterialAttachmentPostResult[]
- `DELETE /Materials/{materialID}/attachments` — Метод помечает связку материала и вложения как удаленную · коды: 202, 500
  ← path: materialID:int; body: int[]
- `POST /Materials/{materialID}/attachments/upload/fromBody` — Метод загружает файл на файловый сервер и привязывает его к материалу. Данные будут получены из тела запроса. · коды: 201, 500
  ← path: materialID:int; body: DataAttachmentsFromBodyUploadData → ResultsMaterialAttachmentsUploadResult
- `POST /Materials/{materialID}/attachments/upload/fromForm` — Метод загружает файлы на файловый сервер и привязывает его к материалу. Данные будут получены из формы. · коды: 201, 500
  ← path: materialID:int; body: { Attachments?: DataAttachmentsFromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → ResultsMaterialAttachmentsUploadResult
- `GET /Materials/{materialID}/attachments/{attachmentID}` — Метод получения TemporaryRedirect на временную ссылку для скачки файла · коды: 303
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Materials/{materialID}/barcodes` — Возвращает список штрихкодов для материалов · коды: 200, 400
  ← path: materialID:int → map<ResultsMaterialBarcodesListResult[]>
- `DELETE /Materials/{materialID}/barcodes/{barcodeID}` — Удаляет штрихкоды у материала · коды: 202, 409
  ← path: materialID:int, barcodeID:int
- `GET /Materials/{required}` — Возвращает список материалов · paginated · коды: 200, 206
  ← path: required:str; query: searchText?:str, orderBy?:int, sortDirection?:int, warehouseID?:int, warehouseAssignedTo?:int, inventoryDate?:datetime → ResultsMaterialsListRequiredResult[]

## NumberSequences
- `GET /NumberSequences` — Возвращает список масок номеров складских документов · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:int → ResultsNumberSequencesNumberSequenceResult[]
- `POST /NumberSequences` — Добавляет маски номеров докуметов · коды: 409
  ← body: WHNumberSequenceModifyData[]
- `PUT /NumberSequences` — Изменяет маски номеров докуметов · коды: 202, 409
  ← body: WHNumberSequenceModifyData[]
- `GET /NumberSequences/{documentTypeId}` — Возвращает информацию о маске номера складского документа · коды: 200
  ← path: documentTypeId:int → ResultsNumberSequencesNumberSequenceResult

## OperationTypes
- `GET /OperationTypes` — Возвращает список типов операций · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:int, isDeleted?:bool → map<ResultsOperationTypesOperationTypeResult>
- `POST /OperationTypes` — Добавляет типы операций · коды: 201, 409
  ← body: WHOperationTypeAddData[] → ResultsOperationTypesOperationTypeAddResult[]
- `PUT /OperationTypes` — Изменяет типы операций · коды: 202, 409
  ← body: WHOperationTypeUpdateData[]
- `DELETE /OperationTypes` — Удаляет типы операций · коды: 202
  ← body: int[]
- `GET /OperationTypes/{id}` — Возвращает информацию о типе операции · коды: 200
  ← path: id:int → ResultsOperationTypesOperationTypeResult
- `DELETE /OperationTypes/{id}` — Удаляет тип операции · коды: 202
  ← path: id:int

## Receipts
- `GET /Receipts` — Получение списка оприходываний материалов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime, responsiblePersonID?:int → map<ResultsReceiptsReceiptResult>
- `POST /Receipts` — Создание оприходываний материалов · коды: 201, 409 · примеры
  ← body: WHReceiptAddData[] → int[]
- `PUT /Receipts` — Изменение оприходываний материалов · коды: 202, 409 · примеры
  ← body: WHReceiptUpdateData[]
- `DELETE /Receipts` — Удаление оприходываний материалов · коды: 202 · примеры
  ← body: int[]
- `HEAD /Receipts` — Получение общего количества оприходываний материалов · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, warehouseID?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime
- `POST /Receipts/items` — Добавляет строки к документам оприходывания материалов · коды: 202, 409 · примеры
  ← body: WHReceiptReceiptItemMergeData[]
- `DELETE /Receipts/items` — Удаляет строки у документов оприходывания материалов · коды: 202, 409 · примеры
  ← body: WHReceiptReceiptItemDeleteData[]
- `PUT /Receipts/post` — Проведение оприходываний материалов · коды: 202 · примеры
  ← body: int[]
- `PUT /Receipts/restore` — Восстановление оприходываний материалов из удаленных · коды: 202 · примеры
  ← body: int[]
- `PUT /Receipts/unpost` — Отмена проведения оприходываний материалов · коды: 202 · примеры
  ← body: int[]
- `GET /Receipts/{id}` — Получение детальной информации об оприходывании материалов · коды: 200, 204 · примеры
  ← path: id:int → ResultsReceiptsReceiptResult
- `DELETE /Receipts/{id}` — Удаление оприходывания материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Receipts/{id}/post` — Проведение оприходывания материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Receipts/{id}/restore` — Восстановление оприходывания материалов из удаленных по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Receipts/{id}/unpost` — Отмена проведения оприходывания материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `GET /Receipts/{receiptID}/items` — Возвращает список строк для документа оприходывания материалов · коды: 200, 204 · примеры
  ← path: receiptID:int → ResultsReceiptItemsListResult[]
- `DELETE /Receipts/{receiptID}/items/{materialID}` — Удаляет строки у документа оприходывания материалов · коды: 202, 409 · примеры
  ← path: receiptID:int, materialID:int

## Transfers
- `GET /Transfers` — Получение списка перемещений материалов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, fromWarehouses?:int, toWarehouses?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime, responsiblePersonID?:int → map<ResultsTransfersTransferResult>
- `POST /Transfers` — Создание перемещений материалов · коды: 201, 409 · примеры
  ← body: WHTransferAddData[] → int[]
- `PUT /Transfers` — Изменение перемещений материалов · коды: 202, 409 · примеры
  ← body: WHTransferUpdateData[]
- `DELETE /Transfers` — Удаление перемещений материалов · коды: 202, 409 · примеры
  ← body: int[]
- `HEAD /Transfers` — Получение общего количества перемещений материалов · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, fromWarehouses?:int, toWarehouses?:int, documentStatusID?:int, operationTypeID?:int, consumptionPeriodFrom?:datetime, consumptionPeriodTill?:datetime
- `POST /Transfers/items` — Добавляет данные к документам перемещения материалов · коды: 202, 409 · примеры
  ← body: WHTransferTransferItemMergeData[]
- `DELETE /Transfers/items` — Удаляет данные у документов перемещения материалов · коды: 202, 409 · примеры
  ← body: WHTransferTransferItemDeleteData[]
- `PUT /Transfers/post` — Проведение перемещений материалов · коды: 202, 409 · примеры
  ← body: int[]
- `PUT /Transfers/restore` — Восстановление удаленных перемещений материалов · коды: 202, 409 · примеры
  ← body: int[]
- `PUT /Transfers/unpost` — Отмена проведения перемещений материалов · коды: 202, 409 · примеры
  ← body: int[]
- `GET /Transfers/{id}` — Получение детальной информации о перемещении материалов · коды: 200, 204 · примеры
  ← path: id:int → ResultsTransfersTransferResult
- `DELETE /Transfers/{id}` — Удаление перемещения материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Transfers/{id}/post` — Проведение перемещения материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Transfers/{id}/restore` — Восстановление удаленного перемещения материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /Transfers/{id}/unpost` — Отмена проведения перемещения материалов по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
- `GET /Transfers/{transferID}/items` — Возвращает список данных для документа перемещения материалов · коды: 200, 204 · примеры
  ← path: transferID:int → ResultsTransferItemsListResult[]
- `DELETE /Transfers/{transferID}/items/{materialID}` — Удаляет данные у документа перемещения материалов · коды: 202, 409 · примеры
  ← path: transferID:int, materialID:int

## UserWarehouses
- `POST /UserWarehouses` — Добавляет множество складов к пользователям · коды: 201, 500
  ← body: WHWarehouseUserUserWarehousesData[]
- `DELETE /UserWarehouses` — Удаляет множество складов у пользователя · коды: 202, 500
  ← body: WHWarehouseUserUserWarehousesData[]
- `GET /UserWarehouses/{id}` — Возвращает полный список складов пользователя · коды: 200
  ← path: id:int; query: searchText?:str → ResultsWarehouseUsersUserWarehouseListResult[]
- `POST /UserWarehouses/{id}` — Добавляет множество складов к пользователю · коды: 201, 500
  ← path: id:int; body: int[]
- `DELETE /UserWarehouses/{id}` — Удаляет множество складов у пользователя · коды: 201, 500
  ← path: id:int; body: int[]

## Warehouses
- `GET /Warehouses` — Метод получения списка складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDefault?:bool, warehouseAssignedTo?:int → map<ResultsWarehousesListShortResult>
- `POST /Warehouses` — Метод для создания складов · коды: 201
  ← query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:bool; body: WHWarehouseAddData[] → int[]
- `PUT /Warehouses` — Метод изменения складов · коды: 202
  ← body: WHWarehouseUpdateData[]
- `DELETE /Warehouses` — Метод для удаления складов · коды: 202
  ← body: int[]
- `HEAD /Warehouses` — Методо получения общего количества складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool → map<ResultsWarehousesListResult>
- `GET /Warehouses/V2` — Метод получения списка складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool, isDefault?:bool, warehouseAssignedTo?:int → map<ResultsWarehousesListResult>
- `PUT /Warehouses/restore` — Метод для восстановления складов из удаленных · коды: 202
  ← body: int[]
- `GET /Warehouses/short` — Метод получения списка складов · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:bool, isDefault?:bool, warehouseAssignedTo?:int → map<ResultsWarehousesListShortResult>
- `POST /Warehouses/users` — Добавляет множество пользователей к складам · коды: 201, 500
  ← body: WHWarehouseUserWarehouseUsersData[]
- `DELETE /Warehouses/users` — Удаляет множество пользователей у складов · коды: 202, 500
  ← body: WHWarehouseUserWarehouseUsersDeleteData[]
- `GET /Warehouses/{id}` — Метод получения детальной информации о складе · коды: 200
  ← path: id:int → ResultsWarehousesGetResult
- `DELETE /Warehouses/{id}` — Метод для удаления склада · коды: 202, 409
  ← path: id:int
- `PUT /Warehouses/{id}/restore` — Метод для восстановления склада из удаленных · коды: 202, 409
  ← path: id:int
- `GET /Warehouses/{id}/users` — Список пользователей склада · paginated · коды: 200, 206
  ← path: id:int; query: searchText?:str → ResultsWarehouseUsersWarehouseUserListResult[]
- `POST /Warehouses/{id}/users` — Добавляет множество пользователей к складу · коды: 201, 500
  ← path: id:int; query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:bool; body: int[]
- `DELETE /Warehouses/{id}/users` — Удаляет множество пользователей у склада · коды: 201, 500
  ← path: id:int; query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:bool; body: int[]
