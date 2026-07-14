# WH — справочник ручек

> **Что здесь:** все ручки сервиса WH (API for WH in HubEx): сигнатуры, параметры, права. Типы — schemas/WH.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WH.md`; грабли — `notes/WH.md` (если есть).
> **Источник:** `snapshots/WH.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/WH`

## BarcodeTypes
- `GET /BarcodeTypes` — Возвращает полный список типов штрихкодов · права: BarcodeTypesList
  → map<BarcodeTypes.ListResult>

## DocumentStatuses
- `GET /DocumentStatuses` — Возвращает полный список статусов складских документов · права: DocumentStatusesList
  → map<DocumentStatuses.ListResult>

## DocumentTypes
- `GET /DocumentTypes` — Возвращает полный список типов складских документов · права: DocumentTypesList
  → map<DocumentTypes.ListResult>

## Inventories
- `GET /Inventories` — Возвращает список инвентаризаций · права: InventoryList · paginated
  ← query: validFrom?:any, validTill?:any → map<Inventories.ListResult>
- `POST /Inventories` — Добавляет точку инвентаризации · права: InventoryAdd
  ← body: Inventory.AddData[] → Inventories.PostResult[]
- `PUT /Inventories` — Изменяет точку инвентаризации · права: InventoryUpdate
  ← body: Inventory.UpdateData[]
- `DELETE /Inventories` — Удаляет точки инвентаризации · права: InventoryDelete
  ← body: int[]
- `GET /Inventories/actual` — Возвращает информацию о последней инвентаризации · права: InventoryGetActual
  → Inventories.ListResult
- `DELETE /Inventories/{id}` — Удаляет точку инвентаризации · права: InventoryDelete
  ← path: id:int

## Issues
- `GET /Issues` — Метод получения списка списаний материалов · права: IssueList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, responsiblePersonID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<IssueResult>
- `POST /Issues` — Метод для создания списаний материалов · права: IssueAdd
  ← body: Issue.AddData[] → int[]
- `PUT /Issues` — Метод изменения списаний материалов · права: IssueUpdate
  ← body: Issue.UpdateData[]
- `DELETE /Issues` — Метод для удаления списаний материалов · права: IssueDelete
  ← body: int[]
- `HEAD /Issues` — Метод получения общего количества списаний материалов · права: IssueList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, responsiblePersonID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<IssueResult>
- `POST /Issues/items` — Добавляет строки к документам списания материалов · права: IssueAdd
  ← body: IssueItemMergeData[]
- `DELETE /Issues/items` — Удаляет строки у документов списания материалов · права: IssueDelete
  ← body: IssueItemDeleteData[]
- `PUT /Issues/post` — Метод для проведения списаний материалов · права: IssuePost
  ← body: int[]
- `PUT /Issues/restore` — Метод для восстановления списаний материалов из удаленных · права: IssueRestore
  ← body: int[]
- `PUT /Issues/unpost` — Метод для отмены проведения списаний материалов · права: IssueUnpost
  ← body: int[]
- `GET /Issues/{id}` — Метод получения детальной информации об списании материалов · права: IssueGet
  ← path: id:int → IssueResult
- `DELETE /Issues/{id}` — Метод для удаления списаний материалов · права: IssueDelete
  ← path: id:int
- `PUT /Issues/{id}/post` — Метод для проведения списания материалов · права: IssuePost
  ← path: id:int
- `PUT /Issues/{id}/restore` — Метод для восстановления списания материалов из удаленных · права: IssueRestore
  ← path: id:int
- `PUT /Issues/{id}/unpost` — Метод для отмены проведения списания материалов · права: IssueUnpost
  ← path: id:int
- `GET /Issues/{issueID}/items` — Возвращает список строк для документа списания материалов · права: IssueList · paginated
  ← path: issueID:int → IssueItems.ListResult[]
- `DELETE /Issues/{issueID}/items/{materialID}` — Удаляет строки у документа списания материалов · права: IssueDelete
  ← path: issueID:int, materialID:int

## MaterialConsumptions
- `GET /MaterialConsumptions` — Возвращает список израсходованных материалов. · права: MaterialConsumptionListForTenantMember · paginated
  ← query: searchText?:str, orderBy?:any, sortDirection?:any, assetID?:any, taskTypeID?:any, workTypeID?:any, warehouseID?:any, consumedByUserID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<MaterialInventoryResult>

## Materials
- `GET /Materials` — Возвращает список материалов · права: MaterialListForTenantMember · paginated
  ← query: searchText?:str, orderBy?:any, sortDirection?:any, warehouseID?:any, inventoryDate?:any, materialID?:any, warehouseAssignedTo?:any → Materials.ListResult[]
- `POST /Materials` — Метод для создания материалов · права: MaterialAdd
  ← body: Material.AddData[] → int[]
- `PUT /Materials` — Метод изменения материалов · права: MaterialUpdate
  ← body: Material.UpdateData[]
- `DELETE /Materials` — Метод для удаления материалов · права: MaterialDelete
  ← body: int[]
- `HEAD /Materials` — Методо получения общего количества материалов · права: MaterialList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false) → map<MaterialListResult>
- `POST /Materials/barcodes` — Добавляет штрихкоды к материалам · права: MaterialBarcodeAdd
  ← body: MaterialBarcode.AddData[] → MaterialBarcodes.PostResult
- `PUT /Materials/barcodes` — Изменяет штрихкоды у материалов · права: MaterialBarcodeUpdate
  ← body: MaterialBarcode.UpdateData[]
- `DELETE /Materials/barcodes` — Удаляет штрихкоды у материалов · права: MaterialBarcodeDelete
  ← body: MaterialActionData<Int16>[]
- `PUT /Materials/restore` — Метод для восстановления материалов из удаленных · права: MaterialRestore
  ← body: int[]
- `GET /Materials/v2` — Метод получения списка материалов · права: MaterialList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), isMarkable?:enum(true, false) → map<MaterialListResult>
- `GET /Materials/{id}` — Метод получения детальной информации о материале · права: MaterialGet
  ← path: id:int → MaterialResult
- `DELETE /Materials/{id}` — Метод для удаления материала · права: MaterialDelete
  ← path: id:int
- `PUT /Materials/{id}/restore` — Метод для восстановления материала из удаленных · права: MaterialRestore · paginated
  ← path: id:int
- `GET /Materials/{materialID}/attachment/{attachmentID}` — Метод получения прикрепленного к материалу файла вложения
<param name="materialID">Идентификатор материала</param><param name="attachmentID">Идентификатор прикрепленного файла к договору</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: MaterialAttachmentGet
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int → MaterialAttachmentResult
- `DELETE /Materials/{materialID}/attachment/{attachmentID}` — Метод помечает связку материла и вложения как удаленную · права: MaterialAttachmentDelete
  ← path: materialID:int, attachmentID:int
- `GET /Materials/{materialID}/attachments` — Метод получения списка файлов вложений прикрепленных к материалу
<param name="materialID">Идентификатор материала</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · права: MaterialAttachmentList · paginated
  ← path: materialID:int; query: thumbnailSize?:int → map<MaterialAttachmentListResult>
- `POST /Materials/{materialID}/attachments` — Метод связывающий материал и вложение · права: MaterialAttachmentAdd
  ← path: materialID:int; body: int[] → MaterialAttachmentPostResult[]
- `DELETE /Materials/{materialID}/attachments` — Метод помечает связку материала и вложения как удаленную · права: MaterialAttachmentDelete
  ← path: materialID:int; body: int[]
- `POST /Materials/{materialID}/attachments/upload/fromBody` — Метод загружает файл на файловый сервер и привязывает его к материалу. Данные будут получены из тела запроса. · права: MaterialAttachmentUpload
  ← path: materialID:int; body: FromBodyUploadData → UploadResult
- `POST /Materials/{materialID}/attachments/upload/fromForm` — Метод загружает файлы на файловый сервер и привязывает его к материалу. Данные будут получены из формы. · права: MaterialAttachmentUpload
  ← path: materialID:int; body: { Attachments?: FromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → UploadResult
- `GET /Materials/{materialID}/attachments/{attachmentID}` — Метод получения TemporaryRedirect на временную ссылку для скачки файла · права: MaterialAttachmentDownload
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Materials/{materialID}/barcodes` — Возвращает список штрихкодов для материалов · права: MaterialBarcodesList · paginated
  ← path: materialID:int → map<MaterialBarcodes.ListResult[]>
