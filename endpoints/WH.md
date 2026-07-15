# WH — справочник ручек

> **Что здесь:** все ручки сервиса WH (API for WH in HubEx): сигнатуры, параметры, права. Типы — schemas/WH.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WH.md`; грабли — `notes/WH.md` (если есть).
> **Источник:** swagger сервиса WH · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/WH`

## BarcodeTypes
- `GET /BarcodeTypes` — Возвращает полный список типов штрихкодов · права: BarcodeTypesList · коды: 200
  → map<BarcodeTypes.ListResult>

## DocumentStatuses
- `GET /DocumentStatuses` — Возвращает полный список статусов складских документов · права: DocumentStatusesList · коды: 200
  → map<DocumentStatuses.ListResult>

## DocumentTypes
- `GET /DocumentTypes` — Возвращает полный список типов складских документов · права: DocumentTypesList · коды: 200
  → map<DocumentTypes.ListResult>

## Inventories
- `GET /Inventories` — Возвращает список инвентаризаций · права: InventoryList · paginated · коды: 200, 206, 500
  ← query: validFrom?:any, validTill?:any → map<Inventories.ListResult>
- `POST /Inventories` — Добавляет точку инвентаризации · права: InventoryAdd · коды: 201, 409
  ← body: Inventory.AddData[] → Inventories.PostResult[]
- `PUT /Inventories` — Изменяет точку инвентаризации · права: InventoryUpdate · коды: 202, 409
  ← body: Inventory.UpdateData[]
- `DELETE /Inventories` — Удаляет точки инвентаризации · права: InventoryDelete · коды: 202
  ← body: int[]
- `GET /Inventories/actual` — Возвращает информацию о последней инвентаризации · права: InventoryGetActual · коды: 200
  → Inventories.ListResult
- `DELETE /Inventories/{id}` — Удаляет точку инвентаризации · права: InventoryDelete · коды: 202
  ← path: id:int

## Issues
- `GET /Issues` — Метод получения списка списаний материалов · права: IssueList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, responsiblePersonID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<IssueResult>
- `POST /Issues` — Метод для создания списаний материалов · права: IssueAdd · коды: 201, 409
  ← body: Issue.AddData[] → int[]
- `PUT /Issues` — Метод изменения списаний материалов · права: IssueUpdate · коды: 202, 409
  ← body: Issue.UpdateData[]
- `DELETE /Issues` — Метод для удаления списаний материалов · права: IssueDelete · коды: 202
  ← body: int[]
- `HEAD /Issues` — Метод получения общего количества списаний материалов · права: IssueList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, responsiblePersonID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<IssueResult>
- `POST /Issues/items` — Добавляет строки к документам списания материалов · права: IssueAdd · коды: 202, 409
  ← body: IssueItemMergeData[]
- `DELETE /Issues/items` — Удаляет строки у документов списания материалов · права: IssueDelete · коды: 202, 409
  ← body: IssueItemDeleteData[]
- `PUT /Issues/post` — Метод для проведения списаний материалов · права: IssuePost · коды: 202
  ← body: int[]
- `PUT /Issues/restore` — Метод для восстановления списаний материалов из удаленных · права: IssueRestore · коды: 202
  ← body: int[]
- `PUT /Issues/unpost` — Метод для отмены проведения списаний материалов · права: IssueUnpost · коды: 202
  ← body: int[]
- `GET /Issues/{id}` — Метод получения детальной информации об списании материалов · права: IssueGet · коды: 200
  ← path: id:int → IssueResult
- `DELETE /Issues/{id}` — Метод для удаления списаний материалов · права: IssueDelete · коды: 202, 409
  ← path: id:int
- `PUT /Issues/{id}/post` — Метод для проведения списания материалов · права: IssuePost · коды: 202, 409
  ← path: id:int
- `PUT /Issues/{id}/restore` — Метод для восстановления списания материалов из удаленных · права: IssueRestore · коды: 202, 409
  ← path: id:int
- `PUT /Issues/{id}/unpost` — Метод для отмены проведения списания материалов · права: IssueUnpost · коды: 202, 409
  ← path: id:int
- `GET /Issues/{issueID}/items` — Возвращает список строк для документа списания материалов · права: IssueList · paginated · коды: 200, 206, 400
  ← path: issueID:int → IssueItems.ListResult[]
- `DELETE /Issues/{issueID}/items/{materialID}` — Удаляет строки у документа списания материалов · права: IssueDelete · коды: 202, 409
  ← path: issueID:int, materialID:int

