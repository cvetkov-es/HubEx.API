# WH — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса WH (API for WH in HubEx): сигнатуры, параметры, права. Типы — schemas/WH.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WH.md`; грабли — `notes/WH.md` (если есть).
> **Источник:** swagger сервиса WH · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/WH`

**Оглавление**

- BarcodeTypes — строки 25–27
- DocumentStatuses — строки 29–31
- DocumentTypes — строки 33–35
- Inventories — строки 37–41
- Issues — строки 43–51
- MaterialConsumptions — строки 53–55
- Materials — строки 57–77
- NumberSequences — строки 79–83
- OperationTypes — строки 85–89
- Receipts — строки 91–99
- UserWarehouses — строки 101–103
- Warehouses — строки 105–117

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
- `GET /Inventories/actual` — Возвращает информацию о последней инвентаризации · права: InventoryGetActual · коды: 200
  → Inventories.ListResult

## Issues
- `GET /Issues` — Метод получения списка списаний материалов · права: IssueList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, responsiblePersonID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<IssueResult>
- `HEAD /Issues` — Метод получения общего количества списаний материалов · права: IssueList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, responsiblePersonID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<IssueResult>
- `GET /Issues/{id}` — Метод получения детальной информации об списании материалов · права: IssueGet · коды: 200
  ← path: id:int → IssueResult
- `GET /Issues/{issueID}/items` — Возвращает список строк для документа списания материалов · права: IssueList · paginated · коды: 200, 206, 400
  ← path: issueID:int → IssueItems.ListResult[]

## MaterialConsumptions
- `GET /MaterialConsumptions` — Возвращает список израсходованных материалов. · права: MaterialConsumptionListForTenantMember · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:any, sortDirection?:any, assetID?:any, taskTypeID?:any, workTypeID?:any, warehouseID?:any, consumedByUserID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<MaterialInventoryResult>

## Materials
- `GET /Materials` — Возвращает список материалов · права: MaterialListForTenantMember · paginated · коды: 200, 206
  ← query: searchText?:str, orderBy?:any, sortDirection?:any, warehouseID?:any, inventoryDate?:any, materialID?:any, warehouseAssignedTo?:any → Materials.ListResult[]
- `HEAD /Materials` — Методо получения общего количества материалов · права: MaterialList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false) → map<MaterialListResult>
- `GET /Materials/v2` — Метод получения списка материалов · права: MaterialList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), isMarkable?:enum(true, false) → map<MaterialListResult>
- `GET /Materials/{id}` — Метод получения детальной информации о материале · права: MaterialGet · коды: 200
  ← path: id:int → MaterialResult
- `GET /Materials/{materialID}/attachment/{attachmentID}` — Метод получения прикрепленного к материалу файла вложения
<param name="materialID">Идентификатор материала</param><param name="attachmentID">Идентификатор прикрепленного файла к договору</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: MaterialAttachmentGet · коды: 200, 500
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int → MaterialAttachmentResult
- `GET /Materials/{materialID}/attachments` — Метод получения списка файлов вложений прикрепленных к материалу
<param name="materialID">Идентификатор материала</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · права: MaterialAttachmentList · paginated · коды: 200, 206, 500
  ← path: materialID:int; query: thumbnailSize?:int → map<MaterialAttachmentListResult>
- `GET /Materials/{materialID}/attachments/{attachmentID}` — Метод получения TemporaryRedirect на временную ссылку для скачки файла · права: MaterialAttachmentDownload · коды: 303
  ← path: materialID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Materials/{materialID}/barcodes` — Возвращает список штрихкодов для материалов · права: MaterialBarcodesList · paginated · коды: 200, 206, 400
  ← path: materialID:int → map<MaterialBarcodes.ListResult[]>
- `GET /Materials/{required}` — Возвращает список материалов · права: MaterialRequiredListForTenantMember · paginated · коды: 200, 206
  ← path: required:str; query: searchText?:str, orderBy?:any, sortDirection?:any, warehouseID?:any, warehouseAssignedTo?:any, inventoryDate?:any → ListRequiredResult[]

## NumberSequences
- `GET /NumberSequences` — Возвращает список масок номеров складских документов · права: NumberSequenceList · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:any → NumberSequenceResult[]
- `GET /NumberSequences/{documentTypeId}` — Возвращает информацию о маске номера складского документа · права: NumberSequenceGet · коды: 200
  ← path: documentTypeId:int → NumberSequenceResult

## OperationTypes
- `GET /OperationTypes` — Возвращает список типов операций · права: OperationTypeList · paginated · коды: 200, 206, 500
  ← query: documentTypeID?:any, isDeleted?:enum(true, false) → map<OperationTypeResult>
- `GET /OperationTypes/{id}` — Возвращает информацию о типе операции · права: OperationTypeGet · коды: 200
  ← path: id:int → OperationTypeResult

## Receipts
- `GET /Receipts` — Метод получения списка оприходываний материалов · права: ReceiptList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any, responsiblePersonID?:any → map<ReceiptResult>
- `HEAD /Receipts` — Метод получения общего количества оприходываний материалов · права: ReceiptList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), warehouseID?:any, documentStatusID?:any, operationTypeID?:any, consumptionPeriodFrom?:any, consumptionPeriodTill?:any → map<ReceiptResult>
- `GET /Receipts/{id}` — Метод получения детальной информации об оприходывании материалов · права: ReceiptGet · коды: 200
  ← path: id:int → ReceiptResult
- `GET /Receipts/{receiptID}/items` — Возвращает список строк для документа оприходывания материалов · права: ReceiptList · paginated · коды: 200, 206, 400
  ← path: receiptID:int → ReceiptItems.ListResult[]

## UserWarehouses
- `GET /UserWarehouses/{id}` — Возвращает полный список складов пользователя · права: UserWarehouseList · paginated · коды: 200, 206
  ← path: id:int; query: searchText?:str → UserWarehouseListResult[]

## Warehouses
- `GET /Warehouses` — Метод получения списка складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDefault?:enum(true, false), warehouseAssignedTo?:any → map<ListShortResult>
- `HEAD /Warehouses` — Методо получения общего количества складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false) → map<Warehouses.ListResult>
- `GET /Warehouses/V2` — Метод получения списка складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), isDefault?:enum(true, false), warehouseAssignedTo?:any → map<Warehouses.ListResult>
- `GET /Warehouses/short` — Метод получения списка складов · права: WarehousesList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), isDefault?:enum(true, false), warehouseAssignedTo?:any → map<ListShortResult>
- `GET /Warehouses/{id}` — Метод получения детальной информации о складе · права: WarehouseGet · коды: 200
  ← path: id:int → GetResult
- `GET /Warehouses/{id}/users` — Список пользователей склада · права: UserWarehouseList · paginated · коды: 200, 206
  ← path: id:int; query: searchText?:str → WarehouseUserListResult[]