- `DELETE /Materials/{materialID}/barcodes/{barcodeID}` — Удаляет штрихкоды у материала · права: MaterialBarcodeDelete
  ← path: materialID:int, barcodeID:int
- `GET /Materials/{required}` — Возвращает список материалов · права: MaterialRequiredListForTenantMember · paginated
  ← path: required:str; query: searchText?:str, orderBy?:any, sortDirection?:any, warehouseID?:any, warehouseAssignedTo?:any, inventoryDate?:any → ListRequiredResult[]

## NumberSequences
- `GET /NumberSequences` — Возвращает список масок номеров складских документов · права: NumberSequenceList · paginated
  ← query: documentTypeID?:any → NumberSequenceResult[]
- `POST /NumberSequences` — Добавляет маски номеров докуметов · права: NumberSequenceAdd
  ← body: ModifyData[]
- `PUT /NumberSequences` — Изменяет маски номеров докуметов · права: NumberSequenceUpdate
  ← body: ModifyData[]
- `GET /NumberSequences/{documentTypeId}` — Возвращает информацию о маске номера складского документа · права: NumberSequenceGet
  ← path: documentTypeId:int → NumberSequenceResult

## OperationTypes
- `GET /OperationTypes` — Возвращает список типов операций · права: OperationTypeList · paginated
  ← query: documentTypeID?:any, isDeleted?:enum(true, false) → map<OperationTypeResult>
