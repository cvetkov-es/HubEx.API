# WH — схемы

> **Что здесь:** определения типов запросов/ответов сервиса WH. Ручки, ссылающиеся на них — `endpoints/WH.md`.

```
type AssetResult { deleted?: datetime, host?: IdNameDeletedResult<Int32>, id?: int, name?: str }
type BarcodeAddData { barcodeTypeID?: int, value: str }
type BarcodeTypes.ListResult { name?: str /* Имя типа штрихкода */ }
type BarcodeUpdateData { barcodeTypeID?: int, id?: int, value: str }
type CountryResult { id?: int, name?: str, twoSymbolCode?: str /* Двухбуквенный код страны */ }
type CurrencyResult { asciiCode?: str /* Ascii код валюты */, id?: int /* Идентификатор валюты */, shortName?: str /* Краткое наименование валюты */ }
type DocumentStatuses.ListResult { code?: str /* Код складского документа */, name?: str /* Имя статуса складского документа */ }
type DocumentTypes.ListResult { code?: str /* Код типа складского документа */, name?: str /* Имя типа складского документа */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type FromBodyUploadData { checkSum?: str, contentLength?: int, contentStream?: file, contentType: str, coordinate?: str, description?: str, file: str, fileName: str, isIgnorePossibleDuplication?: bool, isPublic?: bool, md5Hash?: str, roles?: int[], uid?: uuid }
type FromFormUploadData { contentLength?: int, contentStream?: file, contentType?: str, coordinate?: str, description?: str, file: file, fileName?: str, isIgnorePossibleDuplication?: bool, isPublic?: bool, md5Hash?: str, roles?: int[], uid?: uuid }
type GetResult { deleted?: datetime /* Дата удаления склада */, deletedBy?: int /* Член тенанта, который удалил склад */, description?: str /* Описание склада */, erpID?: str /* Идентификатор склада в сторонней системе */, id?: int, isDefault?: bool /* Признак склада по умолчанию */, location?: LocationResult, name?: str }
type IdCodeNameResult<Byte> { code?: str, id?: int, name?: str }
type IdNameDeletedResult<Int32> { deleted?: datetime, id?: int, name?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type Inventories.ListResult { dateFrom?: datetime /* Дата начала инвентаризации */, dateTill?: datetime /* Дата окончания инвентаризации */, id?: int /* Идентификатор инвентаризации */ }
type Inventories.PostResult { dateFrom?: datetime /* Дата начала инвентаризации */, dateTill?: datetime /* Дата окончания инвентаризации */, id?: int /* Идентификатор инвентаризации */ }
type Inventory.AddData { inventoryDateFrom: datetime, materials?: InventoryMaterialData[] }
type Inventory.UpdateData { inventoryDateFrom?: datetime, inventoryID: int, materials?: InventoryMaterialData[] }
type InventoryMaterialData { materialCost?: float, materialCurrencyID?: int, materialErpID?: str, materialName?: str, measurementUnitID?: int, quantity?: float, warehouseErpID?: str, warehouseName?: str }
type Issue.AddData { description?: str, documentDate?: datetime, erpID?: str, number?: str, operationTypeID: int, relatedTaskID?: int, responsiblePersonID?: int, warehouseID: int }
type Issue.UpdateData { description?: str, documentDate?: datetime, erpID?: str, id?: int, number?: str, operationTypeID: int, relatedTaskID?: int, responsiblePersonID?: int, warehouseID: int }
type IssueItemData { materialID: int, measurementUnitID: int, quantity: float, sortOrder: int }
type IssueItemDeleteData { issueID?: int, items?: int[] }
type IssueItemMergeData { issueID?: int, items?: IssueItemData[] }
type IssueItems.ListResult { issueID?: int /* Идентификатор списания материалов */, material?: MaterialResult, measurementUnit?: IdNameResult<Int16>, quantity?: float /* Количество материала */, sortOrder?: int /* Номер строки */ }
type IssueResult { created?: datetime /* Дата создания списания материала */, deleted?: datetime /* Дата удаления списания материала */, description?: str /* Описание документа */, documentDate?: datetime /* Дата документа */, documentStatus?: IdCodeNameResult<Byte>, erpID?: str /* Идентификатор документа во внешней системе */, id?: int, modified?: datetime /* Дата изменения списания материала */, name?: str, number?: str /* Номер документа */, operationType?: IdNameResult<Int16>, posted?: datetime /* Дата проведения списания материала */, relatedTaskID?: int /* Идентификатор связанной заявки */, responsiblePerson?: IdNameResult<Int32>, taskNumber?: str /* Номер связанной заявки */, warehouseID?: int /* Идентификатор склада */, warehouseName?: str /* Название склада */ }
type ListRequiredResult { actualQuantity?: float /* Акутальное количество */, cost?: float /* Стоимость материала */, currency?: CurrencyResult, description?: str /* Описание материала */, erpID?: str /* Код материала */, id?: int /* Идентификатор материала */, importQuantity?: float /* Импортированное количество */, materialIsMarkable?: bool /* Признак обязательности маркировки */, measurementUnit?: IdNameResult<Int16>, name?: str /* Наименование материала */, sortOrder?: int /* Индекс сортировки */, vendorCode?: str /* Код поставщика */, warehouse?: WarehouseResult }
type ListShortResult { deleted?: datetime /* Дата удаления склада */, erpID?: str /* Идентификатор склада в сторонней системе */, id?: int, isDefault?: bool /* Признак склада по умолчанию */, name?: str }
type LocationResult { address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, country?: CountryResult, deleted?: datetime /* Дата удаления */, description?: str /* Описание локации */, id?: int }
type LocationShortResult { address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, description?: str /* Описание локации */, id?: int }
type Material.AddData { cost?: float, costCurrencyID?: int, description?: str, erpID?: str, isMarkable?: bool, measurementUnitID?: int, name: str, purchaseCost?: float, purchaseCostCurrencyID?: int, vendorCode?: str }
type Material.UpdateData { cost?: float, costCurrencyID?: int, description?: str, erpID?: str, id?: int, isMarkable?: bool, measurementUnitID?: int, name: str, purchaseCost?: float, purchaseCostCurrencyID?: int, vendorCode?: str }
type MaterialActionData<Int16> { data: int[], materialID?: int }
type MaterialAttachmentListResult { created?: datetime /* Дата загрузки UTC */, description?: str /* Описание */, fileName?: str /* Название файла (с расширением) */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */, thumbnailUrl?: str /* Ссылка на эскиз изображения */ }
type MaterialAttachmentPostResult { attachmentID?: int /* Идентификатор вложения */, materialID?: int /* Идентификатор материала */, tenantID?: int /* Идентификатор тенанта */ }
type MaterialAttachmentResult { attachmentID?: int /* Идентификатор прикрепленного к материалу файла */, created?: datetime /* Дата загрузки UTC */, description?: str /* Описание */, fileName?: str /* Название файла (с расширением) */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */, thumbnailUrl?: str /* Ссылка на эскиз изображения */ }
type MaterialBarcode.AddData { barcodes?: BarcodeAddData[], materialID?: int }
type MaterialBarcode.UpdateData { barcodes?: BarcodeUpdateData[], materialID?: int }
type MaterialBarcodes.ListResult { barcodeType?: IdNameResult<Byte>, id?: int, value?: str /* Значение штрихкода */ }
type MaterialBarcodes.PostResult { id?: int, materialID?: int /* Идентификатор материала */ }
type MaterialConsumptionsResult { consumed?: datetime /* Дата последнего взятия материала */, consumedBy?: UserResult, consumption?: float /* Израсходованное количество */, cost?: float /* Стоимость материала */, currency?: CurrencyResult, description?: str /* Описание материала */, erpID?: str /* Код материала */, id?: int /* Идентификатор материала */, measurementUnit?: IdNameResult<Int16>, name?: str /* Наименование материала */, sortOrder?: int /* Индекс сортировки */, task?: TaskResult, totalCost?: float /* Общая стоимость материалов */, warehouse?: WarehouseResult }
type MaterialInventoryResult { date?: datetime /* дата импорта/инвентаризации */, id?: int /* Идентификатор импорта/инвентаризации */, materials?: MaterialConsumptionsResult[] /* Расход материалов */, sort?: int /* Ключ сортировки */ }
type MaterialListResult { cost?: float /* Закупочная стоимость материала */, costCurrency?: CurrencyResult, costCurrencyID?: int /* Валюта закупочной стоимости материала */, deleted?: datetime /* Дата удаления материала */, description?: str /* Описание материала */, erpID?: str /* Идентификатор материала во внешней системе */, id?: int, isMarkable?: bool /* Признак маркируемости материала */, measurementUnit?: MeasurementUnitResult, measurementUnitID?: int /* Единица измерения материала */, name?: str, purchaseCost?: float /* Стоимость материала для клиента */, purchaseCostCurrency?: CurrencyResult, purchaseCostCurrencyID?: int /* Валюта стоимости материала для клиента */, sortOrder?: int /* Порядок сортировки */, vendorCode?: str /* Артикул материала */ }
type MaterialResult { cost?: float /* Закупочная стоимость материала */, costCurrency?: CurrencyResult, costCurrencyID?: int /* Валюта закупочной стоимости материала */, deleted?: datetime /* Дата удаления материала */, description?: str /* Описание материала */, erpID?: str /* Идентификатор материала во внешней системе */, id?: int, isMarkable?: bool /* Признак маркируемости материала */, measurementUnit?: MeasurementUnitResult, measurementUnitID?: int /* Единица измерения материала */, name?: str, purchaseCost?: float /* Стоимость материала для клиента */, purchaseCostCurrency?: CurrencyResult, purchaseCostCurrencyID?: int /* Валюта стоимости материала для клиента */, vendorCode?: str /* Артикул материала */ }
type Materials.ListResult { actualQuantity?: float /* Акутальное количество */, cost?: float /* Стоимость материала */, currency?: CurrencyResult, description?: str /* Описание материала */, erpID?: str /* Код материала */, id?: int /* Идентификатор материала */, importQuantity?: float /* Импортированное количество */, materialIsMarkable?: bool /* Признак обязательности маркировки */, measurementUnit?: IdNameResult<Int16>, name?: str /* Наименование материала */, sortOrder?: int /* Индекс сортировки */, taken?: datetime /* Дата последнего взятия материала */, takenBy?: UserResult, task?: TaskResult, vendorCode?: str /* Код поставщика */, warehouse?: WarehouseResult }
type MeasurementUnitResult { abbreviation?: str /* Аббревиатура */, designation?: str /* Обозначение */, id?: int /* Идентификатор */, name?: str /* Наименование */ }
type ModifyData { documentTypeID: int, lastNumber?: int, prefix?: str }
type NumberSequenceResult { documentType?: IdCodeNameResult<Byte>, lastNumber?: int /* Последний занятый номер маски номера документа */, prefix?: str /* Префикс маски номера документа */ }
type OperationType.AddData { documentTypeID?: int, erpID?: str, name: str }
type OperationType.UpdateData { documentTypeID?: int, erpID?: str, id?: int, name: str }
type OperationTypeAddResult { id?: int /* Идентификатор типа операции */ }
type OperationTypeResult { deleted?: datetime /* Метка удаления типа операции */, documentType?: IdCodeNameResult<Byte>, erpID?: str /* Код типа операции во внешней системе */, id?: int /* Идентификатор типа операции */, name?: str /* Наименование типа операции */ }
type Receipt.AddData { description?: str, documentDate?: datetime, erpID?: str, number?: str, operationTypeID: int, relatedTaskID?: int, responsiblePersonID?: int, warehouseID: int }
type Receipt.UpdateData { description?: str, documentDate?: datetime, erpID?: str, id?: int, number?: str, operationTypeID: int, relatedTaskID?: int, responsiblePersonID?: int, warehouseID: int }
type ReceiptItemData { materialID: int, measurementUnitID: int, quantity: float, sortOrder: int }
type ReceiptItemDeleteData { items?: int[], receiptID?: int }
type ReceiptItemMergeData { items?: ReceiptItemData[], receiptID?: int }
type ReceiptItems.ListResult { material?: MaterialResult, measurementUnit?: IdNameResult<Int16>, quantity?: float /* Количество материала */, receiptID?: int /* Идентификатор оприходывания материалов */, sortOrder?: int /* Номер строки */ }
type ReceiptResult { created?: datetime /* Дата создания оприходывания материала */, deleted?: datetime /* Дата удаления оприходывания материала */, description?: str /* Описание документа */, documentDate?: datetime /* Дата документа */, documentStatus?: IdCodeNameResult<Byte>, erpID?: str /* Идентификатор документа во внешней системе */, id?: int, modified?: datetime /* Дата изменения оприходывания материала */, name?: str, number?: str /* Номер документа */, operationType?: IdNameResult<Int16>, posted?: datetime /* Дата проведения оприходывания материала */, relatedTaskID?: int /* Идентификатор связанной заявки */, responsiblePerson?: IdNameResult<Int32>, taskNumber?: str /* Номер связанной заявки */, warehouseID?: int /* Идентификатор склада */, warehouseName?: str /* Название склада */ }
type TaskResult { asset?: AssetResult, id?: int /* Идентификатор */, number?: str /* Наименование заявки */ }
type UploadResult { attachmentID?: int /* Идентификатор вложенного файла */, fileName?: str /* Имя загруженного файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, materialID?: int /* Идентификатор материала */, md5Hash?: str /* Проверочная сумма MD5 */ }
type UserResult { avatarUrl?: str, deleted?: datetime, firstName?: str, id?: int, lastName?: str, middleName?: str }
type UserWarehouseListResult { erpID?: str /* Код склада */, name?: str /* Наименование склада */, warehouseID?: int /* Идентификатор склада */ }
type UserWarehousesData { userID: int, warehouseIDs: int[] }
type Warehouse.AddData { description?: str, erpID?: str, isDefault?: bool, locationID?: int, name: str }
type Warehouse.UpdateData { description?: str, erpID?: str, id?: int, isDefault?: bool, locationID?: int, name: str }
type WarehouseResult { erpID?: str /* Код склада */, id?: int /* Идентификатор склада */, location?: LocationShortResult, name?: str /* Наименование склада */ }
type Warehouses.ListResult { deleted?: datetime /* Дата удаления склада */, description?: str /* Описание склада */, erpID?: str /* Идентификатор склада в сторонней системе */, id?: int, isDefault?: bool /* Признак склада по умолчанию */, location?: LocationShortResult, name?: str, userCount?: int /* Количество пользователей назначенных на склад */ }
type WarehouseUserListResult { userFullName?: str /* Полное имя пользователя */, userID?: int /* Идентификатор пользователя */ }
type WarehouseUsersData { isRelatedToAnyUser?: bool, userIDs?: int[], warehouseID: int }
type WarehouseUsersDeleteData { isRelatedToAnyUser?: bool, userIDs?: int[], warehouseID: int }
```