## MaterialConsumptions
- `GET /MaterialConsumptions` — Возвращает список израсходованных материалов. · права: MaterialConsumptionListForTenantMember · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:any, sortDirection?:any, assetID?:any, taskTypeID?:any, workTypeID?:any, warehouseID?:any, consumedByUserID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<MaterialInventoryResult>

## Materials
- `GET /Materials` — Возвращает список материалов · права: MaterialListForTenantMember · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:any, sortDirection?:any, warehouseID?:any, inventoryDate?:any, materialID?:any, warehouseAssignedTo?:any → Materials.ListResult[]
- `POST /Materials` — Метод для создания материалов · права: MaterialAdd · коды: 201
  ← body: Material.AddData[] → int[]
- `PUT /Materials` — Метод изменения материалов · права: MaterialUpdate · коды: 202
  ← body: Material.UpdateData[]
- `DELETE /Materials` — Метод для удаления материалов · права: MaterialDelete · коды: 202
  ← body: int[]
- `HEAD /Materials` — Методо получения общего количества материалов · права: MaterialList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false) → map<MaterialListResult>
- `POST /Materials/barcodes` — Добавляет штрихкоды к материалам · права: MaterialBarcodeAdd · коды: 201, 409
  ← body: MaterialBarcode.AddData[] → MaterialBarcodes.PostResult
- `PUT /Materials/barcodes` — Изменяет штрихкоды у материалов · права: MaterialBarcodeUpdate · коды: 202, 409
  ← body: MaterialBarcode.UpdateData[]
- `DELETE /Materials/barcodes` — Удаляет штрихкоды у материалов · права: MaterialBarcodeDelete · коды: 202, 409
  ← body: MaterialActionData<Int16>[]
- `PUT /Materials/restore` — Метод для восстановления материалов из удаленных · права: MaterialRestore · коды: 202
  ← body: int[]
- `GET /Materials/v2` — Метод получения списка материалов · права: MaterialList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), isMarkable?:enum(true, false) → map<MaterialListResult>
- `GET /Materials/{id}` — Метод получения детальной информации о материале · права: MaterialGet · коды: 200
  ← path: id:int → MaterialResult
- `DELETE /Materials/{id}` — Метод для удаления материала · права: MaterialDelete · коды: 202, 409
  ← path: id:int
- `PUT /Materials/{id}/restore` — Метод для восстановления материала из удаленных · права: MaterialRestore · paginated · коды: 202, 206, 409
  ← path: id:int
- `GET /Materials/{materialID}/attachment/{attachmentID}` — Метод получения прикрепленного к материалу файла вложения
<param name="materialID">Идентификатор материала</param><param name="attachmentID">Идентификатор прикрепленного файла к договору</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: MaterialAttachmentGet · коды: 200, 500
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int → MaterialAttachmentResult
- `DELETE /Materials/{materialID}/attachment/{attachmentID}` — Метод помечает связку материла и вложения как удаленную · права: MaterialAttachmentDelete · коды: 202, 500
  ← path: materialID:int, attachmentID:int
- `GET /Materials/{materialID}/attachments` — Метод получения списка файлов вложений прикрепленных к материалу
<param name="materialID">Идентификатор материала</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · права: MaterialAttachmentList · paginated · коды: 200, 206, 500
  ← path: materialID:int; query: thumbnailSize?:int → map<MaterialAttachmentListResult>
- `POST /Materials/{materialID}/attachments` — Метод связывающий материал и вложение · права: MaterialAttachmentAdd · коды: 201, 500
  ← path: materialID:int; body: int[] → MaterialAttachmentPostResult[]
- `DELETE /Materials/{materialID}/attachments` — Метод помечает связку материала и вложения как удаленную · права: MaterialAttachmentDelete · коды: 202, 500
  ← path: materialID:int; body: int[]
- `POST /Materials/{materialID}/attachments/upload/fromBody` — Метод загружает файл на файловый сервер и привязывает его к материалу. Данные будут получены из тела запроса. · права: MaterialAttachmentUpload · коды: 201, 500
  ← path: materialID:int; body: FromBodyUploadData → UploadResult