- `POST /OperationTypes` — Добавляет типы операций · права: OperationTypeAdd
  ← body: OperationType.AddData[] → OperationTypeAddResult[]
- `PUT /OperationTypes` — Изменяет типы операций · права: OperationTypeUpdate
  ← body: OperationType.UpdateData[]
- `DELETE /OperationTypes` — Удаляет типы операций · права: OperationTypeDelete
  ← body: int[]
- `GET /OperationTypes/{id}` — Возвращает информацию о типе операции · права: OperationTypeGet
  ← path: id:int → OperationTypeResult
- `DELETE /OperationTypes/{id}` — Удаляет тип операции · права: OperationTypeDelete
  ← path: id:int

## Receipts
- `GET /Receipts` — Метод получения списка оприходываний материалов · права: ReceiptList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any, responsiblePersonID?:any → map<ReceiptResult>
- `POST /Receipts` — Метод для оприходываний материалов · права: ReceiptAdd
  ← body: Receipt.AddData[] → int[]
- `PUT /Receipts` — Метод изменения оприходываний материалов · права: ReceiptUpdate
  ← body: Receipt.UpdateData[]
- `DELETE /Receipts` — Метод для удаления оприходываний материалов · права: ReceiptDelete
  ← body: int[]
- `HEAD /Receipts` — Метод получения общего количества оприходываний материалов · права: ReceiptList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<ReceiptResult>
- `POST /Receipts/items` — Добавляет строки к документам оприходывания материалов · права: ReceiptAdd
  ← body: ReceiptItemMergeData[]
- `DELETE /Receipts/items` — Удаляет строки у документов оприходывания материалов · права: ReceiptDelete
  ← body: ReceiptItemDeleteData[]
- `PUT /Receipts/post` — Метод для проведения оприходываний материалов · права: ReceiptPost
  ← body: int[]
- `PUT /Receipts/restore` — Метод для восстановления оприходываний материалов из удаленных · права: ReceiptRestore
  ← body: int[]
- `PUT /Receipts/unpost` — Метод для для отмены проведения оприходываний материалов · права: ReceiptUnpost
  ← body: int[]
- `GET /Receipts/{id}` — Метод получения детальной информации об оприходывании материалов · права: ReceiptGet
  ← path: id:int → ReceiptResult
- `DELETE /Receipts/{id}` — Метод для удаления оприходывания материалов · права: ReceiptDelete
  ← path: id:int
- `PUT /Receipts/{id}/post` — Метод для проведения оприходывания материалов · права: ReceiptPost
  ← path: id:int
- `PUT /Receipts/{id}/restore` — Метод для восстановления оприходывания материалов из удаленных · права: ReceiptRestore
  ← path: id:int
- `PUT /Receipts/{id}/unpost` — Метод для отмены проведения оприходывания материалов · права: ReceiptUnpost
  ← path: id:int
- `GET /Receipts/{receiptID}/items` — Возвращает список строк для документа оприходывания материалов · права: ReceiptList · paginated
  ← path: receiptID:int → ReceiptItems.ListResult[]
- `DELETE /Receipts/{receiptID}/items/{materialID}` — Удаляет строки у документа оприходывания материалов · права: ReceiptDelete
  ← path: receiptID:int, materialID:int

## UserWarehouses
- `POST /UserWarehouses` — Добавляет множество складов к пользователям · права: UserWarehouseAdd
  ← body: UserWarehousesData[]
- `DELETE /UserWarehouses` — Удаляет множество складов у пользователя · права: UserWarehouseDelete
  ← body: UserWarehousesData[]
- `GET /UserWarehouses/{id}` — Возвращает полный список складов пользователя · права: UserWarehouseList · paginated
  ← path: id:int; query: searchText?:str → UserWarehouseListResult[]
- `POST /UserWarehouses/{id}` — Добавляет множество складов к пользователю · права: UserWarehouseAdd
  ← path: id:int; body: int[]
- `DELETE /UserWarehouses/{id}` — Удаляет множество складов у пользователя · права: UserWarehouseDelete
  ← path: id:int; body: int[]

## Warehouses
- `GET /Warehouses` — Метод получения списка складов · права: WarehousesList · paginated
  ← query: searchText?:str, isDefault?:enum(true, false), warehouseAssignedTo?:any → map<ListShortResult>
- `POST /Warehouses` — Метод для создания складов · права: WarehouseAdd
  ← query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:enum(true, false); body: Warehouse.AddData[] → int[]
- `PUT /Warehouses` — Метод изменения складов · права: WarehouseUpdate
  ← body: Warehouse.UpdateData[]
- `DELETE /Warehouses` — Метод для удаления складов · права: WarehouseDelete
  ← body: int[]
- `HEAD /Warehouses` — Методо получения общего количества складов · права: WarehousesList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false) → map<Warehouses.ListResult>
- `GET /Warehouses/V2` — Метод получения списка складов · права: WarehousesList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), isDefault?:enum(true, false), warehouseAssignedTo?:any → map<Warehouses.ListResult>
- `PUT /Warehouses/restore` — Метод для восстановления складов из удаленных · права: WarehouseRestore
  ← body: int[]
- `GET /Warehouses/short` — Метод получения списка складов · права: WarehousesList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), isDefault?:enum(true, false), warehouseAssignedTo?:any → map<ListShortResult>
- `POST /Warehouses/users` — Добавляет множество пользователей к складам · права: UserWarehouseAdd
  ← body: WarehouseUsersData[]
- `DELETE /Warehouses/users` — Удаляет множество пользователей у складов · права: UserWarehouseDelete
  ← body: WarehouseUsersDeleteData[]
- `GET /Warehouses/{id}` — Метод получения детальной информации о складе · права: WarehouseGet
  ← path: id:int → GetResult
- `DELETE /Warehouses/{id}` — Метод для удаления склада · права: WarehouseDelete
  ← path: id:int
- `PUT /Warehouses/{id}/restore` — Метод для восстановления склада из удаленных · права: WarehouseRestore
  ← path: id:int
- `GET /Warehouses/{id}/users` — Список пользователей склада · права: UserWarehouseList · paginated
  ← path: id:int; query: searchText?:str → WarehouseUserListResult[]
- `POST /Warehouses/{id}/users` — Добавляет множество пользователей к складу · права: UserWarehouseAdd
  ← path: id:int; query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:enum(true, false); body: int[]
- `DELETE /Warehouses/{id}/users` — Удаляет множество пользователей у склада · права: UserWarehouseDelete
  ← path: id:int; query: isRelatedToAnyUser?:bool, isRelatedToAnyUser?:enum(true, false); body: int[]