- `POST /Materials/{materialID}/attachments/upload/fromForm` — Метод загружает файлы на файловый сервер и привязывает его к материалу. Данные будут получены из формы. · права: MaterialAttachmentUpload · коды: 201, 500
  ← path: materialID:int; body: { Attachments?: FromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → UploadResult
- `GET /Materials/{materialID}/attachments/{attachmentID}` — Метод получения TemporaryRedirect на временную ссылку для скачки файла · права: MaterialAttachmentDownload · коды: 303
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Materials/{materialID}/barcodes` — Возвращает список штрихкодов для материалов · права: MaterialBarcodesList · paginated · коды: 200, 206, 400
  ← path: materialID:int → map<MaterialBarcodes.ListResult[]>
- `DELETE /Materials/{materialID}/barcodes/{barcodeID}` — Удаляет штрихкоды у материала · права: MaterialBarcodeDelete · коды: 202, 409
  ← path: materialID:int, barcodeID:int
- `GET /Materials/{required}` — Возвращает список материалов · права: MaterialRequiredListForTenantMember · paginated · коды: 200, 206
  ← path: required:str; query: searchText?:str, orderBy?:any, sortDirection?:any, warehouseID?:any, warehouseAssignedTo?:any, inventoryDate?:any → ListRequiredResult[]

## NumberSequences
- `GET /NumberSequences` — Возвращает список масок номеров складских документов · права: NumberSequenceList · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:any → NumberSequenceResult[]
- `POST /NumberSequences` — Добавляет маски номеров докуметов · права: NumberSequenceAdd · коды: 409
  ← body: ModifyData[]
- `PUT /NumberSequences` — Изменяет маски номеров докуметов · права: NumberSequenceUpdate · коды: 202, 409
  ← body: ModifyData[]
- `GET /NumberSequences/{documentTypeId}` — Возвращает информацию о маске номера складского документа · права: NumberSequenceGet · коды: 200
  ← path: documentTypeId:int → NumberSequenceResult

## OperationTypes
- `GET /OperationTypes` — Возвращает список типов операций · права: OperationTypeList · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:any, isDeleted?:enum(true, false) → map<OperationTypeResult>
- `POST /OperationTypes` — Добавляет типы операций · права: OperationTypeAdd · коды: 201, 409
  ← body: OperationType.AddData[] → OperationTypeAddResult[]
- `PUT /OperationTypes` — Изменяет типы операций · права: OperationTypeUpdate · коды: 202, 409
  ← body: OperationType.UpdateData[]
- `DELETE /OperationTypes` — Удаляет типы операций · права: OperationTypeDelete · коды: 202
  ← body: int[]
- `GET /OperationTypes/{id}` — Возвращает информацию о типе операции · права: OperationTypeGet · коды: 200
  ← path: id:int → OperationTypeResult
- `DELETE /OperationTypes/{id}` — Удаляет тип операции · права: OperationTypeDelete · коды: 202
  ← path: id:int

## Receipts
- `GET /Receipts` — Метод получения списка оприходываний материалов · права: ReceiptList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any, responsiblePersonID?:any → map<ReceiptResult>
- `POST /Receipts` — Метод для оприходываний материалов · права: ReceiptAdd · коды: 201
  ← body: Receipt.AddData[] → int[]
- `PUT /Receipts` — Метод изменения оприходываний материалов · права: ReceiptUpdate · коды: 202
  ← body: Receipt.UpdateData[]
- `DELETE /Receipts` — Метод для удаления оприходываний материалов · права: ReceiptDelete · коды: 202
  ← body: int[]
- `HEAD /Receipts` — Метод получения общего количества оприходываний материалов · права: ReceiptList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<ReceiptResult>
- `POST /Receipts/items` — Добавляет строки к документам оприходывания материалов · права: ReceiptAdd · коды: 202, 409
  ← body: ReceiptItemMergeData[]
- `DELETE /Receipts/items` — Удаляет строки у документов оприходывания материалов · права: ReceiptDelete · коды: 202, 409
  ← body: ReceiptItemDeleteData[]
- `PUT /Receipts/post` — Метод для проведения оприходываний материалов · права: ReceiptPost · коды: 202
  ← body: int[]
- `PUT /Receipts/restore` — Метод для восстановления оприходываний материалов из удаленных · права: ReceiptRestore · коды: 202
  ← body: int[]
- `PUT /Receipts/unpost` — Метод для для отмены проведения оприходываний материалов · права: ReceiptUnpost · коды: 202
  ← body: int[]
- `GET /Receipts/{id}` — Метод получения детальной информации об оприходывании материалов · права: ReceiptGet · коды: 200
  ← path: id:int → ReceiptResult
- `DELETE /Receipts/{id}` — Метод для удаления оприходывания материалов · права: ReceiptDelete · коды: 202, 409
  ← path: id:int
- `PUT /Receipts/{id}/post` — Метод для проведения оприходывания материалов · права: ReceiptPost · коды: 202, 409
  ← path: id:int
- `PUT /Receipts/{id}/restore` — Метод для восстановления оприходывания материалов из удаленных · права: ReceiptRestore · коды: 202, 409
  ← path: id:int
- `PUT /Receipts/{id}/unpost` — Метод для отмены проведения оприходывания материалов · права: ReceiptUnpost · коды: 202, 409
  ← path: id:int
- `GET /Receipts/{receiptID}/items` — Возвращает список строк для документа оприходывания материалов · права: ReceiptList · paginated · коды: 200, 206, 400
  ← path: receiptID:int → ReceiptItems.ListResult[]
- `DELETE /Receipts/{receiptID}/items/{materialID}` — Удаляет строки у документа оприходывания материалов · права: ReceiptDelete · коды: 202, 409
  ← path: receiptID:int, materialID:int

## UserWarehouses
- `POST /UserWarehouses` — Добавляет множество складов к пользователям · права: UserWarehouseAdd · коды: 201, 500
  ← body: UserWarehousesData[]
- `DELETE /UserWarehouses` — Удаляет множество складов у пользователя · права: UserWarehouseDelete · коды: 202, 500
  ← body: UserWarehousesData[]
- `GET /UserWarehouses/{id}` — Возвращает полный список складов пользователя · права: UserWarehouseList · paginated · коды: 200, 206
  ← path: id:int; query: searchText?:str → UserWarehouseListResult[]
- `POST /UserWarehouses/{id}` — Добавляет множество складов к пользователю · права: UserWarehouseAdd · коды: 201, 500
  ← path: id:int; body: int[]
- `DELETE /UserWarehouses/{id}` — Удаляет множество складов у пользователя · права: UserWarehouseDelete · коды: 201, 500
  ← path: id:int; body: int[]

## Warehouses
- `GET /Warehouses` — Метод получения списка складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDefault?:enum(true, false), warehouseAssignedTo?:any → map<ListShortResult>
- `POST /Warehouses` — Метод для создания складов · права: WarehouseAdd · коды: 201
  ← query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:enum(true, false); body: Warehouse.AddData[] → int[]
- `PUT /Warehouses` — Метод изменения складов · права: WarehouseUpdate · коды: 202
  ← body: Warehouse.UpdateData[]
- `DELETE /Warehouses` — Метод для удаления складов · права: WarehouseDelete · коды: 202
  ← body: int[]
- `HEAD /Warehouses` — Методо получения общего количества складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false) → map<Warehouses.ListResult>
- `GET /Warehouses/V2` — Метод получения списка складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), isDefault?:enum(true, false), warehouseAssignedTo?:any → map<Warehouses.ListResult>
- `PUT /Warehouses/restore` — Метод для восстановления складов из удаленных · права: WarehouseRestore · коды: 202
  ← body: int[]
- `GET /Warehouses/short` — Метод получения списка складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), isDefault?:enum(true, false), warehouseAssignedTo?:any → map<ListShortResult>
- `POST /Warehouses/users` — Добавляет множество пользователей к складам · права: UserWarehouseAdd · коды: 201, 500
  ← body: WarehouseUsersData[]
- `DELETE /Warehouses/users` — Удаляет множество пользователей у складов · права: UserWarehouseDelete · коды: 202, 500
  ← body: WarehouseUsersDeleteData[]
- `GET /Warehouses/{id}` — Метод получения детальной информации о складе · права: WarehouseGet · коды: 200
  ← path: id:int → GetResult
- `DELETE /Warehouses/{id}` — Метод для удаления склада · права: WarehouseDelete · коды: 202, 409
  ← path: id:int
- `PUT /Warehouses/{id}/restore` — Метод для восстановления склада из удаленных · права: WarehouseRestore · коды: 202, 409
  ← path: id:int
- `GET /Warehouses/{id}/users` — Список пользователей склада · права: UserWarehouseList · paginated · коды: 200, 206
  ← path: id:int; query: searchText?:str → WarehouseUserListResult[]
- `POST /Warehouses/{id}/users` — Добавляет множество пользователей к складу · права: UserWarehouseAdd · коды: 201, 500
  ← path: id:int; query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:enum(true, false); body: int[]
- `DELETE /Warehouses/{id}/users` — Удаляет множество пользователей у склада · права: UserWarehouseDelete · коды: 201, 500
  ← path: id:int; query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:enum(true, false); body: int[]
